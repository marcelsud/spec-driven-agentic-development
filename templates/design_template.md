# Design: [Feature Name]

## Architecture Overview

### High-Level Architecture
- **Architecture Pattern**: [MVC/MVP/MVVM/Microservices/etc.]
- **Technology Stack**: [Languages, frameworks, databases]
- **Deployment Model**: [Cloud/On-premise/Hybrid]

### Design Principles
- [Principle 1: e.g., Single Responsibility]
- [Principle 2: e.g., Separation of Concerns]
- [Principle 3: e.g., Dependency Inversion]

### Technology Stack Selection
- **Backend**: [Framework/Language] - [Rationale]
- **Frontend**: [Framework/Language] - [Rationale]
- **Database**: [Database type] - [Rationale]
- **Cache**: [Caching solution] - [Rationale]
- **Message Queue**: [If applicable] - [Rationale]

## Data Model

### Database Schema
```sql
-- Table definitions
CREATE TABLE [table_name] (
    id INTEGER PRIMARY KEY,
    [field_name] [TYPE] [CONSTRAINTS],
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Add foreign key relationships
ALTER TABLE [table_name] ADD CONSTRAINT [constraint_name] 
    FOREIGN KEY ([field_name]) REFERENCES [referenced_table]([field_name]);
```

### Entity Relationships
- **[Entity1]** has relationship with **[Entity2]**
- **[Entity2]** belongs to **[Entity3]**
- **[Entity3]** can have many **[Entity1]**

### Data Validation Rules
- [Field]: [Validation rule, e.g., required, min/max length, format]
- [Field]: [Validation rule]
- [Field]: [Validation rule]

## API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `POST /api/auth/refresh` - Token refresh

### Core Endpoints
```
GET /api/[resource]
- Description: [What this endpoint does]
- Parameters: [Query parameters]
- Response: [Response format]
- Status Codes: 200, 400, 401, 403, 404, 500

POST /api/[resource]
- Description: [What this endpoint does]
- Request Body: [JSON structure]
- Response: [Response format]
- Status Codes: 201, 400, 401, 403, 409, 500

PUT /api/[resource]/{id}
- Description: [What this endpoint does]
- Parameters: {id} - [Resource identifier]
- Request Body: [JSON structure]
- Response: [Response format]
- Status Codes: 200, 400, 401, 403, 404, 500

DELETE /api/[resource]/{id}
- Description: [What this endpoint does]
- Parameters: {id} - [Resource identifier]
- Response: [Response format]
- Status Codes: 204, 401, 403, 404, 500
```

### Request/Response Examples
```json
// POST /api/[resource] Request
{
    "[field1]": "[value1]",
    "[field2]": "[value2]"
}

// POST /api/[resource] Response
{
    "id": 1,
    "[field1]": "[value1]",
    "[field2]": "[value2]",
    "created_at": "2024-01-01T00:00:00Z",
    "updated_at": "2024-01-01T00:00:00Z"
}
```

## Application Structure

### Directory Structure
```
project/
├── src/
│   ├── controllers/        # Request handlers
│   ├── models/            # Data models
│   ├── routes/            # Route definitions
│   ├── middleware/        # Custom middleware
│   ├── services/          # Business logic
│   ├── utils/             # Utility functions
│   └── config/            # Configuration
├── tests/                 # Test files
├── migrations/            # Database migrations
└── docs/                  # Documentation
```

### Module Responsibilities
- **Controllers**: Handle HTTP requests and responses
- **Models**: Define data structures and database interactions
- **Services**: Implement business logic
- **Middleware**: Handle cross-cutting concerns
- **Utils**: Provide helper functions
- **Config**: Manage application configuration

## Error Handling

### Error Response Format
```json
{
    "error": {
        "code": "[ERROR_CODE]",
        "message": "[Human-readable message]",
        "details": "[Additional details]",
        "timestamp": "[ISO 8601 timestamp]"
    }
}
```

### HTTP Status Code Strategy
- **200 OK**: Successful GET, PUT
- **201 Created**: Successful POST
- **204 No Content**: Successful DELETE
- **400 Bad Request**: Invalid input
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: Access denied
- **404 Not Found**: Resource not found
- **409 Conflict**: Resource conflict
- **500 Internal Server Error**: Server error

### Global Error Handling
- Centralized error handling middleware
- Consistent error response format
- Appropriate logging for different error types
- Graceful degradation for non-critical failures

## Data Validation

### Input Validation Strategy
- **Request Level**: Validate all incoming requests
- **Field Level**: Validate individual fields
- **Business Rule Level**: Validate business logic constraints
- **Database Level**: Database constraints as final check

### Validation Rules
```javascript
// Example validation schema
const [resourceSchema] = {
    [field1]: {
        required: true,
        type: 'string',
        minLength: 1,
        maxLength: 100
    },
    [field2]: {
        required: false,
        type: 'email'
    }
};
```

## Advanced Considerations (Optional)

### Security Considerations
- Input sanitization and validation
- SQL injection prevention
- XSS protection
- CSRF protection
- Rate limiting
- Data encryption at rest and in transit

### Performance Considerations
- Database indexing strategy
- Caching implementation
- Connection pooling
- Query optimization
- Asynchronous processing

### Monitoring and Logging
- Application performance monitoring
- Error tracking and alerting
- Audit logging
- Security event logging
- Performance metrics collection

## Template Usage Notes
- Replace [bracketed placeholders] with actual values
- Include concrete examples for all API endpoints
- Provide actual database schema definitions
- Consider all requirements from requirements.md
- Add advanced sections if using advanced mode
- Review technical approach before proceeding to tasks