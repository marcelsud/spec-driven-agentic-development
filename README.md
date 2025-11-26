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

## Installation

```bash
git clone https://github.com/marcelsud/spec-driven-agentic-development.git
cp -r spec-driven-agentic-development/.claude /path/to/your/project/
```

## Workflow

```
/spec:create [feature]  →  context.md + requirements.md + tasks.md
/spec:execute [feature] →  Implementation
```

## Commands

| Command | Description |
|---------|-------------|
| `/spec:create [feature]` | Generate complete specification |
| `/spec:execute [feature]` | Execute implementation from tasks |
| `/spec:list` | List all features |
| `/spec:status` | Show implementation status |
| `/spec:help` | Command help |

## File Structure

```
your-project/
├── .claude/
│   ├── CLAUDE.md           # Methodology reference
│   └── commands/spec/      # Slash commands
└── features/
    └── [feature-name]/
        ├── context.md      # Context + technical decisions
        ├── requirements.md # EARS-formatted requirements
        └── tasks.md        # TDD task breakdown
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) for details.

---

Made by [Marcelo Santos](https://www.linkedin.com/in/marcelsud/)

[Subscribe](https://buttondown.com/marcelsud) to receive links, insights and more.
