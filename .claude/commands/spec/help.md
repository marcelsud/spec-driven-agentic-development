---
description: Display help information for spec:driven development commands
allowed-tools: Read(*)
---

# Spec-Driven Development Help

Quick reference for the spec:driven development methodology.

## Available Commands

| Command | Description |
|---------|-------------|
| `/spec:create [feature]` | Generate complete specification (context + requirements + tasks) |
| `/spec:execute [feature]` | Execute implementation from tasks.md |
| `/spec:status` | Show implementation status of all features |
| `/spec:list` | List all available features |
| `/spec:help` | Display this help |

## Workflow

```
/spec:create [feature]  →  context.md + requirements.md + tasks.md
/spec:execute [feature] →  Implementation following TDD
```

## `/spec:create` Flow

1. **Initial Questions** - Gather context (goal, scope, tech stack, constraints)
2. **context.md** - Project context + technical decisions
3. **requirements.md** - EARS-formatted requirements
4. **Pre-planning Questions** - Clarify implementation approach
5. **tasks.md** - TDD task breakdown

## EARS Requirements Format

| Type | Template |
|------|----------|
| Ubiquitous | "The system SHALL [requirement]" |
| Event-Driven | "WHEN [trigger] THEN the system SHALL [response]" |
| State-Driven | "WHILE [state] the system SHALL [requirement]" |
| Conditional | "IF [condition] THEN the system SHALL [requirement]" |
| Optional | "WHERE [feature] the system SHALL [requirement]" |

## TDD Cycle

1. **Red**: Write failing test
2. **Green**: Minimal code to pass
3. **Refactor**: Improve while green

## File Structure

```
features/[feature-name]/
├── context.md      # Context + technical decisions
├── requirements.md # EARS requirements
└── tasks.md        # TDD implementation tasks
```

## Example Usage

```bash
# Create new feature specification
/spec:create user-authentication

# View all features
/spec:list

# Check status
/spec:status

# Implement feature
/spec:execute user-authentication
```

## More Info

See `.claude/CLAUDE.md` for complete methodology.
