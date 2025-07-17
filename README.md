# Spec-Driven Agentic Development

A modern methodology for building software features through structured specifications, optimized for Claude Code's native capabilities and focused slash commands.

## 🎯 What This Is

This framework transforms complex feature development into manageable, iterative phases with explicit approval gates and quality controls. Instead of feeding large documents to AI agents, it uses focused slash commands for reliable, efficient development workflows.

## ⚡ Quick Start

### For Claude Code (Recommended)

1. **Install the methodology** in your project:
   ```bash
   # Copy methodology and commands to your project
   cp -r .claude templates /path/to/your/project/
   ```

2. **Run the focused workflow**:
   ```bash
   # Phase 1: Create EARS requirements
   /spec:init user-authentication-system
   
   # Phase 2: Generate technical design  
   /spec:design
   
   # Phase 3: Create TDD implementation tasks
   /spec:tasks
   
   # Phase 4: Implement with chosen approach
   # (TDD, standard, collaborative, or self-implementation)
   ```

3. **Follow approval gates**:
   - Review and approve requirements before design
   - Review and approve design before tasks
   - Review and approve tasks before implementation

### For Other AI Tools

Load `.claude/CLAUDE.md` as context and guide the AI through the structured phases manually.

## 🔧 Core Methodology

### EARS Requirements Format

Structured requirement syntax for clarity and testability:

```
Ubiquitous:    "The system SHALL [requirement]"
Event-Driven:  "WHEN [trigger] THEN the system SHALL [response]"
State-Driven:  "WHILE [state] the system SHALL [requirement]"  
Conditional:   "IF [condition] THEN the system SHALL [requirement]"
Optional:      "WHERE [feature] the system SHALL [requirement]"
```

**Example**: "WHEN a user enters incorrect credentials three times THEN the system SHALL lock the account for 15 minutes"

### Test-Driven Development (TDD)

Every implementation follows Red-Green-Refactor:

1. **🔴 Red**: Write failing test for next functionality
2. **🟢 Green**: Write minimal code to make test pass
3. **🔄 Refactor**: Improve code while keeping tests green

### Quality Gates

- ✅ Requirements must be testable and specific (no vague terms)
- ✅ Design must address all requirements with technical solutions
- ✅ Tasks must include comprehensive TDD steps and test scenarios
- ✅ Implementation must follow structured task breakdown

## 📁 Project Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md                # Complete methodology reference
│   └── commands/
│       ├── spec-init.md        # /spec:init - Initialize requirements  
│       ├── spec-design.md      # /spec:design - Generate design
│       ├── spec-tasks.md       # /spec:tasks - Create TDD tasks
│       ├── spec-advanced.md    # /spec:advanced - Enterprise analysis
│       └── spec-help.md        # /spec:help - Command reference
├── templates/                   # Reference templates for the agent
│   ├── requirements.md         # EARS requirements template
│   ├── design.md              # Technical design template
│   └── tasks.md               # TDD task breakdown template
└── features/                   # Your generated specifications
    └── [feature-name]/
        ├── requirements.md     # EARS-formatted requirements
        ├── design.md          # Technical design document
        └── tasks.md           # Implementation task breakdown
```

## 🚀 Workflow Commands

| Phase | Command | Input | Output | Purpose |
|-------|---------|-------|--------|---------|
| 1️⃣ | `/spec:init feature-name` | Feature description | `requirements.md` | EARS requirements |
| 2️⃣ | `/spec:design` | Existing requirements | `design.md` | Technical architecture |
| 3️⃣ | `/spec:tasks` | Existing design | `tasks.md` | TDD implementation plan |
| 4️⃣ | Implementation | Task breakdown | Working code | Choose your approach |
| ⚡ | `/spec:advanced` | Existing specifications | Enhanced specs | Security & risk analysis |
| ❓ | `/spec:help` | None | Command reference | Quick help guide |

### Phase Details

#### 1️⃣ Requirements (`/spec:init`)
- Creates comprehensive EARS-formatted requirements
- Covers functional, non-functional, and edge case scenarios
- Includes specific validation rules and error handling
- **Approval Gate**: "Requirements complete. Ready for design phase?"

#### 2️⃣ Design (`/spec:design`)  
- Presents 4 tech stack options + custom choice
- Creates detailed technical architecture
- Addresses security, performance, and scalability
- Maps all requirements to technical solutions
- **Approval Gate**: "Design complete. Ready for task breakdown?"

#### 3️⃣ Tasks (`/spec:tasks`)
- Breaks design into 8-15 implementable tasks
- Each task includes Red-Green-Refactor TDD steps
- Comprehensive test scenarios and dependencies
- Clear acceptance criteria and quality gates
- **Approval Gate**: "Tasks ready. Ready to begin implementation?"

#### 4️⃣ Implementation
Choose your approach:
- **🔴🟢🔄 TDD**: Strict Red-Green-Refactor methodology
- **⚡ Standard**: Traditional implementation following tasks
- **🤝 Collaborative**: Mixed human-AI development
- **👤 Self**: Use spec as implementation guide

#### ⚡ Advanced Analysis (`/spec:advanced`)
- Applies enterprise-grade analysis to existing specifications
- Includes STRIDE threat modeling for security vulnerabilities
- Provides comprehensive risk assessment with mitigation strategies
- Identifies performance bottlenecks and scalability requirements
- Covers edge cases and failure scenarios
- **Usage**: Can be run at any phase for enhanced analysis

#### ❓ Help (`/spec:help`)
- Displays comprehensive command reference and usage guide
- Shows EARS format examples and TDD methodology
- Provides file structure and workflow overview
- **Usage**: Run anytime you need quick reference information

## 🎯 Why This Approach Works

### Problems with Traditional AI Development
- ❌ **Context Overload**: Large documents overwhelm AI context windows
- ❌ **Reliability Issues**: Complex workflows fail unpredictably  
- ❌ **Poor Iteration**: Hard to modify individual phases
- ❌ **Vague Requirements**: Natural language lacks precision

### Solutions with Spec-Driven Development
- ✅ **Focused Commands**: Each command has single, clear purpose
- ✅ **Reliable Results**: Smaller operations with higher success rates
- ✅ **Easy Iteration**: Modify requirements/design/tasks independently
- ✅ **EARS Precision**: Structured requirements eliminate ambiguity
- ✅ **TDD Quality**: Built-in testing ensures robust implementation
- ✅ **Approval Gates**: Human oversight at every decision point

## 🛠️ Advanced Features

### Tech Stack Options
The methodology includes 4 predefined tech stacks plus custom options:

1. **Full-Stack JavaScript** (Node.js + React/Vue + Database)
2. **Python + Modern Frontend** (FastAPI/Django + React/Vue)  
3. **Cloud-Native Microservices** (Kubernetes + API Gateway)
4. **Enterprise Java/C#** (Spring Boot/.NET + Enterprise patterns)
5. **Custom/Other** (User-defined stack)

### Quality Assurance
- **Validation**: Every requirement must be testable
- **Traceability**: Design elements map to specific requirements
- **Test Coverage**: Comprehensive test scenarios for all functionality
- **Performance**: Specific timing and scalability requirements
- **Security**: Built-in security considerations and threat modeling

### Extensibility
- **Custom Templates**: Modify `.claude/templates/` for your standards
- **Organization Standards**: Integrate with existing development practices
- **Tool Integration**: Works with any development environment
- **Language Agnostic**: Methodology applies to any programming language

## 📚 Additional Resources

- **Complete Methodology**: See `.claude/CLAUDE.md` for detailed guidance
- **Templates**: Use `.claude/templates/` as starting points
- **Example Project**: Study `features/task-management-api/` for reference
- **Command Reference**: Each `.claude/commands/*.md` contains usage instructions

## 🤝 Contributing

This methodology evolved from practical experience with AI-assisted development. Improvements and refinements are welcome through issues and pull requests.

---

**Ready to build better software with structured specifications?**

Start with: `/spec:init your-first-feature` 🚀