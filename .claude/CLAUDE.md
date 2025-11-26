# Spec-Driven Agentic Development Methodology

A streamlined approach to software development that generates complete feature specifications efficiently.

## Core Workflow

### Single Command Flow
Run `/spec:create [feature-description]` to generate a complete specification:

1. **Initial Questions** - Gather context via AskUserQuestion tool
2. **context.md** - Project context + technical decisions
3. **requirements.md** - EARS-formatted requirements
4. **Pre-planning Questions** - Clarify implementation approach
5. **tasks.md** - TDD task breakdown
6. **Implementation** - Run `/spec:execute [feature-name]` to implement

### Key Principles
- **Efficient**: Single command generates all spec files
- **Interactive**: Uses AskUserQuestion for clarification (not approval gates)
- **EARS Requirements**: Structured requirement syntax for clarity
- **TDD Ready**: Tasks include test scenarios

## EARS Format (Easy Approach to Requirements Syntax)

### Templates
1. **Ubiquitous**: "The system SHALL [requirement]"
2. **Event-Driven**: "WHEN [trigger] THEN the system SHALL [response]"  
3. **State-Driven**: "WHILE [state] the system SHALL [requirement]"
4. **Conditional**: "IF [condition] THEN the system SHALL [requirement]"
5. **Optional**: "WHERE [feature included] the system SHALL [requirement]"

### Best Practices
- Use active voice and "SHALL" for mandatory requirements
- Be specific and measurable (avoid "quickly", use "within 2 seconds")
- One requirement per statement
- Avoid ambiguous terms ("appropriate", "reasonable", "user-friendly")

### Examples
- "WHEN a user enters incorrect credentials three times THEN the system SHALL lock the account for 15 minutes"
- "WHILE processing a payment the system SHALL display a loading indicator"
- "IF inventory is insufficient THEN the system SHALL display an out-of-stock message"

## Test-Driven Development (TDD)

### Red-Green-Refactor Cycle
1. **Red**: Write a failing test for next functionality
2. **Green**: Write minimal code to make test pass
3. **Refactor**: Improve code while keeping tests green

### Benefits
- Requirements validation through executable tests
- Early design feedback and issue detection
- Built-in documentation through test scenarios
- Safe refactoring with comprehensive test coverage

### Implementation Flow
1. Start with acceptance criteria from tasks as test scenarios
2. Write unit tests for components and functions
3. Write integration tests for APIs and data operations
4. Implement code incrementally to satisfy tests
5. Refactor continuously while maintaining green tests

## File Structure

```
features/
└── [feature-name]/
    ├── context.md      # Context + technical decisions
    ├── requirements.md # EARS-formatted requirements
    └── tasks.md        # Implementation tasks
```

## Slash Commands

- `/spec:create [feature]` - Generate complete specification (context + requirements + tasks)
- `/spec:execute [feature]` - Execute implementation from tasks.md
- `/spec:status` - Show implementation status
- `/spec:list` - List all features

