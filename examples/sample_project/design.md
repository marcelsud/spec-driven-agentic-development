# Design: Task Management API

## Architecture Overview

### High-Level Architecture
- **Architecture Pattern**: REST API with MVC pattern
- **Technology Stack**: Node.js, Express.js, PostgreSQL, Redis
- **Deployment Model**: Containerized deployment with Docker

### Design Principles
- Single Responsibility: Each module has one clear purpose
- Separation of Concerns: Business logic separated from HTTP concerns
- Dependency Inversion: Controllers depend on service abstractions
- Open/Closed: Extensible design for new features

### Technology Stack Selection
- **Backend**: Node.js with Express.js - Fast development, excellent JSON handling
- **Database**: PostgreSQL - ACID compliance, strong data integrity
- **Cache**: Redis - Fast in-memory storage for session data
- **Testing**: Jest - Comprehensive testing framework
- **Validation**: Joi - Schema validation library

## Data Model

### Database Schema
```sql
-- Users table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tasks table
CREATE TABLE tasks (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL,
    title VARCHAR(200) NOT NULL,
    description TEXT,
    status VARCHAR(20) DEFAULT 'pending',
    due_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- Add indexes for performance
CREATE INDEX idx_tasks_user_id ON tasks(user_id);
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_tasks_due_date ON tasks(due_date);
```

### Entity Relationships
- **User** has many **Tasks** (one-to-many)
- **Task** belongs to one **User**
- Tasks are deleted when user is deleted (cascade)

### Data Validation Rules
- title: Required, 1-200 characters
- description: Optional, max 1000 characters
- status: Must be 'pending', 'in_progress', or 'completed'
- due_date: Optional, must be valid date format (YYYY-MM-DD)
- user_id: Required, must reference existing user

## API Endpoints

### Authentication (Future Enhancement)
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `POST /api/auth/logout` - User logout

### Task Management
```
GET /api/tasks
- Description: Retrieve all tasks for authenticated user
- Parameters: 
  - page (optional): Page number for pagination (default: 1)
  - limit (optional): Items per page (default: 10, max: 100)
  - status (optional): Filter by status
- Response: Array of task objects with pagination metadata
- Status Codes: 200, 400, 401, 500

POST /api/tasks
- Description: Create a new task
- Request Body: Task object without id, user_id, timestamps
- Response: Created task object
- Status Codes: 201, 400, 401, 422, 500

GET /api/tasks/{id}
- Description: Retrieve specific task by ID
- Parameters: {id} - Task identifier (integer)
- Response: Task object
- Status Codes: 200, 400, 401, 404, 500

PUT /api/tasks/{id}
- Description: Update existing task
- Parameters: {id} - Task identifier (integer)
- Request Body: Task object with fields to update
- Response: Updated task object
- Status Codes: 200, 400, 401, 404, 422, 500

DELETE /api/tasks/{id}
- Description: Delete specific task
- Parameters: {id} - Task identifier (integer)
- Response: Empty response
- Status Codes: 204, 401, 404, 500
```

### Request/Response Examples
```json
// POST /api/tasks Request
{
    "title": "Complete project documentation",
    "description": "Write comprehensive API documentation",
    "status": "pending",
    "due_date": "2024-12-31"
}

// POST /api/tasks Response
{
    "id": 1,
    "title": "Complete project documentation",
    "description": "Write comprehensive API documentation",
    "status": "pending",
    "due_date": "2024-12-31",
    "user_id": 1,
    "created_at": "2024-01-15T10:30:00Z",
    "updated_at": "2024-01-15T10:30:00Z"
}

// GET /api/tasks Response
{
    "data": [
        {
            "id": 1,
            "title": "Complete project documentation",
            "description": "Write comprehensive API documentation",
            "status": "pending",
            "due_date": "2024-12-31",
            "user_id": 1,
            "created_at": "2024-01-15T10:30:00Z",
            "updated_at": "2024-01-15T10:30:00Z"
        }
    ],
    "pagination": {
        "current_page": 1,
        "per_page": 10,
        "total": 1,
        "total_pages": 1
    }
}
```

## Application Structure

### Directory Structure
```
task-api/
├── src/
│   ├── controllers/        # Request handlers
│   │   └── taskController.js
│   ├── models/            # Data models
│   │   └── Task.js
│   ├── routes/            # Route definitions
│   │   └── taskRoutes.js
│   ├── middleware/        # Custom middleware
│   │   ├── validation.js
│   │   ├── errorHandler.js
│   │   └── rateLimit.js
│   ├── services/          # Business logic
│   │   └── taskService.js
│   ├── utils/             # Utility functions
│   │   ├── database.js
│   │   └── logger.js
│   └── config/            # Configuration
│       ├── database.js
│       └── server.js
├── tests/                 # Test files
│   ├── controllers/
│   ├── models/
│   └── services/
├── migrations/            # Database migrations
└── docs/                  # API documentation
```

### Module Responsibilities
- **Controllers**: Handle HTTP requests, call services, format responses
- **Models**: Define data structures and database operations
- **Services**: Implement business logic and data processing
- **Middleware**: Handle validation, error handling, rate limiting
- **Utils**: Provide database connections and logging utilities
- **Config**: Manage environment-specific configuration

## Error Handling

### Error Response Format
```json
{
    "error": {
        "code": "VALIDATION_ERROR",
        "message": "Title is required and must be between 1 and 200 characters",
        "details": {
            "field": "title",
            "value": "",
            "constraint": "required"
        },
        "timestamp": "2024-01-15T10:30:00Z"
    }
}
```

### HTTP Status Code Strategy
- **200 OK**: Successful GET, PUT operations
- **201 Created**: Successful POST (task creation)
- **204 No Content**: Successful DELETE
- **400 Bad Request**: Invalid request format or parameters
- **401 Unauthorized**: Authentication required
- **404 Not Found**: Task not found
- **422 Unprocessable Entity**: Validation errors
- **500 Internal Server Error**: Server-side errors

### Global Error Handling
- Express error handling middleware catches all errors
- Validation errors are formatted consistently
- Database errors are logged and return generic messages
- Unhandled promise rejections are caught and logged

## Data Validation

### Input Validation Strategy
- **Request Level**: Validate request structure and types
- **Field Level**: Validate individual field constraints
- **Business Rule Level**: Validate business logic rules
- **Database Level**: Database constraints as final safety net

### Validation Rules
```javascript
// Task validation schema
const taskSchema = Joi.object({
    title: Joi.string().min(1).max(200).required(),
    description: Joi.string().max(1000).allow(''),
    status: Joi.string().valid('pending', 'in_progress', 'completed').default('pending'),
    due_date: Joi.date().iso().allow(null)
});

// Task update schema (all fields optional)
const taskUpdateSchema = Joi.object({
    title: Joi.string().min(1).max(200),
    description: Joi.string().max(1000).allow(''),
    status: Joi.string().valid('pending', 'in_progress', 'completed'),
    due_date: Joi.date().iso().allow(null)
}).min(1); // At least one field must be provided
```

## Security Considerations

### Input Sanitization
- All user inputs are validated and sanitized
- SQL injection prevention through parameterized queries
- XSS prevention through input validation and output encoding

### Rate Limiting
- API endpoints are rate-limited to prevent abuse
- Different limits for different endpoint types
- Rate limit headers included in responses

### Data Protection
- Sensitive data is not logged
- Database connections use connection pooling
- Error messages don't expose internal system details

## Performance Considerations

### Database Optimization
- Indexes on frequently queried fields (user_id, status, due_date)
- Connection pooling for database connections
- Query optimization with proper WHERE clauses

### Caching Strategy
- Redis for session storage and frequently accessed data
- HTTP response caching for static content
- Database query result caching for expensive operations

### Response Optimization
- Pagination to limit response size
- Selective field return (future enhancement)
- Compression for large responses