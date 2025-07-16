# Agentic Development Workflow using Specs

This repository contains a structured set of Markdown documents designed to guide agentic AI development tools (like Google's Gemini, Anthropic's Claude, or others) in building software features in a controlled, iterative, and professional manner.

The core idea is to formalize the development process into distinct phases, each with its own specification document. This allows for clear communication, explicit approval gates, and a high degree of control over the AI's work.

## How to Use with an Agentic AI Tool

This workflow is designed to be tool-agnostic. The general process involves providing the AI agent with the content of these files as context for the tasks.

1.  **Provide Initial Context**: Start by giving the agent the content of `docs/workflow.md`. This file is the main entry point and describes the entire workflow. You can do this by copying and pasting the content into your prompt or by referencing the file if the tool supports it.

2.  **Load Supporting Documents**: As you progress through the development phases, provide the content of the other relevant documents (`advanced/advanced_mode.md`, `methodology/tdd.md`, `methodology/best_practices.md`, etc.) to the agent. The `docs/workflow.md` file itself contains references to indicate when a particular document is relevant.

3.  **Follow the Phases**: Interact with the agent by following the phases outlined in `docs/workflow.md`:
    *   **Phase 1: Requirements**: Ask the agent to generate a `requirements.md` file based on your feature idea.
    *   **Phase 2: Design**: Once requirements are approved, ask the agent to create a `design.md` file.
    *   **Phase 3: Tasks**: After approving the design, have the agent break it down into an actionable `tasks.md` file.
    *   **Phase 4: Implementation**: Finally, instruct the agent to implement the feature based on the tasks, using the methodology you prefer (TDD is recommended).

4.  **Use as a Guide**: These documents are not just for the agent; they are for you. Use them to structure your requests and to ensure the agent is following a sound engineering process.

## File Structure

### Core Documentation (`docs/`)
-   `docs/workflow.md`: The main document. It outlines the entire interactive workflow, including all phases and interaction patterns. **This is your starting point.**
-   `docs/structure.md`: Details the expected structure and content for the `requirements.md`, `design.md`, and `tasks.md` files that will be generated during the workflow.

### Development Methodology (`methodology/`)
-   `methodology/tdd.md`: Describes the Test-Driven Development (TDD) process in detail, including the Red-Green-Refactor cycle and its benefits. Load this file when you want the agent to follow a strict TDD approach.
-   `methodology/ears.md`: Provides examples of the EARS (Easy Approach to Requirements Syntax) format for writing clear and unambiguous requirements.
-   `methodology/best_practices.md`: A collection of general software development best practices to guide the agent.

### Advanced Features (`advanced/`)
-   `advanced/advanced_mode.md`: An optional extension to the standard workflow. It provides prompts and capabilities for a more in-depth, enterprise-grade analysis at each phase (e.g., security threat modeling, scalability planning). Load this file to enable "Advanced Mode."
-   `advanced/steering.md`: (Optional) Can be used to provide high-level goals, constraints, or principles that should guide the agent throughout the entire process.

## The Workflow Explained

The process is divided into four main phases, with an explicit approval gate at the end of each one. The agent cannot proceed to the next phase without your approval.

1.  **Requirements Creation**: The agent defines *what* needs to be built.
2.  **Design Creation**: The agent defines *how* it will be built.
3.  **Tasks Creation**: The agent breaks down the "how" into small, implementable steps.
4.  **Implementation**: The agent writes the code, preferably following TDD.

This structured approach ensures that you and the AI are aligned at every step, minimizing wasted effort and producing a higher-quality result.
