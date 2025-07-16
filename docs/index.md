# Kiro Spec Documentation Index

## Quick Start
Start here to understand the agentic development workflow:
- [README.md](../README.md) - Project overview and setup
- [workflow.md](workflow.md) - **Main workflow guide** (start here)
- [structure.md](structure.md) - Spec file structure and templates

## Development Methodology
Learn about the development approaches and best practices:
- [tdd.md](../methodology/tdd.md) - Test-Driven Development process
- [ears.md](../methodology/ears.md) - Requirements syntax (EARS format)
- [prd.md](../methodology/prd.md) - Product Requirements Document guide
- [best_practices.md](../methodology/best_practices.md) - General development best practices

## Advanced Features
Enhance your workflow with advanced capabilities:
- [advanced_mode.md](../advanced/advanced_mode.md) - Advanced workflow options
- [steering.md](../advanced/steering.md) - Project steering and context generation

## Templates and Examples
Resources for implementing the workflow:
- [templates/](../templates/) - Template files for specs (requirements, design, tasks, PRD)
- [examples/](../examples/) - Example implementations

## Navigation Guide

### For First-Time Users
1. Read [README.md](../README.md) for project overview
2. Study [workflow.md](workflow.md) for the main process
3. Review [structure.md](structure.md) for spec file formats
4. Explore [methodology/](../methodology/) for development approaches

### For Experienced Users
- Jump to [advanced_mode.md](../advanced/advanced_mode.md) for enhanced capabilities
- Check [steering.md](../advanced/steering.md) for project context features
- Use [templates/](../templates/) for quick spec creation

### For Developers
- Review [best_practices.md](../methodology/best_practices.md) for coding standards
- Study [tdd.md](../methodology/tdd.md) for testing methodology
- Use [templates/](../templates/) for structured development

## File Organization

```
kiro_spec/
├── README.md                    # Project overview
├── docs/                        # Core documentation
│   ├── index.md                # This file
│   ├── workflow.md             # Main workflow guide
│   └── structure.md            # Spec structure
├── methodology/                # Development approaches
│   ├── tdd.md                 # Test-driven development
│   ├── ears.md                # Requirements syntax
│   ├── prd.md                 # Product requirements
│   └── best_practices.md      # Best practices
├── advanced/                   # Advanced features
│   ├── advanced_mode.md       # Advanced capabilities
│   └── steering.md            # Project steering
├── templates/                  # Template files
└── examples/                   # Example implementations
```

## Workflow Summary

The Kiro Spec workflow follows these phases:
0. **PRD (Optional)** - Define business context and strategic foundation
1. **Requirements** - Define what needs to be built (using EARS format)
2. **Design** - Define how it will be built  
3. **Tasks** - Break down into implementation steps
4. **Implementation** - Execute using TDD or other methodology

Each phase has explicit approval gates and can be enhanced with advanced mode capabilities.