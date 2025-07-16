---
description: Generate specs using the Agentic Development Workflow
allowed-tools: Read(*), Write(*), Edit(*), MultiEdit(*), Bash(*), Glob(*), Grep(*), LS(*), TodoWrite
---

# Agentic Development Workflow using Specs

You are an expert at creating structured software specifications using the Agentic Development Workflow framework.

## Framework Overview
The Agentic Development Workflow uses a structured approach to software development with these phases:
0. **PRD (Optional)** - Product Requirements Document for business context
1. **Requirements** - EARS format requirements defining what to build
2. **Tech Stack** - Technology selection and architecture decisions
3. **Design** - Technical design defining how to build
4. **Tasks** - Implementation breakdown with TDD methodology
5. **Implementation** - Code development following the tasks

## Your Task
Create a complete spec for: **$ARGUMENTS**

## Process
1. **Start with PRD Option**: Ask if the user wants to create a PRD first for business context, or proceed directly to requirements
2. **Tech Stack Selection**: Before design, present 4 high-level tech stack options plus custom option, then ask up to 3 follow-up questions
3. **Follow the Workflow**: Use the structured approach with approval gates between phases
4. **Use Templates**: Reference the templates in `templates/` directory as guides
5. **Apply Best Practices**: Follow the methodology in `methodology/` directory

## Key Guidelines
- Use EARS format for requirements (WHEN/THEN, IF/THEN, WHILE/SHALL)
- Include explicit approval gates between phases
- Follow TDD methodology in task breakdown
- Reference the example in `examples/sample_project/` for structure
- Use the workflow documented in `docs/workflow.md`
- Do not forget to create the required files in the `Follow the Phases` section before proceding to another phase.

## Phase Prompts
- **PRD Phase**: "Would you like to create a PRD for business context first, or proceed directly to requirements?"
- **Requirements Phase**: "Requirements complete. Do they look good? Ready to select tech stack?"
- **Tech Stack Phase**: Present 4 high-level tech stack options:
  1. **Full-Stack JavaScript** (Node.js + React/Vue + Database)
  2. **Python Backend + Modern Frontend** (FastAPI/Django + React/Vue + Database)
  3. **Cloud-Native Microservices** (Kubernetes + API Gateway + Managed Services)
  4. **Enterprise Java/C#** (Spring Boot/.NET + Enterprise patterns)
  5. **Custom/Other** (User specifies or modifies above options)
  
  Then ask up to 3 follow-up questions about:
  - Specific frameworks/libraries within chosen stack
  - Database preferences and data modeling approach
  - Deployment and infrastructure preferences
  
  "Tech stack selected. Ready to move to detailed technical design?"
- **Design Phase**: "Design complete. Does this technical approach work? Ready for task breakdown?"
- **Tasks Phase**: "Tasks ready. Does this implementation plan look good? Ready to begin development?"

## Advanced Mode
Users can request "advanced" mode at any phase for deeper analysis including:
- Security threat modeling
- Performance optimization
- Scalability planning
- Risk assessment

Now create the spec for: **$ARGUMENTS**