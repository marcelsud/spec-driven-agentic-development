# Agentic Development Workflow using Specs

This repository contains a structured set of Markdown documents designed to guide agentic AI development tools (like Google's Gemini, Anthropic's Claude, or others) in building software features in a controlled, iterative, and professional manner.

The core idea is to formalize the development process into distinct phases, each with its own specification document. This allows for clear communication, explicit approval gates, and a high degree of control over the AI's work.

## How to Use

### For Claude Code Users (Recommended)

The easiest way to use this framework is with Claude Code's custom slash command:

1. **Clone this repository** to your local machine
2. **Copy the slash command** to your project:
   ```bash
   cp .claude/commands/spec.md /path/to/your/project/.claude/commands/
   ```
3. **Use the `/spec` command** in Claude Code:
   ```
   /spec user authentication system
   /spec shopping cart functionality
   /spec API rate limiting
   ```

The `/spec` command will guide you through the structured workflow with approval gates between each phase.

### For Other AI Tools

This workflow is designed to be tool-agnostic. The general process involves providing the AI agent with the content of these files as context for the tasks.

1.  **Provide Initial Context**: Start by giving the agent the content of `docs/workflow.md`. This file is the main entry point and describes the entire workflow. You can do this by copying and pasting the content into your prompt or by referencing the file if the tool supports it.

2.  **Load Supporting Documents**: As you progress through the development phases, provide the content of the other relevant documents (`advanced/advanced_mode.md`, `methodology/tdd.md`, `methodology/best_practices.md`, etc.) to the agent. The `docs/workflow.md` file itself contains references to indicate when a particular document is relevant.

3.  **Follow the Phases**: Interact with the agent by following the phases outlined in `docs/workflow.md`:
    *   **Phase 0 (Optional): PRD**: Create a Product Requirements Document for business context
    *   **Phase 1: Requirements**: Generate a `requirements.md` file using EARS format
    *   **Phase 2: Design**: Create a `design.md` file with technical specifications
    *   **Phase 3: Tasks**: Break down into an actionable `tasks.md` file with TDD methodology
    *   **Phase 4: Implementation**: Implement the feature following the structured tasks

4.  **Use as a Guide**: These documents are not just for the agent; they are for you. Use them to structure your requests and to ensure the agent is following a sound engineering process.

## File Structure

### Core Documentation (`docs/`)
-   `docs/workflow.md`: The main document. It outlines the entire interactive workflow, including all phases and interaction patterns. **This is your starting point.**
-   `docs/structure.md`: Details the expected structure and content for the `requirements.md`, `design.md`, and `tasks.md` files that will be generated during the workflow.

### Development Methodology (`methodology/`)
-   `methodology/tdd.md`: Describes the Test-Driven Development (TDD) process in detail, including the Red-Green-Refactor cycle and its benefits. Load this file when you want the agent to follow a strict TDD approach.
-   `methodology/ears.md`: Provides examples of the EARS (Easy Approach to Requirements Syntax) format for writing clear and unambiguous requirements.
-   `methodology/prd.md`: Guide for creating Product Requirements Documents to provide business context before technical requirements.
-   `methodology/best_practices.md`: A collection of general software development best practices to guide the agent.

### Advanced Features (`advanced/`)
-   `advanced/advanced_mode.md`: An optional extension to the standard workflow. It provides prompts and capabilities for a more in-depth, enterprise-grade analysis at each phase (e.g., security threat modeling, scalability planning). Load this file to enable "Advanced Mode."
-   `advanced/steering.md`: (Optional) Can be used to provide high-level goals, constraints, or principles that should guide the agent throughout the entire process.

## The Workflow Explained

The process is divided into phases with explicit approval gates. The agent cannot proceed to the next phase without your approval.

0.  **PRD Creation (Optional)**: The agent creates a Product Requirements Document with business context, market analysis, and strategic foundation.
1.  **Requirements Creation**: The agent defines *what* needs to be built using EARS format.
2.  **Design Creation**: The agent defines *how* it will be built with technical specifications.
3.  **Tasks Creation**: The agent breaks down the "how" into small, implementable steps using TDD methodology.
4.  **Implementation**: The agent writes the code, following the structured tasks and TDD approach.

This structured approach ensures that you and the AI are aligned at every step, minimizing wasted effort and producing a higher-quality result.

## Templates and Examples

The framework includes:
- **Templates**: Ready-to-use templates for PRD, requirements, design, and tasks
- **Examples**: A complete sample project showing the workflow in action
- **Slash Command**: Pre-configured Claude Code command for easy access
