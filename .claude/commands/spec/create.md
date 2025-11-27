---
description: Generate context, requirements, and tasks for a feature in a single unified flow.
allowed-tools: Read(*), Write(*), Edit(*), MultiEdit(*), Glob(*), Grep(*), Bash(*), TodoWrite, AskUserQuestion, Task
---

# Unified Feature Specification (Enhanced)

Generate complete feature specification with deep codebase exploration using Task agents.

## Your Task
Create a complete specification for: **$ARGUMENTS**

## Enhanced Flow Overview
1. **Triage** - Assess complexity, determine exploration depth
2. **Explore** - Spawn Explore agents to understand codebase (parallel)
3. **Initial Questions** - Gather context informed by exploration
4. **Plan** - Spawn Plan agents for approaches and strategies (parallel)
5. **Synthesize** - Create exploration.md with all findings
6. **Generate** - Create context.md, requirements.md, tasks.md
7. **Summary** - Present all generated files

---

## Phase 0: Triage

Quickly assess feature complexity to determine how many Explore agents to spawn.

**Assessment Steps:**
1. Parse the feature description for complexity keywords
2. Check if `features/` directory exists with established patterns: `Glob("features/*/context.md")`
3. Estimate project size: `Glob("**/*.{ts,js,py,go,rs,java}")` (count source files)

**Complexity Matrix:**

| Indicator | Low | Medium | High |
|-----------|-----|--------|------|
| Description keywords | Simple CRUD, basic | Auth, API, data | Integration, realtime, complex |
| Existing features | 0 | 1-3 | 4+ |
| Source files | < 20 | 20-100 | > 100 |

**Agent Count Decision:**
- **Low complexity**: 1 Explore agent (comprehensive)
- **Medium complexity**: 2 Explore agents (patterns + similar features)
- **High complexity**: 3 Explore agents (patterns, similar features, tech stack)

---

## Phase 1: Explore Agents

Use the `Task` tool with `subagent_type: "Explore"` to spawn codebase exploration agents. Run all applicable agents **in parallel**.

### Agent 1: Patterns & Conventions (Always spawn)

```
Task tool parameters:
- subagent_type: "Explore"
- description: "Explore codebase patterns"
- prompt: |
    Explore the codebase to understand existing patterns for implementing: [feature-description]

    Search for and document:
    1. Directory structure - Where does similar code live? (use Glob)
    2. Naming conventions - File names, function names, class names
    3. Code organization - How are modules/services/controllers structured?
    4. Error handling - How are errors caught, logged, and reported?
    5. Configuration - How is config managed? Environment variables?

    Use Glob and Grep to find concrete examples. Return findings with specific file paths.
```

### Agent 2: Similar Features (Medium/High complexity)

```
Task tool parameters:
- subagent_type: "Explore"
- description: "Find similar features"
- prompt: |
    Search for existing features similar to: [feature-description]

    Look for:
    1. Features with overlapping functionality (search keywords in code)
    2. How similar features are structured (files, folders, components)
    3. What patterns they follow
    4. Their test coverage and testing approach
    5. Any shared utilities or helpers they use

    Return specific file paths and brief code snippets as examples.
```

### Agent 3: Tech Stack & Dependencies (High complexity only)

```
Task tool parameters:
- subagent_type: "Explore"
- description: "Analyze tech stack"
- prompt: |
    Analyze the tech stack and dependencies relevant to: [feature-description]

    Document:
    1. Framework and version (check package.json, requirements.txt, go.mod, etc.)
    2. Relevant installed libraries that could be used
    3. Database/storage solutions in use
    4. Testing frameworks and tools
    5. Build/deployment configuration
    6. Any constraints these impose

    Return a summary of available tools and technical constraints.
```

---

## Phase 2: Initial Questions (Informed by Exploration)

After exploration completes, use `AskUserQuestion` with context-aware questions.

**Craft questions that reference exploration findings:**

Example informed questions:
```
1. "Your codebase uses [pattern X] for similar features (found in [file Y]). Should this feature follow the same pattern?"
   Options:
   - "Yes, follow existing pattern"
   - "No, try a different approach"
   - "Hybrid - adapt the pattern"

2. "Found similar feature [feature-name] that handles [X]. Should we follow its structure?"
   Options:
   - "Yes, use as reference"
   - "No, different approach needed"
   - "Partially - use [specific aspect]"

3. "The project uses [library Z] for [purpose]. Use it for this feature?"
   Options:
   - "Yes, use existing library"
   - "No, add a different solution"
   - "Evaluate during implementation"
```

**Standard questions (if no relevant exploration findings):**
- Goal: What is the main objective?
- Scope: MVP or full feature?
- Tech preferences: Any specific requirements?
- Constraints: Performance, security, integration needs?

---

## Phase 3: Plan Agents

Use the `Task` tool with `subagent_type: "Plan"` to spawn planning agents. Run all agents **in parallel**.

### Agent 1: Implementation Approaches

```
Task tool parameters:
- subagent_type: "Plan"
- description: "Evaluate approaches"
- prompt: |
    Given the exploration findings and user requirements, propose 2-3 implementation approaches for: [feature-description]

    Exploration context:
    [Insert summarized findings from Phase 1]

    User requirements:
    [Insert answers from Phase 2]

    For each approach provide:
    1. Name and brief description
    2. Pros and cons
    3. Complexity estimate (Low/Medium/High)
    4. How well it fits existing codebase patterns (1-10)
    5. Key risks or considerations

    Recommend the best approach with clear rationale.
```

### Agent 2: Testing Strategy

```
Task tool parameters:
- subagent_type: "Plan"
- description: "Design testing strategy"
- prompt: |
    Design a testing strategy for: [feature-description]

    Existing test patterns found:
    [Insert testing patterns from exploration]

    Cover:
    1. Unit test approach and coverage targets
    2. Integration test requirements
    3. E2E test scenarios (if applicable)
    4. Test data and fixture needs
    5. Mocking strategy
    6. CI/CD integration considerations

    Align with existing project testing conventions.
```

### Agent 3: Architecture & Integration

```
Task tool parameters:
- subagent_type: "Plan"
- description: "Design architecture"
- prompt: |
    Design the architecture and integration approach for: [feature-description]

    Existing architecture patterns:
    [Insert architecture findings from exploration]

    Cover:
    1. Component boundaries and responsibilities
    2. Integration points with existing code
    3. Data flow and state management
    4. API design (if applicable)
    5. Security considerations
    6. Performance implications

    Ensure compatibility with existing codebase structure.
```

---

## Phase 4: Synthesize Findings

Create `features/[feature-name]/exploration.md` combining all agent outputs:

```markdown
# [Feature Name] - Exploration

## Codebase Analysis

### Patterns & Conventions
[From Explore Agent 1]
- Directory structure: ...
- Naming conventions: ...
- Code organization: ...
- Error handling: ...

### Similar Features
[From Explore Agent 2, if spawned]
- [Feature 1]: `path/to/feature` - [relevance]
- [Feature 2]: `path/to/feature` - [relevance]

### Tech Stack
[From Explore Agent 3, if spawned]
- Framework: ...
- Key libraries: ...
- Database: ...
- Testing tools: ...

## Implementation Analysis

### Evaluated Approaches

#### Approach 1: [Name]
- Description: ...
- Pros: ...
- Cons: ...
- Pattern fit: X/10
- Complexity: [Low/Medium/High]

#### Approach 2: [Name]
- Description: ...
- Pros: ...
- Cons: ...
- Pattern fit: X/10
- Complexity: [Low/Medium/High]

### Recommended Approach
**[Name]**: [Brief description]

Rationale: [Why this approach was selected based on exploration + user requirements]

### Testing Strategy
[From Plan Agent 2]
- Unit tests: ...
- Integration tests: ...
- E2E tests: ...

### Architecture Design
[From Plan Agent 3]
- Components: ...
- Integration points: ...
- Data flow: ...

## Reference Files
Files to reference during implementation:
- `path/to/similar/feature` - [why relevant]
- `path/to/pattern/example` - [why relevant]
- `path/to/test/example` - [testing pattern]
```

---

## Phase 5: Generate Spec Files

Generate the three core spec files, incorporating exploration findings.

### Generate context.md

```markdown
# [Feature Name] - Context

## Overview
[Brief description informed by exploration]

## Exploration Reference
See `exploration.md` for detailed codebase analysis and approach evaluation.

## Chosen Approach
**[Approach Name]**: [Brief description]

Rationale: [Why selected, referencing exploration findings]

## Goals
[From user answers]

## Scope
### In Scope
[From user answers + exploration insights]

### Out of Scope
[Explicitly excluded items]

## Technical Decisions

### Stack
[Informed by tech stack exploration]

### Architecture
[From architecture planning agent]

### Key Design Decisions
1. **Decision**: [What] - **Rationale**: [Why, referencing exploration]

## Constraints & Considerations
[From exploration + user input]

## Dependencies
[From exploration tech stack analysis]
```

### Generate requirements.md

Use EARS format, informed by similar features found:

```markdown
# [Feature Name] - Requirements

## Reference
Implementation patterns: See `exploration.md` for similar feature examples.

## Functional Requirements

### Core Functionality
- REQ-001: [EARS requirement based on goals]
- REQ-002: ...

### User Interactions
- REQ-010: WHEN [user action] THEN the system SHALL [response]

### Data Management
- REQ-020: The system SHALL [data requirement]

## Non-Functional Requirements

### Performance
- NFR-001: [Based on existing patterns or user constraints]

### Security
- NFR-010: [Security requirement]

### Reliability
- NFR-020: WHILE [state] the system SHALL [behavior]

## Acceptance Criteria Summary
- [ ] [Criterion from requirements]
```

### Generate tasks.md

TDD tasks with specific file paths from exploration:

```markdown
# [Feature Name] - Implementation Tasks

## Reference Files
Based on exploration, use these as implementation references:
- `path/to/similar/feature` - Follow this pattern for [X]
- `path/to/test/example` - Follow this testing approach

## Overview
- Total tasks: N
- Complexity: [from exploration]
- Testing approach: [from planning agent]

## Task List

### Phase 1: Foundation

#### Task 1: [Setup/Foundation task]
**Pattern Reference**: `path/to/similar/setup`

- Description: [What to implement]
- Tests:
  - Unit: [specific tests]
  - Integration: [if needed]
- Acceptance: [criteria tied to requirements]
- TDD Steps:
  1. RED: Write failing test for [specific behavior]
  2. GREEN: Implement [minimal code]
  3. REFACTOR: [improvements]

### Phase 2: Core Implementation

#### Task 2: [Core feature task]
**Pattern Reference**: `path/to/similar/implementation`

- Description: [What to implement]
- Tests: [specific tests]
- Acceptance: [criteria]
- Depends on: Task 1

### Phase 3: Integration & Polish

#### Task N: [Final task]
- Description: [What to implement]
- Tests: [specific tests]
- Acceptance: [criteria]

## Implementation Notes
[Key insights from exploration]

## Definition of Done
- [ ] All tasks marked [IMPLEMENTED]
- [ ] Tests passing (coverage: X%)
- [ ] Requirements satisfied
- [ ] Code reviewed
```

---

## Phase 6: Summary

Present enhanced summary:

```markdown
## Specification Complete

Created specification for **[Feature Name]**:

| File | Description |
|------|-------------|
| `features/[name]/exploration.md` | Codebase analysis + approach evaluation |
| `features/[name]/context.md` | Context + technical decisions |
| `features/[name]/requirements.md` | EARS requirements (N items) |
| `features/[name]/tasks.md` | Implementation tasks (N items) |

### Exploration Summary
- **Complexity detected**: [Low/Medium/High]
- **Explore agents used**: N
- **Similar features found**: N
- **Patterns identified**: N

### Chosen Approach
**[Approach Name]**: [One-sentence summary]

### Key References
- `path/to/most/relevant/file` - [Why important]

### Next Steps
1. Review `exploration.md` for detailed analysis
2. Run `/spec:execute [feature-name]` to begin implementation
```

---

## Key Guidelines

1. **Parallel Execution**: Run independent agents in parallel (multiple Task calls in one message)
2. **Dynamic Agent Count**: Adjust based on triage results - don't over-explore simple features
3. **Informed Questions**: Questions should reference exploration findings when relevant
4. **Synthesis First**: Create exploration.md before other spec files
5. **Cross-Reference**: Spec files should reference exploration.md and specific file paths
6. **Be Efficient**: Don't stop between phases, minimize back-and-forth

## File Structure

```
features/
└── [feature-name]/
    ├── exploration.md  # Codebase analysis + approach evaluation
    ├── context.md      # Context + technical decisions
    ├── requirements.md # EARS requirements
    └── tasks.md        # Implementation tasks
```

---

Now, start with Phase 0 (Triage) for: **$ARGUMENTS**
