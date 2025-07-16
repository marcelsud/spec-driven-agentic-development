# Steering Generation Capability

## Overview
Agent can automatically generate comprehensive steering files to establish project context, technical standards, and organizational principles for any codebase. This capability creates foundational guidance that influences all subsequent AI interactions within the workspace.

## What Steering Generation Does
1. **Analyzes Project Context**: Examines existing files (prompt.md, README, package.json, etc.) to understand project purpose and scope
2. **Creates Foundational Rules**: Generates steering files that encode project-specific knowledge and standards
3. **Establishes Consistency**: Ensures all AI interactions follow consistent patterns and principles
4. **Provides Context**: Gives future AI sessions immediate understanding of project goals and constraints

## Generated Steering File Types

### 1. Product Steering (product.md)
**Purpose**: Defines what the project does and why it exists
**Contents**:
- Core functionality description
- Key features and capabilities
- Target use cases and user scenarios
- Business context and compliance requirements
- Success criteria and objectives

**Example Structure**:
```markdown
# Product Overview
[Project description and purpose]

## Core Functionality
- [Primary features]
- [Key capabilities]

## Key Features
- [Feature list with brief descriptions]

## Target Use Cases
- [Specific scenarios and user needs]
```

### 2. Technical Steering (tech.md)
**Purpose**: Establishes technical architecture and development standards
**Contents**:
- Technology stack decisions and rationale
- Architectural patterns and principles
- Development tools and frameworks
- Technical constraints and requirements
- Common commands and workflows

**Example Structure**:
```markdown
# Technology Stack

## Architecture
- [High-level architecture description]
- [Key architectural decisions]

## Tech Stack
- **Language**: [Primary language with rationale]
- **Database**: [Database choice and reasoning]
- **Framework**: [Framework selection]

## Key Technical Requirements
- [Critical technical constraints]
- [Performance/security/compliance needs]

## Development Principles
- [Coding standards and practices]
```

### 3. Structure Steering (structure.md)
**Purpose**: Defines project organization and file/folder conventions
**Contents**:
- Directory structure and organization
- File naming conventions
- Module organization principles
- Code organization patterns
- Documentation structure

**Example Structure**:
```markdown
# Project Structure

## Current Organization
[Current directory tree]

## Planned Structure
[Future/target directory organization]

## Key Principles
- [Organizational principles]
- [Separation of concerns]

## File Naming Conventions
- [Naming patterns and rules]

## Module Organization
- [How code should be organized]
```

## Steering Generation Process

### Step 1: Project Analysis
1. **File Discovery**: Scan workspace for key files (prompt.md, README, package.json, etc.)
2. **Content Analysis**: Extract project purpose, technology hints, and organizational patterns
3. **Context Extraction**: Identify domain, technical requirements, and constraints
4. **Pattern Recognition**: Detect existing conventions and standards

### Step 2: Content Generation
1. **Product Definition**: Create clear product overview based on project description
2. **Technical Standards**: Establish technology stack and architectural principles
3. **Organizational Rules**: Define structure, naming, and organizational conventions
4. **Integration Points**: Ensure steering files work together cohesively

### Step 3: File Creation
1. **Atomic Creation**: Generate all steering files simultaneously for consistency
2. **Cross-Reference**: Ensure files reference and complement each other
3. **Validation**: Check that generated content aligns with discovered project context
4. **Optimization**: Keep content concise but comprehensive

## Advanced Steering Generation Features

### Context-Aware Generation
- **Domain-Specific**: Generates appropriate content for different domains (web apps, APIs, data processing, etc.)
- **Technology-Aware**: Adapts to detected or specified technology stacks
- **Compliance-Focused**: Emphasizes regulatory/compliance aspects when detected
- **Scale-Appropriate**: Adjusts complexity based on project size and scope

### Incremental Enhancement
- **Iterative Improvement**: Can update steering files as project evolves
- **Context Addition**: Add new steering files for specific aspects (security.md, deployment.md)
- **Rule Refinement**: Enhance existing rules based on implementation learnings
- **Standard Evolution**: Update standards as team practices mature

### Integration Capabilities
- **Spec Integration**: Steering rules influence spec generation and implementation
- **Code Generation**: Technical steering guides code structure and patterns
- **Documentation**: Structure steering influences documentation organization
- **Testing**: Technical principles guide testing strategies and patterns

## Best Practices for Steering Generation

### Content Quality
1. **Specificity**: Make rules specific to the project, not generic
2. **Actionability**: Ensure rules provide clear, actionable guidance
3. **Consistency**: Maintain consistency across all steering files
4. **Completeness**: Cover all major aspects of project development
5. **Clarity**: Use clear, unambiguous language

### File Organization
1. **Logical Separation**: Keep different concerns in separate files
2. **Cross-References**: Link related concepts across files
3. **Hierarchical Structure**: Organize content from general to specific
4. **Searchable Content**: Structure for easy reference and searching
5. **Version Control**: Track changes to steering rules over time

### Maintenance Strategy
1. **Regular Review**: Periodically review and update steering files
2. **Team Alignment**: Ensure steering reflects team consensus
3. **Evolution Tracking**: Document why steering rules change
4. **Conflict Resolution**: Address conflicts between steering files
5. **Deprecation**: Remove outdated or conflicting guidance

## Usage Patterns

### Initial Project Setup
```
User: "Generate basic steering files for this project"
Agent: [Analyzes context, creates product.md, tech.md, structure.md]
```

### Specific Domain Enhancement
```
User: "Add security steering for this API project"
Agent: [Creates security.md with API-specific security guidance]
```

### Technology Migration
```
User: "Update steering for migration from REST to GraphQL"
Agent: [Updates tech.md and structure.md for GraphQL patterns]
```

### Team Onboarding
```
User: "Create comprehensive steering for new team members"
Agent: [Generates detailed steering covering all project aspects]
```

## Integration with Other Agent Features

### Spec Generation
- Steering rules influence requirement gathering
- Technical steering guides design decisions
- Structure steering shapes implementation tasks

### Code Generation
- Technical principles guide code structure
- Naming conventions influence generated code
- Architectural patterns shape implementation

### Documentation
- Structure steering guides documentation organization
- Product steering influences user-facing documentation
- Technical steering shapes developer documentation

### Testing Strategy
- Technical principles guide testing approaches
- Structure steering influences test organization
- Compliance requirements shape testing coverage

## Steering File Lifecycle

### Creation Phase
1. **Analysis**: Understand project context and requirements
2. **Generation**: Create comprehensive steering files
3. **Validation**: Ensure consistency and completeness
4. **Integration**: Connect with existing project structure

### Evolution Phase
1. **Monitoring**: Track how steering rules are used
2. **Feedback**: Collect input on rule effectiveness
3. **Refinement**: Update rules based on experience
4. **Expansion**: Add new steering files as needed

### Maintenance Phase
1. **Review**: Regular assessment of rule relevance
2. **Updates**: Keep rules current with project evolution
3. **Cleanup**: Remove outdated or conflicting guidance
4. **Documentation**: Track changes and rationale

## Key Benefits

### For Development Teams
- **Consistency**: Ensures all team members follow same standards
- **Onboarding**: New team members quickly understand project context
- **Decision Making**: Provides framework for technical decisions
- **Quality**: Maintains code and architecture quality over time

### For AI Assistance
- **Context Awareness**: AI understands project specifics immediately
- **Consistent Guidance**: All AI interactions follow same principles
- **Reduced Ambiguity**: Clear rules reduce misunderstandings
- **Improved Suggestions**: AI recommendations align with project goals

### For Project Success
- **Reduced Technical Debt**: Consistent standards prevent accumulation of debt
- **Faster Development**: Clear guidelines speed up development decisions
- **Better Maintainability**: Organized structure improves long-term maintenance
- **Risk Mitigation**: Standards help avoid common pitfalls and mistakes

