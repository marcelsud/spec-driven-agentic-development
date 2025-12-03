---
description: Review a feature specification for completeness, EARS compliance, and quality
allowed-tools: Read(*), Glob(*), Grep(*), Edit(*), Write(*), AskUserQuestion
---

# Review Feature Specification

Review a feature specification for completeness, EARS format compliance, and identify areas for improvement.

## Feature: $ARGUMENTS

## Feature Selection

1. **IF a feature name is provided in `$ARGUMENTS`**:
   - Find a directory in `features/` that matches `$ARGUMENTS`
   - If no exact match, search for closest match and ask for confirmation

2. **IF no feature name is provided**:
   - List all directories under `features/`
   - If only one exists, select it automatically
   - If multiple exist, ask user to specify using `AskUserQuestion`

## Your Task

Analyze the feature specification files and produce a comprehensive quality review.

## Process

### Step 1: Load Feature Files

Read all specification files:
- `features/[feature-name]/context.md`
- `features/[feature-name]/requirements.md`
- `features/[feature-name]/tasks.md`

If any file is missing, note it as a critical issue.

### Step 2: Review context.md

Check for required sections:
- [ ] Overview - Brief description of the feature
- [ ] Goals - What the feature aims to achieve
- [ ] Scope - In Scope / Out of Scope clearly defined
- [ ] Technical Decisions - Stack, architecture, key decisions with rationale
- [ ] Constraints & Considerations - Limitations and important factors
- [ ] Dependencies - External dependencies and requirements

**Flag as issues:**
- Missing sections (Critical)
- Empty or placeholder content (Warning)
- Technical decisions without rationale (Suggestion)

### Step 3: Review requirements.md - EARS Compliance

#### Check EARS Format

Each requirement must use one of these patterns:

| Type | Pattern | Example |
|------|---------|---------|
| Ubiquitous | "The system SHALL [requirement]" | The system SHALL encrypt all passwords |
| Event-Driven | "WHEN [trigger] THEN the system SHALL [response]" | WHEN user clicks submit THEN the system SHALL validate input |
| State-Driven | "WHILE [state] the system SHALL [requirement]" | WHILE processing payment the system SHALL display progress |
| Conditional | "IF [condition] THEN the system SHALL [requirement]" | IF cart is empty THEN the system SHALL show empty message |
| Optional | "WHERE [feature] the system SHALL [requirement]" | WHERE premium enabled the system SHALL allow exports |

**Validation Rules:**
1. Must contain "SHALL" keyword for mandatory requirements
2. Event-Driven: Must have "WHEN" and "THEN"
3. State-Driven: Must start with "WHILE"
4. Conditional: Must have "IF" and "THEN"

#### Flag Ambiguous Terms

Search for and flag these vague terms:
- "quickly", "fast", "slow" - Specify time (e.g., "within 2 seconds")
- "appropriate", "reasonable", "adequate" - Define specific criteria
- "user-friendly", "intuitive", "easy" - Describe measurable behavior
- "properly", "correctly" - Specify expected outcome
- "some", "few", "many", "several" - Use specific numbers
- "etc.", "and so on" - List all items explicitly

### Step 4: Review tasks.md

Check each task for:
- [ ] Clear description of what needs to be done
- [ ] Test scenarios (Red-Green-Refactor or test cases)
- [ ] Acceptance criteria tied to requirements
- [ ] Dependencies on other tasks (if applicable)

**Flag as issues:**
- Tasks without test scenarios (Critical)
- Tasks without acceptance criteria (Warning)
- Circular dependencies (Critical)
- Orphaned tasks with no requirement connection (Suggestion)

### Step 5: Cross-Reference Analysis

1. **Requirements Coverage**: For each requirement in requirements.md, verify there's at least one task addressing it
2. **Task Traceability**: For each task, verify it references a requirement
3. **Identify gaps**: Requirements without tasks, tasks without requirements

### Step 6: Generate Review Report

Present findings organized by severity:

```markdown
## Specification Review: [Feature Name]

### Summary
| File | Status | Issues |
|------|--------|--------|
| context.md | [Complete/Incomplete/Missing] | [count] |
| requirements.md | [EARS Compliant/Issues Found/Missing] | [count] |
| tasks.md | [Complete/Incomplete/Missing] | [count] |

### Critical Issues
[Issues that must be addressed before implementation]
1. [File:Line] Issue description
   - Suggested fix: [how to fix]

### Warnings
[Issues that should be addressed]
1. [File:Line] Issue description

### Suggestions
[Improvements that could be made]
1. [File:Line] Suggestion

### EARS Compliance Details
| Requirement | Type | Status | Issue |
|-------------|------|--------|-------|
| REQ-001 | Event-Driven | Valid | - |
| REQ-002 | Ubiquitous | Invalid | Missing SHALL |

### Coverage Analysis
- Requirements with tasks: X/Y (Z%)
- Requirements without tasks: [list]
- Tasks without requirement reference: [list]

### Ambiguous Terms Found
| Term | Location | Suggested Replacement |
|------|----------|----------------------|
| "quickly" | requirements.md:15 | "within 500ms" |
```

### Step 7: Offer Fixes

Use `AskUserQuestion` to ask:

"I found [X] issues in the specification. Would you like me to fix any of these?"

Options (multiSelect: true):
- **Fix EARS formatting** - Add missing SHALL keywords, correct patterns
- **Remove ambiguous terms** - Replace vague terms with placeholders for you to fill
- **Add missing sections** - Create skeleton sections in context.md
- **Skip fixes** - Just show the review report without making changes

### Step 8: Apply Fixes (if requested)

For each selected fix category:
1. Make the edits using the `Edit` tool
2. Track what was changed

### Step 9: Present Final Results

**DO NOT create a review.md file.** Instead, present the results directly to the user:

1. Show the complete review report in the output
2. If fixes were applied, include a "Corrections Applied" section listing:
   - File and line number
   - Original content
   - New content
3. End with a summary:
   - Total issues found
   - Issues fixed
   - Remaining issues (if any)

## Example Output

```
## Specification Review: user-authentication

### Summary
| File | Status | Issues |
|------|--------|--------|
| context.md | Complete | 1 |
| requirements.md | Issues Found | 4 |
| tasks.md | Incomplete | 2 |

### Critical Issues
1. [requirements.md:23] REQ-005 missing SHALL keyword
   - Current: "The system will validate tokens"
   - Suggested fix: "The system SHALL validate tokens"

2. [tasks.md:45] Task 4 has no test scenarios defined
   - Suggested fix: Add Red-Green-Refactor steps

### Warnings
1. [requirements.md:15] Uses ambiguous term "quickly"
   - Suggested fix: Specify time constraint (e.g., "within 2 seconds")

2. [requirements.md:31] NFR-002 lacks measurable criteria
   - Current: "System should be responsive"
   - Suggested fix: "System SHALL respond within 200ms"

### Suggestions
1. [context.md:8] Technical decision lacks rationale
   - "Using JWT for authentication" - Add why JWT was chosen

2. [tasks.md:12] Task 2 could be split for better granularity

### EARS Compliance: 8/12 requirements valid (67%)

### Coverage Analysis
- Requirements with tasks: 10/12 (83%)
- Requirements without tasks: REQ-011, REQ-012
- Tasks without requirement reference: Task 6

### Corrections Applied ✓
| File | Line | Original | Corrected |
|------|------|----------|-----------|
| requirements.md | 23 | "The system will validate tokens" | "The system SHALL validate tokens" |
| requirements.md | 15 | "respond quickly" | "respond within 2 seconds" |

---
**Review Summary**
- Issues found: 7
- Issues fixed: 2
- Remaining issues: 5
```
