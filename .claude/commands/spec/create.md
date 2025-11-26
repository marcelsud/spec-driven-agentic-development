---
description: Generate context, requirements, and tasks for a feature in a single unified flow.
allowed-tools: Read(*), Write(*), Edit(*), MultiEdit(*), Glob(*), Grep(*), TodoWrite, AskUserQuestion
---

# Unified Feature Specification

Generate complete feature specification (context.md, requirements.md, tasks.md) in a single streamlined flow.

## Your Task
Create a complete specification for: **$ARGUMENTS**

## Flow Overview
1. **Initial Questions** - Gather essential context
2. **Generate context.md** - Project context + technical decisions
3. **Generate requirements.md** - EARS-formatted requirements
4. **Pre-planning Questions** - Clarify implementation approach
5. **Generate tasks.md** - TDD task breakdown
6. **Summary** - Present all generated files

---

## Phase 1: Initial Questions

Use the `AskUserQuestion` tool to gather essential information. Ask 2-4 focused questions covering:

**Question Categories:**
- **Goal**: What is the main objective? What problem does this solve?
- **Scope**: What's in scope vs out of scope? MVP or full feature?
- **Tech Stack**: Any existing stack to follow? Preferences?
- **Constraints**: Performance requirements? Security concerns? Integration needs?

**Example Questions:**
```
1. "What is the main goal of this feature?"
   Options: [User-facing feature, Internal tool, API/Backend, Integration]

2. "What's the scope for this iteration?"
   Options: [MVP/Basic, Full feature, Proof of concept]

3. "Tech stack preference?"
   Options: [JavaScript/TypeScript, Python, Go, Use existing project stack, Other]
```

---

## Phase 2: Generate context.md

Create `features/[feature-name]/context.md` with:

```markdown
# [Feature Name] - Context

## Overview
Brief description of the feature and its purpose.

## Goals
- Primary goal
- Secondary goals

## Scope
### In Scope
- ...

### Out of Scope
- ...

## Technical Decisions
### Stack
- Language/Framework: ...
- Database: ...
- External services: ...

### Architecture Approach
- Pattern: ...
- Key components: ...

### Key Design Decisions
1. **Decision**: [What] - **Rationale**: [Why]
2. ...

## Constraints & Considerations
- Performance: ...
- Security: ...
- Integration: ...

## Dependencies
- External: ...
- Internal: ...
```

---

## Phase 3: Generate requirements.md

Create `features/[feature-name]/requirements.md` using EARS format:

```markdown
# [Feature Name] - Requirements

## Functional Requirements

### Core Functionality
- REQ-001: WHEN [trigger] THEN the system SHALL [response]
- REQ-002: The system SHALL [requirement]
- REQ-003: IF [condition] THEN the system SHALL [behavior]

### User Interactions
- REQ-010: WHEN [user action] THEN the system SHALL [response]

### Data Management
- REQ-020: The system SHALL [data requirement]

## Non-Functional Requirements

### Performance
- NFR-001: The system SHALL [performance requirement]

### Security
- NFR-010: The system SHALL [security requirement]

### Reliability
- NFR-020: WHILE [state] the system SHALL [behavior]

## Acceptance Criteria Summary
- [ ] Criterion 1
- [ ] Criterion 2
```

### EARS Templates Reference
- **Ubiquitous**: "The system SHALL [requirement]"
- **Event-Driven**: "WHEN [trigger] THEN the system SHALL [response]"
- **State-Driven**: "WHILE [state] the system SHALL [requirement]"
- **Conditional**: "IF [condition] THEN the system SHALL [requirement]"
- **Optional**: "WHERE [feature included] the system SHALL [requirement]"

---

## Phase 4: Pre-Planning Questions

Before generating tasks, use `AskUserQuestion` to clarify implementation approach:

**Question Categories:**
- **Priority**: Which requirements are highest priority?
- **Testing**: Unit tests only? Integration? E2E?
- **Implementation**: TDD strict? Standard? Incremental?

**Example Questions:**
```
1. "Testing approach?"
   Options: [TDD strict (Red-Green-Refactor), Unit + Integration, Minimal testing, Comprehensive (Unit + Integration + E2E)]

2. "Implementation priority?"
   Options: [Core functionality first, User-facing first, Infrastructure first]
```

---

## Phase 5: Generate tasks.md

Create `features/[feature-name]/tasks.md`:

```markdown
# [Feature Name] - Implementation Tasks

## Overview
Total tasks: N
Estimated complexity: [Low/Medium/High]
Testing approach: [from user input]

## Task List

### Phase 1: Foundation
- [ ] **Task 1**: [Description]
  - Tests: [What to test]
  - Acceptance: [Criteria]

- [ ] **Task 2**: [Description]
  - Tests: [What to test]
  - Acceptance: [Criteria]

### Phase 2: Core Implementation
- [ ] **Task 3**: [Description]
  - Tests: [What to test]
  - Acceptance: [Criteria]
  - Depends on: Task 1, Task 2

### Phase 3: Integration & Polish
- [ ] **Task N**: [Description]
  - Tests: [What to test]
  - Acceptance: [Criteria]

## Implementation Notes
- Key patterns to follow: ...
- Common pitfalls to avoid: ...
- Reference files: ...

## Definition of Done
- [ ] All tasks completed
- [ ] Tests passing
- [ ] Requirements satisfied
- [ ] Code reviewed
```

---

## Phase 6: Summary

After generating all files, present a summary:

```
## Specification Complete

Created specification for **[Feature Name]**:

| File | Description |
|------|-------------|
| `features/[name]/context.md` | Context + technical decisions |
| `features/[name]/requirements.md` | EARS requirements (N items) |
| `features/[name]/tasks.md` | Implementation tasks (N items) |

### Quick Stats
- Requirements: N functional, N non-functional
- Tasks: N total across N phases
- Testing: [approach]

### Next Steps
Run `/spec:execute [feature-name]` to begin implementation, or review the generated files first.
```

---

## Key Guidelines

1. **Be efficient**: Minimize back-and-forth, batch questions
2. **Use AskUserQuestion**: For clarification, not for approval gates
3. **Generate all files**: Don't stop between phases
4. **Keep it concise**: Avoid verbose documentation
5. **Be practical**: Focus on actionable items

## File Structure
```
features/
└── [feature-name]/
    ├── context.md      # Context + technical decisions
    ├── requirements.md # EARS requirements
    └── tasks.md        # Implementation tasks
```

Now, start by asking initial questions about: **$ARGUMENTS**
