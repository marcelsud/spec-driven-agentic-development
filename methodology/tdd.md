# Test-Driven Development (TDD)

This document describes the Test-Driven Development (TDD) methodology as it applies to the spec-based workflow.

## TDD Methodology: "By the Book"
The recommended implementation approach follows the classic Red-Green-Refactor cycle:

### Red Phase: Write a Failing Test
1. Write a test for the next small piece of functionality.
2. Run the test to confirm it fails (red).
3. Ensure the test fails for the right reason.
4. Write only enough test code to specify the behavior.

### Green Phase: Make the Test Pass
1. Write the minimal amount of production code to make the test pass.
2. Don't worry about code quality yet - just make it work.
3. Run the test to confirm it passes (green).
4. Don't write more code than necessary.

### Refactor Phase: Improve the Code
1. Clean up the production code while keeping tests green.
2. Remove duplication and improve design.
3. Run tests frequently to ensure nothing breaks.
4. Refactor test code as well if needed.

## TDD Benefits for Spec Implementation
- **Requirements Validation**: Tests verify that implementation matches spec requirements.
- **Design Feedback**: Writing tests first reveals design issues early.
- **Documentation**: Tests serve as executable documentation of behavior.
- **Confidence**: A comprehensive test suite enables safe refactoring.
- **Quality**: TDD typically results in better code design and fewer bugs.

## TDD Implementation Flow
1. **Start with acceptance criteria** from `tasks.md` as test scenarios.
2. **Write unit tests** for individual components and functions.
3. **Write integration tests** for API endpoints and database operations.
4. **Implement code** to satisfy tests, one small piece at a time.
5. **Refactor continuously** to improve design while maintaining green tests.

---

## TDD in the Interactive Workflow

### Implementation Approach Selection
When it's time to implement, the agent will propose TDD:

- **Agent**: "The tasks are ready for implementation. The recommended approach is Test-Driven Development (TDD). See `tdd.md` for details on this process. Would you like to proceed with TDD implementation?"
- **User responses**:
  - "Yes, use TDD" → Begin TDD implementation cycle.
  - "No, implement without TDD" → Begin standard implementation.
  - "I'll implement myself" → User takes over implementation.
  - "Let's do it together" → Collaborative implementation approach.

### TDD Implementation Process
Once TDD is selected, the process for each task is:
1.  Write failing tests first (Red).
2.  Implement minimal code to make tests pass (Green).
3.  Refactor code while keeping tests green (Refactor).
4.  Repeat the cycle for each piece of functionality.