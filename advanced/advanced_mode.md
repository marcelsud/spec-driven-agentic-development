# Advanced Mode: Optional Spec Workflow Extensions

This document provides optional "Advanced Mode" capabilities that can be layered on top of the standard workflow described in workflow.md.

### Activating Advanced Mode
Users can access advanced mode at any approval gate by:
- Typing "advanced" in response to the agent's standard prompt.
- Requesting specific advanced features by name.

---

## Phase 0: Product Requirements Document (PRD) Creation (Advanced)

### Agent Prompt
"Would you like to create a comprehensive Product Requirements Document (PRD) before proceeding with EARS requirements? A PRD provides business context, market analysis, and strategic foundation. Type 'PRD' to generate one, or 'requirements' to proceed directly to EARS requirements."

### Capabilities
- **Business Context Analysis**: Market opportunity, competitive landscape, and business case development.
- **User Research Integration**: Persona development, user journey mapping, and experience design.
- **Strategic Planning**: Feature prioritization, phased implementation strategy, and success metrics.
- **Stakeholder Alignment**: Executive summary, resource requirements, and ROI projections.
- **Risk Assessment**: Technical, business, and market risk identification and mitigation.

### User Responses
- "PRD" → Generate comprehensive Product Requirements Document
- "requirements" → Skip PRD and proceed directly to EARS requirements
- "advanced PRD" → Generate PRD with enhanced business analysis and strategic planning

### PRD to EARS Transition
Once PRD is approved, the agent will:
1. Extract user stories from personas and user journey
2. Convert feature specifications to EARS format
3. Use success metrics to define acceptance criteria
4. Reference technical considerations in requirements
5. Ensure all PRD elements are reflected in structured requirements

---

## Phase 1: Requirements Creation (Advanced)

### Agent Prompt
"Requirements document created with [X] requirements covering [key areas]. Would you like to review the EARS format compliance, add edge cases, or proceed to design? Type 'advanced' for detailed review options."

### Capabilities
- **EARS Format Validation**: Detailed compliance checking for requirement syntax.
- **Requirement Traceability Matrix**: Cross-reference requirements with user stories and acceptance criteria.
- **Edge Case Analysis**: Systematic identification of boundary conditions and error scenarios.
- **Stakeholder Impact Analysis**: Assessment of how requirements affect different user roles.
- **Compliance Mapping**: Alignment with regulatory or industry standards.
- **PRD Alignment Check**: Ensure requirements align with PRD objectives (if PRD was created).

---

## Phase 2: Design Creation (Advanced)

### Agent Prompt
"Design document completed with [technology stack] addressing all [X] requirements. Would you like to review architecture trade-offs, security analysis, performance considerations, or proceed to tasks? Type 'advanced' for detailed design review."

### Capabilities
- **Architecture Alternatives Analysis**: Comparison of different technical approaches with trade-offs.
- **Security Threat Modeling**: Systematic security risk assessment and mitigation strategies.
- **Performance Bottleneck Identification**: Analysis of potential performance issues and optimization opportunities.
- **Scalability Planning**: Assessment of system growth capabilities and scaling strategies.
- **Technology Risk Assessment**: Evaluation of technology choices and their long-term implications.

---

## Phase 3: Tasks Creation (Advanced)

### Agent Prompt
"Implementation plan created with [X] tasks across [Y] phases. Would you like to review task dependencies, risk analysis, or proceed to implementation? Type 'advanced' for detailed task review."

### Capabilities
- **Critical Path Analysis**: Identification of task dependencies and project timeline bottlenecks.
- **Resource Allocation Planning**: Optimization of task assignment and parallel execution opportunities.
- **Risk Assessment**: Identification of implementation risks and mitigation strategies.
- **Quality Gate Definition**: Specification of completion criteria and acceptance testing.

### User Responses
- "advanced" → Show detailed task analysis options
- "Show critical path" → Display task dependency analysis
- "Risk assessment" → Identify implementation risks
- "Proceed" → Move to implementation approach selection

---

## Phase 4: Implementation (Advanced)

### Agent Prompt
"Implementation ready with TDD tasks. Would you like to configure test strategy, CI/CD pipeline, code quality gates, or proceed with standard TDD? Type 'advanced' for implementation configuration options."

### Capabilities
- **Custom Test Strategies**: Configuration of specialized testing approaches (integration, performance, security).
- **CI/CD Pipeline Setup**: Automated build, test, and deployment configuration.
- **Code Quality Gates**: Definition of quality metrics and automated enforcement.
- **Performance Benchmarking**: Establishment of performance baselines and monitoring.
- **Security Testing Integration**: Automated security scanning and vulnerability assessment.
- **Test Coverage Analysis**, **Mutation Testing**.
- **Continuous Integration Feedback** and **Deployment Pipeline Integration**.

### User Responses
- "advanced" → Show implementation configuration options
- "Configure testing" → Set up custom test strategies
- "Setup CI/CD" → Configure deployment pipeline
- "Quality gates" → Define code quality requirements
- "Standard TDD" → Begin standard TDD implementation

---

## General Benefits of Advanced Mode
- **Deeper Analysis**: More thorough examination of each phase.
- **Risk Mitigation**: Proactive identification and planning for potential issues.
- **Quality Assurance**: Higher standards for deliverables and implementation.
- **Professional Standards**: Alignment with enterprise development practices.
- **Learning Opportunities**: Educational insights into best practices and methodologies.