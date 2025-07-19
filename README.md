# Spec-Driven Agentic Development

A structured methodology for building software features through specifications, optimized for AI-powered development tools.

```
 ███████╗ ██████╗  ███████╗  ██████╗        ██████╗  ██████╗  ██╗ ██╗   ██╗ ███████╗ ███╗   ██╗
 ██╔════╝ ██╔══██╗ ██╔════╝ ██╔════╝        ██╔══██╗ ██╔══██╗ ██║ ██║   ██║ ██╔════╝ ████╗  ██║
 ███████╗ ██████╔╝ █████╗   ██║      █████╗ ██║  ██║ ██████╔╝ ██║ ██║   ██║ █████╗   ██╔██╗ ██║
 ╚════██║ ██╔═══╝  ██╔══╝   ██║      ╚════╝ ██║  ██║ ██╔══██╗ ██║ ╚██╗ ██╔╝ ██╔══╝   ██║╚██╗██║
 ███████║ ██║      ███████╗ ╚██████╗        ██████╔╝ ██║  ██║ ██║  ╚████╔╝  ███████╗ ██║ ╚████║
 ╚══════╝ ╚═╝      ╚══════╝  ╚═════╝        ╚═════╝  ╚═╝  ╚═╝ ╚═╝   ╚═══╝   ╚══════╝ ╚═╝  ╚═══╝

  █████╗   ██████╗  ███████╗ ███╗   ██╗ ████████╗ ██╗  ██████╗     ██████╗  ███████╗ ██╗   ██╗
 ██╔══██╗ ██╔════╝  ██╔════╝ ████╗  ██║ ╚══██╔══╝ ██║ ██╔════╝     ██╔══██╗ ██╔════╝ ██║   ██║
 ███████║ ██║  ███╗ █████╗   ██╔██╗ ██║    ██║    ██║ ██║          ██║  ██║ █████╗   ██║   ██║
 ██╔══██║ ██║   ██║ ██╔══╝   ██║╚██╗██║    ██║    ██║ ██║          ██║  ██║ ██╔══╝   ╚██╗ ██╔╝
 ██║  ██║ ╚██████╔╝ ███████╗ ██║ ╚████║    ██║    ██║ ╚██████╗     ██████╔╝ ███████╗  ╚████╔╝
 ╚═╝  ╚═╝  ╚═════╝  ╚══════╝ ╚═╝  ╚═══╝    ╚═╝    ╚═╝  ╚═════╝     ╚═════╝  ╚══════╝   ╚═══╝
 by @marcelsud
``` 
## 🚀 Quick Start

1. **Copy to your project**: `cp -r /path/to/spec-driven-agentic-development/.claude /path/to/your/project/`
2. **Start planning**: `/spec:plan "your project description"`
3. **Follow the workflow**: Plan → Requirements → Design → Tasks → Execute

See the working example in [`todo-app/`](todo-app/) built using this methodology.

## 🎯 The 5-Phase Workflow

```
1. /spec:plan [description]     → Feature List     → [Approval Gate]
2. /spec:requirements [feature] → requirements.md  → [Approval Gate]
3. /spec:design                 → design.md        → [Approval Gate]
4. /spec:tasks                  → tasks.md         → [Approval Gate]
5. /spec:execute [feature]      → Working Code     → [Testing & Deploy]
```

### Phase 1️⃣: Planning (`/spec:plan`)
Break down a project goal into manageable features.
- **Input**: Project description
- **Output**: Feature directories with basic requirements
- **Gate**: "Ready to detail requirements for the first feature?"

### Phase 2️⃣: Requirements (`/spec:requirements`)
Define WHAT needs to be built using EARS format.
- **Input**: Feature name
- **Output**: Detailed `requirements.md` with testable specifications
- **Gate**: "Requirements complete. Ready for design phase?"

### Phase 3️⃣: Design (`/spec:design`)
Define HOW it will be built with technical specifications.
- **Input**: Approved requirements
- **Output**: `design.md` with architecture, APIs, and data models
- **Gate**: "Technical design complete. Ready for task breakdown?"

### Phase 4️⃣: Tasks (`/spec:tasks`)
Break down design into TDD implementation steps.
- **Input**: Approved design
- **Output**: `tasks.md` with Red-Green-Refactor cycles
- **Gate**: "Task breakdown complete. Ready to implement?"

### Phase 5️⃣: Implementation (`/spec:execute`)
Execute the implementation plan using TDD.
- **Input**: Task breakdown
- **Output**: Working, tested code
- **Approaches**: TDD, Standard, Collaborative, or Self-implementation

## 📋 Commands Reference

| Phase | Command | Purpose |
|-------|---------|---------|
| 1️⃣ | `/spec:plan [description]` | Break down project into features |
| 2️⃣ | `/spec:requirements [feature]` | Create EARS requirements |
| 3️⃣ | `/spec:design` | Generate technical design |
| 4️⃣ | `/spec:tasks` | Create TDD implementation plan |
| 5️⃣ | `/spec:execute [feature]` | Execute implementation |
| ⚡ | `/spec:advanced` | Enhanced enterprise analysis |
| 📋 | `/spec:list` | List all features |
| 📊 | `/spec:status` | Show implementation status |
| ❓ | `/spec:help` | Command help |

## 🔧 Key Concepts

### EARS Requirements Format
Structured, testable requirements using standardized patterns:

| Pattern | Format |
|---------|--------|
| **Ubiquitous** | "The system SHALL [requirement]" |
| **Event-Driven** | "WHEN [trigger] THEN the system SHALL [response]" |
| **State-Driven** | "WHILE [state] the system SHALL [requirement]" |
| **Conditional** | "IF [condition] THEN the system SHALL [requirement]" |

**Example**: "WHEN a user enters incorrect credentials three times THEN the system SHALL lock the account for 15 minutes."

### Test-Driven Development (TDD)
Every implementation follows the Red-Green-Refactor cycle:
1. **🔴 Red**: Write failing test
2. **🟢 Green**: Write minimal code to pass
3. **🔄 Refactor**: Improve code while keeping tests green

### Quality Gates
- ✅ **Requirements**: Testable, specific, EARS-formatted
- ✅ **Design**: Addresses all requirements, technically sound
- ✅ **Tasks**: Granular, actionable, includes test scenarios

## 📁 Project Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md                 # Complete methodology
│   ├── commands/spec/            # Slash commands
│   │   ├── plan.md, requirements.md, design.md
│   │   ├── tasks.md, execute.md, advanced.md
│   │   ├── list.md, status.md, help.md
│   └── templates/                # Reference templates
│       ├── requirements.md, design.md, tasks.md
└── features/                     # Generated specifications
    └── [feature-name]/
        ├── requirements.md       # EARS requirements
        ├── design.md            # Technical design
        ├── tasks.md             # TDD task breakdown
        └── task_*_completed.md  # Completion summaries
```

## 💡 Why This Works

**Problems Solved:**
- ❌ Context overload → ✅ Focused commands
- ❌ Reliability issues → ✅ Smaller, reliable operations
- ❌ Poor iteration → ✅ Independent phase modification
- ❌ Vague requirements → ✅ EARS precision

**Benefits:**
- **Human Control**: Explicit approval gates
- **Quality Assurance**: Built-in testing via TDD
- **Iterative**: Easy to refine individual phases
- **Scalable**: Works for simple features to complex systems

## 🛠️ Installation

### Prerequisites
- AI coding assistant (Claude Code, Cursor, etc.)
- Basic understanding of software development

### Setup
```bash
# Clone and copy to your project
git clone https://github.com/your-repo/spec-driven-agentic-development
cp -r spec-driven-agentic-development/.claude /path/to/your/project/
```

### Usage
1. Load `.claude/CLAUDE.md` as context for your AI tool
2. Start with `/spec:plan "your project description"`
3. Follow the 5-phase workflow with approval gates
4. Use `/spec:list` and `/spec:status` to track progress

## 📚 Examples

- **[Todo App](todo-app/)**: Complete example built using this methodology
- **[Features](features/)**: Actual specifications used to build the todo app
- **[Templates](.claude/templates/)**: Reference templates for each phase

## 🤝 Contributing

Improvements welcome via issues and pull requests. This methodology evolved from practical AI-assisted development experience.

---

**Ready to build better software?** Start with: `/spec:plan your-awesome-project` 🚀