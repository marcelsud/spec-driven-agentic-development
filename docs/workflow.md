# Spec Workflow Guidelines

## Overview
Specs are a structured way of building and documenting a feature you want to build. A spec is a formalization of the design and implementation process, iterating with the agent on requirements, design, and implementation tasks, then allowing the agent to work through the implementation.

Specs allow incremental development of complex features, with control and feedback.

## File References
Spec files allow for the inclusion of references to additional files via "#[[file:<relative_file_name>]]". This means that documents like an openapi spec or graphql spec can be used to influence implementation in a low-friction way.

## Workflow Process
1. (Optional) Start with PRD - define business context and strategic foundation
2. Create requirements.md - define what needs to be built (using EARS format)
3. Create design.md - define how it will be built
4. Break down into tasks.md - define the implementation steps
5. Iterate and refine each document as needed
6. Use the spec to guide incremental development with control and feedback

## Interactive Workflow Flow

### Phase 0: Product Requirements Document (PRD) Creation (Optional Advanced)
1. **Agent offers PRD creation**: "Would you like to create a comprehensive Product Requirements Document (PRD) before proceeding with EARS requirements? A PRD provides business context, market analysis, and strategic foundation."
2. **User chooses approach**:
   - "PRD" → Agent creates comprehensive PRD with business analysis
   - "requirements" → Skip directly to EARS requirements
   - "advanced PRD" → Agent creates enhanced PRD with deeper analysis
3. **If PRD is created**:
   - Agent generates PRD with business context, user personas, market analysis
   - Agent asks for approval: "The PRD is complete with business context and strategic foundation. Ready to proceed to EARS requirements?"
   - User reviews and approves or requests changes

### Phase 1: Requirements Creation
1. **Agent creates requirements.md** based on user's initial feature description (or approved PRD)
2. **Agent asks for user approval**: "Do the requirements look good? If so, we can move on to the design."
3. **User reviews and responds**:
   - If approved: Move to Phase 2
   - If changes needed: Agent iterates on requirements.md based on feedback

### Phase 2: Design Creation
1. **Agent creates design.md** addressing all requirements from requirements.md
2. **Agent asks for user approval**: "The design document is complete. Does this technical approach look good? Ready to move on to creating the implementation tasks?"
3. **User reviews and responds**:
   - If approved: Move to Phase 3
   - If changes needed: Agent iterates on design.md based on feedback

### Phase 3: Tasks Creation
1. **Agent creates tasks.md** breaking down the design into implementable steps
2. **Agent asks for user approval**: "The implementation tasks are ready. Do these tasks look comprehensive and properly ordered? Ready to begin implementation?"
3. **User reviews and responds**:
   - If approved: Move to implementation phase
   - If changes needed: Agent adjusts task breakdown, or ordering

### Phase 4: Implementation (Optional)
1. **Agent asks about implementation approach**: "The tasks are ready for implementation. Would you like to proceed with the implementation?"

2. **Implementation Approach Options**:
   - **Test-Driven Development (TDD)**: See `tdd.md` for the recommended approach.
   - Agent can implement tasks autonomously using a different methodology.
   - User can implement tasks themselves using the spec as a guide.
   - Hybrid approach with agent implementing some tasks and user others.

3. **Iterative feedback during implementation**:
   - User can request changes to remaining tasks based on implementation learnings
   - Agent can suggest spec updates based on implementation challenges
   - Test results guide implementation decisions and reveal design issues early

### Key Interaction Principles:
- **Explicit Approval Gates**: Agent always asks for explicit approval before moving to the next phase.
- **Iterative Refinement**: Each document can be refined multiple times based on user feedback.
- **User Control**: User maintains control over the direction and can request changes at any stage.
- **Contextual Questions**: Agent may ask clarifying questions during document creation to ensure accuracy.
- **Flexible Implementation**: Implementation phase can be handled by agent, user, or collaboratively.
- **TDD Recommendation**: The agent recommends the TDD approach. See `../methodology/tdd.md` for details.
- **Advanced Mode Access**: Users can request advanced analysis and configuration options at any phase by consulting `../advanced/advanced_mode.md`.

### Sample Interaction Patterns:

#### Requirements Approval:
- Agent: "Do the requirements look good? If so, we can move on to the design."
- User responses:
  - "Yes, looks good" → Proceed to design
  - "Add requirement for X" → Iterate on requirements
  - "Change requirement 3 to include Y" → Update specific requirement

#### Design Approval:
- Agent: "The design document is complete. Does this technical approach look good?"
- User responses:
  - "Approved, create tasks" → Proceed to tasks
  - "Use PostgreSQL instead of SQLite" → Update design
  - "Add caching layer" → Enhance design

#### Tasks Approval:
- Agent: "The implementation tasks are ready. Do these look comprehensive and properly ordered?"
- User responses:
  - "Ready to implement" → Proceed to implementation approach selection
  - "Break down task 5 into smaller pieces" → Refine tasks
  - "Add testing tasks" → Enhance task list

#### Implementation Approach Selection:
- Agent: "The tasks are ready for implementation. The recommended approach is Test-Driven Development (TDD). See `../methodology/tdd.md` for details on this process. Would you like to proceed with TDD implementation?"
- User responses:
  - "Yes, use TDD" → Begin TDD implementation cycle (see `../methodology/tdd.md`)
  - "No, implement without TDD" → Begin standard implementation
  - "I'll implement myself" → User takes over implementation
  - "Let's do it together" → Collaborative implementation approach

---
## Referenced Documents

- ../advanced/advanced_mode.md
- ../methodology/tdd.md
- ../methodology/ears.md
- ../methodology/best_practices.md
- structure.md
- ../templates/prd_template.md