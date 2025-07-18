# Spec-Driven Agentic Development

A modern methodology for building software features through structured specifications, optimized for AI-powered development tools and focused slash commands.

## 🎯 What This Is

This framework transforms complex feature development into manageable, iterative phases with explicit approval gates and quality controls. It provides a structured, iterative approach to software development that turns complex feature development into a series of well-defined phases. Instead of feeding large documents to AI agents, it uses focused slash commands for reliable, efficient development workflows.

This methodology ensures high-quality, well-tested software development through structured phases, clear requirements, and iterative feedback loops. It provides the framework for reliable agentic development while maintaining human oversight and control.

## Key Principles

- **Explicit Approval Gates**: Always request approval before proceeding to the next phase.
- **EARS Requirements**: Use structured requirement syntax for clarity and testability.
- **Test-Driven Development**: Implement using the Red-Green-Refactor cycle.
- **Iterative Refinement**: Allow multiple iterations within each phase.
- **User Control**: Maintain user oversight throughout the process.
- **Focused Commands**: Each command has a specific, well-defined purpose for better context management.

## 🚀 The Workflow

The core of the methodology is a five-phase workflow, driven by simple commands.

### Workflow Overview

```
1. /spec:plan [project-description] → List of Features → [Approval Gate]
2. /spec:requirements [feature-name] → requirements.md → [Approval Gate]
3. /spec:design [feature-name]       → design.md       → [Approval Gate]
4. /spec:tasks [feature-name]        → tasks.md        → [Approval Gate]
5. /spec:execute [feature-name]      → Working Code    → [Testing & Deploy]
```

---

### Phase 1️⃣: Planning (`/spec:plan`)

This phase is about breaking down a high-level goal into a structured plan of individual, manageable features.

- **Command**: `/spec:plan [project-description]`
- **Process**: The agent interactively works with you to break down a high-level goal into a list of discrete, sequential features.
- **Output**: A set of feature directories (e.g., `features/01-project-setup/`) each containing a basic `requirements.md`.
- **Approval Gate**: "Project plan complete. Shall we begin detailing the requirements for the first feature?"

### Phase 2️⃣: Requirements (`/spec:requirements`)

This phase is about defining **WHAT** needs to be built for a specific feature.

- **Command**: `/spec:requirements [feature-name]`
- **Process**: The agent interactively works with you to elicit detailed requirements for a single feature. It asks open-ended questions about goals, users, and problems to solve, then drafts requirements using the EARS format for your feedback.
- **Output**: A detailed `features/[feature-name]/requirements.md` file.
- **Approval Gate**: "Requirements for [feature-name] are now detailed. Ready to proceed to the design phase with `/spec:design`?"

### Phase 2️⃣: Design (`/spec:design`)

This phase is about defining **HOW** it will be built.

- **Command**: `/spec:design`
- **Process**: Based on the approved requirements, the agent generates a technical design. It will present technology stack options (e.g., Full-Stack JS, Python backend, etc.) and ask clarifying questions to create a comprehensive design.
- **Output**: A `design.md` file detailing the system architecture, data models, API design, security considerations, and more.
- **Approval Gate**: "Technical design complete. Ready to proceed to task breakdown with `/spec:tasks`?"

### Phase 3️⃣: Tasks (`/spec:tasks`)

This phase breaks down the design into an implementable plan.

- **Command**: `/spec:tasks`
- **Process**: The agent converts the technical design into a detailed list of implementation tasks, structured for Test-Driven Development (TDD). Each task includes acceptance criteria, TDD steps (Red-Green-Refactor), test scenarios, and dependencies.
- **Output**: A `tasks.md` file with a structured implementation plan.
- **Approval Gate**: "Implementation task breakdown complete. Ready to begin implementation?"

### Phase 4️⃣: Implementation (`/spec:execute`)

This is the coding phase, following the structured tasks.

- **Command**: `/spec:execute [feature-name]`
- **Process**: The agent executes the implementation plan from `tasks.md`. It follows the TDD cycle for each task: write a failing test, write code to pass the test, and refactor. After each task, it seeks confirmation before proceeding.
- **Output**: Working, tested code that meets the feature requirements.
- **Implementation Approaches**: You can choose the implementation strategy:
    - **🔴🟢🔄 TDD**: Strict Red-Green-Refactor methodology.
    - **⚡ Standard**: Traditional implementation following tasks.
    - **🤝 Collaborative**: Mixed human-AI development.
    - **👤 Self**: You use the spec as a guide for your own implementation.

---

### ⚡ Advanced Analysis (`/spec:advanced`)

At any stage, you can enhance the specification with enterprise-grade analysis.

- **Command**: `/spec:advanced`
- **Process**: The agent applies comprehensive frameworks for deeper insights into the existing specifications.
- **Output**: Enhanced specifications including:
    - **Security Threat Modeling (STRIDE)**: Identifies spoofing, tampering, repudiation, etc.
    - **Risk Assessment**: Analyzes probability and impact of risks.
    - **Scalability Analysis**: Pinpoints performance bottlenecks and scaling needs.
    - **Edge Case Analysis**: Covers boundary conditions, error scenarios, and system failures.

## 🔧 Core Concepts

### EARS Requirements Format

A structured requirement syntax for clarity and testability.

| Template | Format |
|---|---|
| **Ubiquitous** | "The system SHALL [requirement]" |
| **Event-Driven** | "WHEN [trigger] THEN the system SHALL [response]" |
| **State-Driven** | "WHILE [state] the system SHALL [requirement]" |
| **Conditional** | "IF [condition] THEN the system SHALL [requirement]" |
| **Optional** | "WHERE [feature included] the system SHALL [requirement]" |

**Example**: "WHEN a user enters incorrect credentials three times THEN the system SHALL lock the account for 15 minutes."

### Test-Driven Development (TDD)

Every implementation follows the Red-Green-Refactor cycle:

1.  **🔴 Red**: Write a failing test for the next piece of functionality.
2.  **🟢 Green**: Write the minimal amount of code required to make the test pass.
3.  **🔄 Refactor**: Improve the code's structure and quality without changing its behavior, keeping tests green.

### Quality Gates

- ✅ **Requirements**: Must be testable, specific, and use EARS syntax.
- ✅ **Design**: Must address all requirements, be technically sound, and consider security and scalability.
- ✅ **Tasks**: Must be granular, actionable, include test scenarios, and follow TDD.

## 📁 Project Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md                     # Complete methodology reference
│   └── commands/
|       └── spec/
│           ├── init.md               # /spec:init - Initialize requirements
│           ├── design.md             # /spec:design - Generate design
│           ├── tasks.md              # /spec:tasks - Create TDD tasks
│           ├── execute.md            # /spec:execute - Execute implementation
│           ├── advanced.md           # /spec:advanced - Enterprise analysis
│           └── help.md               # /spec:help - Command reference
│   └── templates/                    # Reference templates for the agent
│       ├── requirements.md           # EARS requirements template
│       ├── design.md                 # Technical design template
│       └── tasks.md                  # TDD task breakdown template
└── features/                         # Your generated specifications
    └── [feature-name]/
        ├── requirements.md           # EARS-formatted requirements
        ├── design.md                 # Technical design document
        ├── tasks.md                  # Implementation task breakdown
        └── task_{nr}_completed.md    # Task completion summary
```

## 🚀 Commands Quick Reference

| Phase | Command | Purpose |
|-------|---------|---------|
| 1️⃣ | `/spec:plan [project-description]` | Interactively break down a project into features. |
| 2️⃣ | `/spec:requirements [feature-name]` | Interactively create EARS requirements for a feature. |
| 2️⃣ | `/spec:design` | Generate technical design from requirements. |
| 3️⃣ | `/spec:tasks` | Create a TDD implementation plan from the design. |
| 4️⃣ | `/spec:execute [feature-name]`| Execute the implementation plan from `tasks.md`. |
| ⚡ | `/spec:advanced` | Apply enterprise-grade security, risk, and scalability analysis. |
| ❓ | `/spec:help` | Display help information for all spec commands. |


## 💡 Why This Approach Works

### Problems with Traditional AI Development
- ❌ **Context Overload**: Large documents overwhelm AI context windows.
- ❌ **Reliability Issues**: Complex workflows fail unpredictably.
- ❌ **Poor Iteration**: Hard to modify individual phases.
- ❌ **Vague Requirements**: Natural language lacks precision.

### Solutions with Spec-Driven Development
- ✅ **Focused Commands**: Each command has a single, clear purpose.
- ✅ **Reliable Results**: Smaller operations with higher success rates.
- ✅ **Easy Iteration**: Modify requirements, design, or tasks independently.
- ✅ **EARS Precision**: Structured requirements eliminate ambiguity.
- ✅ **TDD Quality**: Built-in testing ensures robust implementation.
- ✅ **Approval Gates**: Human oversight at every decision point.

## 🛠️ Installation & Usage

This methodology is designed to be used with AI coding assistants like Claude Code.

### Local Installation (Project-Specific)

Install in a specific project only:

```bash
# Copy methodology and commands to your project
# (Assuming you have cloned this repository)
cp -r .claude /path/to/your/project/
```

### Usage with an AI Tool

1.  Load `.claude/CLAUDE.md` as the primary context for the AI.
2.  Use the `/spec:*` commands to guide the AI through the structured phases.
3.  Review and approve the output at each phase before proceeding.

## 🤝 Contributing

This methodology evolved from practical experience with AI-assisted development. Improvements and refinements are welcome through issues and pull requests.

---

**Ready to build better software with structured specifications?**

Start with: `/spec:plan your-awesome-project` 🚀
