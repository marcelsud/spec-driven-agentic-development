---
description: Initialize feature specification using structured EARS requirements
allowed-tools: Read(*), Write(*), Edit(*), MultiEdit(*), TodoWrite
---

# Feature Specification Initialization

You are initializing a new feature specification following the Spec-Driven Agentic Development methodology.

## Your Task
Initialize complete requirements specification for: **$ARGUMENTS**

## Process
1. **Read the methodology**: Reference `.claude/CLAUDE.md` for complete guidance
2. **Create feature directory**: Set up organized file structure
3. **Generate EARS requirements**: Create comprehensive requirements.md
4. **Seek approval**: Request explicit user approval before proceeding

## EARS Requirements Format
Use these structured templates:
- **Ubiquitous**: "The system SHALL [requirement]"
- **Event-Driven**: "WHEN [trigger] THEN the system SHALL [response]"
- **State-Driven**: "WHILE [state] the system SHALL [requirement]"
- **Conditional**: "IF [condition] THEN the system SHALL [requirement]"
- **Optional**: "WHERE [feature included] the system SHALL [requirement]"

## File Structure to Create
```
features/[feature-name]/
├── requirements.md    # EARS-formatted requirements
├── design.md         # (placeholder for next phase)
└── tasks.md          # (placeholder for final phase)
```

## Requirements Quality Gates
Ensure requirements are:
- [ ] Written in proper EARS syntax
- [ ] Testable and specific (no vague terms)
- [ ] Cover all user scenarios and edge cases
- [ ] Include error handling and validation
- [ ] One requirement per statement

## Key Guidelines
- Create comprehensive requirements covering all aspects of the feature
- Use specific, measurable language ("within 2 seconds" not "quickly")
- Include both functional and non-functional requirements
- Consider security, performance, and usability aspects
- Structure requirements logically (authentication → core functionality → error handling)

## Approval Gate
After creating requirements.md, ask:
"Requirements specification complete for [$ARGUMENTS]. The EARS-formatted requirements cover [brief summary of key areas]. Ready to proceed to design phase with `/spec-design`, or would you like to review and modify the requirements first?"

## Next Steps
- User reviews requirements and approves/requests changes
- Once approved, user can run `/spec-design` to proceed to technical design phase
- Implementation follows structured phases with approval gates

Now initialize the feature specification for: **$ARGUMENTS**