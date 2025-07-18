# Technical Design: Project Setup & API Specification

## Technical Overview

### Architecture Approach
This design establishes a **Single-Page Application (SPA) with HTMX** architecture for a personal todo application. The approach uses:
- **Backend**: Go with Gin framework providing RESTful API endpoints
- **Frontend**: HTML templates enhanced with HTMX for dynamic interactions
- **Database**: SQLite for simplicity and personal use
- **Deployment**: Docker Compose for local development

### Technology Stack Justification
- **Go + Gin**: Fast, lightweight web framework with excellent performance
- **HTMX**: Enables dynamic web interactions without complex JavaScript frameworks
- **SQLite**: Zero-configuration database perfect for personal use
- **go-blueprint**: Code generation tool for consistent project structure
- **Docker**: Containerization for consistent development environment

### Key Design Decisions
1. **API-First Design**: OpenAPI specification drives development
2. **HTMX Integration**: Server-side HTML rendering with dynamic client updates
3. **Mock Data Strategy**: Initial endpoints return static data for rapid prototyping
4. **Single Container**: Simplified deployment with unified Go application

## System Architecture

### High-Level Components
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   HTMX Client   │────│   Gin Server    │────│   SQLite DB     │
│   (Browser)     │    │   (Go Backend)  │    │   (File-based)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
    HTTP Requests          API Endpoints           Database Operations
    HTML Responses         JSON/HTML Mixed         CRUD Operations
```

### Data Flow
1. **Page Load**: Browser requests `/` → Server returns HTML with HTMX scripts
2. **HTMX Actions**: User interactions trigger HTMX requests to `/api/*` endpoints
3. **API Processing**: Gin handlers process requests, interact with SQLite
4. **Response**: Server returns HTML fragments or JSON, HTMX updates DOM

### Component Interactions
- **Static Assets**: CSS/JS served directly by Gin
- **API Endpoints**: RESTful endpoints under `/api/` prefix
- **HTML Templates**: Go templates rendered server-side
- **Database**: SQLite file with automatic initialization

## Data Design

### Database Schema
```sql
CREATE TABLE todos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    description TEXT,
    completed BOOLEAN DEFAULT FALSE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### Data Model (Go Structs)
```go
type Todo struct {
    ID          int       `json:"id" db:"id"`
    Title       string    `json:"title" db:"title" binding:"required"`
    Description string    `json:"description" db:"description"`
    Completed   bool      `json:"completed" db:"completed"`
    CreatedAt   time.Time `json:"created_at" db:"created_at"`
    UpdatedAt   time.Time `json:"updated_at" db:"updated_at"`
}
```

### Data Validation
- **Title**: Required, max 255 characters
- **Description**: Optional, max 1000 characters
- **Completed**: Boolean, defaults to false
- **Timestamps**: Auto-managed by database

## API Design

### Endpoint Specifications
```yaml
/api/todos:
  GET:    # List all todos
    responses:
      200: Todo[]
  POST:   # Create new todo
    request: {title, description}
    responses:
      201: Todo

/api/todos/{id}:
  GET:    # Get specific todo
    responses:
      200: Todo
      404: Error
  PUT:    # Replace entire todo
    request: {title, description, completed}
    responses:
      200: Todo
      404: Error
  PATCH:  # Partial update
    request: {title?, description?, completed?}
    responses:
      200: Todo
      404: Error
  DELETE: # Remove todo
    responses:
      204: No Content
      404: Error
```

### Mock Data Strategy
Initial endpoints return static mock data:
```json
[
  {"id": 1, "title": "Learn HTMX", "description": "Build a todo app", "completed": false},
  {"id": 2, "title": "Setup Docker", "description": "Configure development environment", "completed": true},
  {"id": 3, "title": "Write Tests", "description": "Add unit and integration tests", "completed": false}
]
```

## Security Considerations

### Authentication
- **Phase 1**: No authentication (personal use, local development)
- **Future**: Basic auth or session-based authentication

### Data Protection
- **Input Validation**: Gin binding tags and custom validators
- **SQL Injection**: Parameterized queries through database/sql
- **XSS Prevention**: HTML template escaping enabled by default

### Access Control
- **Network**: Docker container isolation
- **Database**: File-based SQLite with container-only access
- **API**: Rate limiting for production use (future enhancement)

## Performance & Scalability

### Performance Targets
- **Startup Time**: < 10 seconds (requirement)
- **API Response**: < 1 second (requirement)
- **Database**: SQLite sufficient for personal use (< 1000 todos)

### Caching Strategy
- **Static Assets**: Gin static middleware with cache headers
- **Database**: In-memory caching for frequently accessed data (future)
- **Templates**: Compiled templates cached in memory

### Database Optimization
- **Indexes**: Primary key on ID, index on created_at for sorting
- **Connection Pool**: Single connection sufficient for SQLite
- **Query Optimization**: Simple queries with minimal joins

## Implementation Approach

### Development Phases
1. **Phase 1**: OpenAPI specification definition
2. **Phase 2**: go-blueprint code generation
3. **Phase 3**: Docker Compose setup
4. **Phase 4**: Mock endpoint implementation
5. **Phase 5**: HTMX frontend integration

### Testing Strategy
- **Unit Tests**: Go standard testing for handlers and models
- **Integration Tests**: HTTP endpoint testing with test database
- **Manual Testing**: Browser testing of HTMX interactions
- **API Testing**: OpenAPI spec validation

### Deployment Plan
```yaml
# docker-compose.yml structure
version: '3.8'
services:
  todo-app:
    build: .
    ports:
      - "8080:8080"
    volumes:
      - ./data:/app/data
    environment:
      - DB_PATH=/app/data/todos.db
```

## File Structure
```
todo-app/
├── api/
│   └── openapi.yaml          # OpenAPI specification
├── cmd/
│   └── server/
│       └── main.go           # Application entry point
├── internal/
│   ├── handlers/             # Gin route handlers
│   ├── models/              # Data models
│   ├── database/            # Database operations
│   └── middleware/          # Custom middleware
├── templates/               # HTML templates
├── static/                  # CSS, JS, HTMX files
├── docker-compose.yml       # Local development setup
├── Dockerfile              # Container definition
└── go.mod                  # Go dependencies
```

## Error Handling

### HTTP Status Codes
- **200**: Successful GET/PUT/PATCH
- **201**: Successful POST (created)
- **204**: Successful DELETE (no content)
- **400**: Bad Request (validation errors)
- **404**: Not Found (invalid todo ID)
- **500**: Internal Server Error

### Error Response Format
```json
{
  "error": "descriptive error message",
  "code": "ERROR_CODE",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### HTMX Error Handling
- **Client-side**: HTMX error events for user feedback
- **Server-side**: HTML error fragments for inline display
- **Fallback**: Full page reload on critical errors

## Documentation & Developer Experience

### OpenAPI Integration
- **Specification**: Complete API documentation at `/docs`
- **Interactive**: Swagger UI for API testing
- **Validation**: Request/response validation against spec

### Hot-Reload Support
- **Air**: Live reloading for Go code changes
- **Docker**: Volume mounts for development
- **Templates**: Automatic template recompilation

### Logging & Monitoring
- **Structured Logs**: JSON format for easier parsing
- **Request Logging**: HTTP request/response details
- **Error Tracking**: Detailed error context and stack traces