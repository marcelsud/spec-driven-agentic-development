# User Authentication System - Technical Design

## Technical Overview

### Architecture Approach
RESTful API-first authentication service built with Node.js, designed as a stateless microservice that can be integrated into any frontend application or consumed by other services.

### Technology Stack
- **Runtime**: Node.js 18+ with TypeScript
- **Framework**: Express.js with helmet, cors, and compression middleware
- **Database**: PostgreSQL 15+ for user data with Redis for session storage
- **Authentication**: JWT tokens with refresh token rotation
- **Password Hashing**: bcrypt with 12 salt rounds
- **API Documentation**: OpenAPI 3.0 specification with Swagger UI
- **Validation**: Joi for request validation and sanitization
- **Email**: Nodemailer with SMTP transport
- **Logging**: Winston with structured logging
- **Rate Limiting**: express-rate-limit with Redis store
- **Testing**: Jest for unit/integration tests
- **Containerization**: Docker with multi-stage builds

### Key Design Decisions
1. **JWT + Refresh Tokens**: Stateless authentication with secure refresh mechanism
2. **Separate Session Storage**: Redis for fast session invalidation and rate limiting
3. **Email Queue System**: Background job processing for reliable email delivery
4. **Database-First Approach**: PostgreSQL constraints and indexes for data integrity
5. **OpenAPI-First**: API specification drives implementation and testing

## System Architecture

### High-Level Components
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   API Gateway   │────│  Auth Service   │────│   PostgreSQL    │
│  (Rate Limiting)│    │   (Node.js)     │    │   (User Data)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                       ┌─────────────────┐    ┌─────────────────┐
                       │      Redis      │    │  Email Service  │
                       │   (Sessions)    │    │  (Background)   │
                       └─────────────────┘    └─────────────────┘
```

### Component Interactions
1. **Request Flow**: Client → API Gateway → Auth Service → Database
2. **Session Management**: Auth Service ↔ Redis for token validation
3. **Email Processing**: Auth Service → Queue → Background Worker → SMTP
4. **Rate Limiting**: API Gateway + Redis for distributed rate limiting
5. **Audit Logging**: Auth Service → Structured Logs → Log Aggregation

### Integration Points
- **OpenAPI Specification**: `/api/docs` endpoint with Swagger UI
- **Health Checks**: `/health` endpoint for monitoring
- **Metrics**: Prometheus metrics for observability
- **CORS**: Configurable origins for frontend integration

## Data Design

### Database Schema

#### Users Table
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    email_verified BOOLEAN DEFAULT FALSE,
    account_locked_until TIMESTAMP,
    failed_login_attempts INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT valid_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$')
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_email_verified ON users(email_verified);
CREATE INDEX idx_users_account_locked ON users(account_locked_until) WHERE account_locked_until IS NOT NULL;
```

#### Email Verification Tokens Table
```sql
CREATE TABLE email_verification_tokens (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    token VARCHAR(255) UNIQUE NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    used_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT valid_expiry CHECK (expires_at > created_at)
);

CREATE INDEX idx_verification_tokens_token ON email_verification_tokens(token);
CREATE INDEX idx_verification_tokens_user_id ON email_verification_tokens(user_id);
CREATE INDEX idx_verification_tokens_expires ON email_verification_tokens(expires_at);
```

#### Password Reset Tokens Table
```sql
CREATE TABLE password_reset_tokens (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    token VARCHAR(255) UNIQUE NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    used_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT valid_expiry CHECK (expires_at > created_at)
);

CREATE INDEX idx_reset_tokens_token ON password_reset_tokens(token);
CREATE INDEX idx_reset_tokens_user_id ON password_reset_tokens(user_id);
CREATE INDEX idx_reset_tokens_expires ON password_reset_tokens(expires_at);
```

#### Refresh Tokens Table
```sql
CREATE TABLE refresh_tokens (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    token_hash VARCHAR(255) UNIQUE NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    revoked_at TIMESTAMP,
    device_info JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    CONSTRAINT valid_expiry CHECK (expires_at > created_at)
);

CREATE INDEX idx_refresh_tokens_user_id ON refresh_tokens(user_id);
CREATE INDEX idx_refresh_tokens_expires ON refresh_tokens(expires_at);
CREATE INDEX idx_refresh_tokens_token_hash ON refresh_tokens(token_hash);
```

#### Audit Logs Table
```sql
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id),
    action VARCHAR(100) NOT NULL,
    resource VARCHAR(100),
    ip_address INET,
    user_agent TEXT,
    success BOOLEAN NOT NULL,
    error_message TEXT,
    metadata JSONB,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_audit_logs_user_id ON audit_logs(user_id);
CREATE INDEX idx_audit_logs_action ON audit_logs(action);
CREATE INDEX idx_audit_logs_created_at ON audit_logs(created_at);
CREATE INDEX idx_audit_logs_ip_address ON audit_logs(ip_address);
```

### Redis Data Structures
```
# Rate limiting
rate_limit:login:{ip_address} → count with TTL
rate_limit:register:{ip_address} → count with TTL
rate_limit:reset:{email} → count with TTL

# Session blacklist (for logout)
session_blacklist:{token_id} → "revoked" with TTL

# Email queue
email_queue → LIST of email job objects
```

## API Design

### OpenAPI 3.0 Specification Structure

#### Base Configuration
```yaml
openapi: 3.0.3
info:
  title: User Authentication API
  version: 1.0.0
  description: Secure user authentication and session management service
servers:
  - url: https://api.example.com/v1
    description: Production server
  - url: http://localhost:3000/v1
    description: Development server
```

#### Core Endpoints

##### Authentication Endpoints
```yaml
/auth/register:
  post:
    summary: Register new user
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [email, password]
            properties:
              email:
                type: string
                format: email
                example: user@example.com
              password:
                type: string
                minLength: 8
                pattern: ^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]
    responses:
      201:
        description: User registered successfully
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/AuthResponse'
      400:
        $ref: '#/components/responses/ValidationError'
      409:
        $ref: '#/components/responses/ConflictError'
      429:
        $ref: '#/components/responses/RateLimitError'

/auth/login:
  post:
    summary: Authenticate user
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [email, password]
            properties:
              email:
                type: string
                format: email
              password:
                type: string
    responses:
      200:
        description: Login successful
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginResponse'
      400:
        $ref: '#/components/responses/ValidationError'
      401:
        $ref: '#/components/responses/UnauthorizedError'
      423:
        $ref: '#/components/responses/AccountLockedError'
      429:
        $ref: '#/components/responses/RateLimitError'

/auth/logout:
  post:
    summary: Logout user and invalidate tokens
    security:
      - bearerAuth: []
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      401:
        $ref: '#/components/responses/UnauthorizedError'

/auth/refresh:
  post:
    summary: Refresh access token
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [refreshToken]
            properties:
              refreshToken:
                type: string
    responses:
      200:
        description: Token refreshed successfully
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/TokenResponse'
      401:
        $ref: '#/components/responses/UnauthorizedError'
```

##### Email Verification Endpoints
```yaml
/auth/verify-email:
  post:
    summary: Verify email address
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [token]
            properties:
              token:
                type: string
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      400:
        $ref: '#/components/responses/ValidationError'
      410:
        $ref: '#/components/responses/ExpiredTokenError'

/auth/resend-verification:
  post:
    summary: Resend email verification
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [email]
            properties:
              email:
                type: string
                format: email
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      429:
        $ref: '#/components/responses/RateLimitError'
```

##### Password Reset Endpoints
```yaml
/auth/forgot-password:
  post:
    summary: Request password reset
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [email]
            properties:
              email:
                type: string
                format: email
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      429:
        $ref: '#/components/responses/RateLimitError'

/auth/reset-password:
  post:
    summary: Reset password with token
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [token, password]
            properties:
              token:
                type: string
              password:
                type: string
                minLength: 8
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      400:
        $ref: '#/components/responses/ValidationError'
      410:
        $ref: '#/components/responses/ExpiredTokenError'
```

##### User Profile Endpoints
```yaml
/user/profile:
  get:
    summary: Get user profile
    security:
      - bearerAuth: []
    responses:
      200:
        description: User profile retrieved
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserProfile'
      401:
        $ref: '#/components/responses/UnauthorizedError'
  patch:
    summary: Update user profile
    security:
      - bearerAuth: []
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            properties:
              email:
                type: string
                format: email
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      400:
        $ref: '#/components/responses/ValidationError'
      401:
        $ref: '#/components/responses/UnauthorizedError'

/user/change-password:
  post:
    summary: Change user password
    security:
      - bearerAuth: []
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [currentPassword, newPassword]
            properties:
              currentPassword:
                type: string
              newPassword:
                type: string
                minLength: 8
    responses:
      200:
        $ref: '#/components/responses/SuccessMessage'
      400:
        $ref: '#/components/responses/ValidationError'
      401:
        $ref: '#/components/responses/UnauthorizedError'
```

### Response Schemas
```yaml
components:
  schemas:
    AuthResponse:
      type: object
      properties:
        message:
          type: string
          example: "User registered successfully. Please check your email for verification."
        userId:
          type: string
          format: uuid
    
    LoginResponse:
      type: object
      properties:
        accessToken:
          type: string
        refreshToken:
          type: string
        expiresIn:
          type: integer
          example: 3600
        tokenType:
          type: string
          example: "Bearer"
    
    UserProfile:
      type: object
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
          format: email
        emailVerified:
          type: boolean
        createdAt:
          type: string
          format: date-time
        updatedAt:
          type: string
          format: date-time
    
    Error:
      type: object
      properties:
        error:
          type: string
        message:
          type: string
        details:
          type: array
          items:
            type: string
```

## Security Considerations

### Authentication Mechanisms
1. **JWT Access Tokens**: Short-lived (15 minutes) with essential claims
2. **Refresh Token Rotation**: New refresh token issued on each use
3. **Token Blacklisting**: Redis-based session invalidation for logout
4. **Device Tracking**: Store device info with refresh tokens

### Data Protection and Encryption
1. **Password Hashing**: bcrypt with 12 salt rounds (configurable)
2. **Token Security**: Cryptographically secure random generation
3. **Data at Rest**: PostgreSQL encryption + Redis AUTH
4. **Data in Transit**: TLS 1.3 enforced with HSTS headers
5. **Sensitive Data**: No passwords in logs, sanitized error messages

### Input Validation and Sanitization
1. **Request Validation**: Joi schemas for all inputs
2. **SQL Injection Prevention**: Parameterized queries only
3. **XSS Prevention**: Input sanitization and CSP headers
4. **Email Validation**: RFC 5322 compliant regex + DNS verification

### Access Control and Permissions
1. **Role-Based Access**: Extensible role system in JWT claims
2. **Resource Ownership**: User can only access own resources
3. **API Rate Limiting**: Per-endpoint and per-user limits
4. **CORS Configuration**: Configurable allowed origins

## Performance & Scalability

### Performance Targets
- **Authentication**: < 1 second (requirement: 1 second)
- **Registration**: < 2 seconds (requirement: 2 seconds)
- **Database Queries**: < 100ms for single-record operations
- **Throughput**: 1000 concurrent users, 10,000 requests/minute

### Caching Strategies
1. **Redis Session Cache**: O(1) token validation lookup
2. **Database Connection Pooling**: pg-pool with 10-50 connections
3. **Rate Limit Cache**: Redis with TTL for distributed limiting
4. **Email Queue**: Redis-backed job queue for async processing

### Database Optimization
1. **Indexes**: Strategic indexing on lookup columns (email, tokens)
2. **Partitioning**: Audit logs partitioned by month
3. **Connection Limits**: Managed pool with circuit breaker pattern
4. **Query Optimization**: Prepared statements and query analysis

### Scaling Considerations
1. **Horizontal Scaling**: Stateless design allows multiple instances
2. **Database Scaling**: Read replicas for audit log queries
3. **Redis Clustering**: Session storage can be clustered
4. **Load Balancing**: Sticky sessions not required

## Implementation Approach

### Development Phases
1. **Phase 1**: Core authentication (register, login, JWT)
2. **Phase 2**: Email verification and password reset
3. **Phase 3**: User profile management and security features
4. **Phase 4**: Advanced logging, monitoring, and optimization

### Testing Strategy Alignment
1. **Unit Tests**: Service layer functions and utilities
2. **Integration Tests**: API endpoints with test database
3. **Security Tests**: Authentication flows and edge cases
4. **Performance Tests**: Load testing with k6 or Artillery
5. **Contract Tests**: OpenAPI specification validation

### Deployment and Rollout Plan
1. **Containerization**: Multi-stage Docker builds
2. **Environment Config**: 12-factor app with environment variables
3. **Database Migrations**: Automated with migration scripts
4. **Blue-Green Deployment**: Zero-downtime deployments
5. **Monitoring**: Health checks, metrics, and alerting

### Dependencies and External Services
- **Database**: PostgreSQL 15+ (persistent storage)
- **Cache**: Redis 6+ (sessions, rate limiting)
- **Email**: SMTP service (SendGrid, AWS SES, or similar)
- **Secrets**: Environment variables or secret management
- **Monitoring**: Optional integration with Prometheus/Grafana

### Error Handling Strategy
1. **Global Error Handler**: Centralized error processing
2. **Structured Logging**: JSON logs with correlation IDs
3. **Graceful Degradation**: Service degradation under load
4. **Circuit Breaker**: External service failure handling
5. **Retry Logic**: Exponential backoff for transient failures