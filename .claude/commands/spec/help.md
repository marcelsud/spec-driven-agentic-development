---
description: Display help information for spec:driven development commands
allowed-tools: Read(*)
---

# Spec-Driven Development Help

Quick reference for the spec:driven development methodology.

## Available Commands

| Command | Description |
|---------|-------------|
| `/spec:create [feature]` | Generate complete specification with codebase exploration |
| `/spec:execute [feature]` | Execute implementation from tasks.md |
| `/spec:status` | Show implementation status of all features |
| `/spec:list` | List all available features |
| `/spec:review [feature]` | Review spec for EARS compliance and quality |
| `/spec:diagram [feature]` | Generate Mermaid diagrams from spec |
| `/spec:next` | Suggest next feature to work on |
| `/spec:help` | Display this help |

## Workflow

```
/spec:create [feature]  →  exploration.md + context.md + requirements.md + tasks.md
/spec:review [feature]  →  Quality review + optional fixes
/spec:diagram [feature] →  Mermaid diagrams in diagrams.md
/spec:next              →  Recommendation for next feature
/spec:execute [feature] →  Implementation following TDD
```

## `/spec:create` Flow (Enhanced)

1. **Triage** - Assess complexity, determine exploration depth
2. **Explore** - Spawn agents to analyze codebase patterns (parallel)
3. **Questions** - Context-aware questions informed by exploration
4. **Plan** - Spawn agents for approaches and strategies (parallel)
5. **Synthesize** - Create exploration.md with findings
6. **Generate** - Create context.md, requirements.md, tasks.md

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
├── exploration.md  # Codebase analysis + approach evaluation
├── context.md      # Context + technical decisions
├── requirements.md # EARS requirements
├── tasks.md        # TDD implementation tasks
├── diagrams.md     # Generated Mermaid diagrams (optional)
└── review.md       # Spec quality review (optional)
```

## Example Usage

```bash
# Create new feature specification (with codebase exploration)
/spec:create user-authentication

# Review spec quality and EARS compliance
/spec:review user-authentication

# Generate architecture diagrams
/spec:diagram user-authentication

# Get recommendation for next feature
/spec:next

# View all features
/spec:list

# Check implementation status
/spec:status

# Implement feature
/spec:execute user-authentication
```

## More Info

See `.claude/CLAUDE.md` for complete methodology.
