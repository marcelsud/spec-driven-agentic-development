# EARS Format (Easy Approach to Requirements Syntax)

## Overview
EARS (Easy Approach to Requirements Syntax) is a structured approach to writing clear, unambiguous requirements. It provides templates that help ensure requirements are testable, traceable, and implementable.

## What is EARS?
EARS was developed by Rolls-Royce to improve the quality of requirements in safety-critical systems. It provides a set of templates that standardize how requirements are written, making them more precise and reducing ambiguity.

## EARS Templates

### 1. Ubiquitous Requirements
For requirements that always apply:
- **Format**: "The system SHALL [requirement]"
- **Example**: "The system SHALL validate user credentials before granting access"

### 2. Event-Driven Requirements
For requirements triggered by specific events:
- **Format**: "WHEN [trigger event] THEN the system SHALL [system response]"
- **Example**: "WHEN a user submits invalid credentials THEN the system SHALL display an error message"

### 3. State-Driven Requirements
For requirements that depend on system state:
- **Format**: "WHILE [in specific state] the system SHALL [requirement]"
- **Example**: "WHILE processing a payment the system SHALL display a loading indicator"

### 4. Optional Feature Requirements
For requirements that apply only under certain conditions:
- **Format**: "WHERE [feature is included] the system SHALL [requirement]"
- **Example**: "WHERE two-factor authentication is enabled the system SHALL request a verification code"

### 5. Conditional Requirements
For requirements with logical conditions:
- **Format**: "IF [condition] THEN the system SHALL [requirement]"
- **Example**: "IF user account is locked THEN the system SHALL prevent login attempts"

## Best Practices for Using EARS

### 1. Use Active Voice
- **Good**: "The system SHALL validate input"
- **Poor**: "Input SHALL be validated"

### 2. Be Specific and Measurable
- **Good**: "The system SHALL respond within 2 seconds"
- **Poor**: "The system SHALL respond quickly"

### 3. Use "SHALL" for Mandatory Requirements
- **SHALL**: Mandatory requirement
- **SHOULD**: Recommended but not mandatory
- **MAY**: Optional feature

### 4. One Requirement Per Statement
- **Good**: "WHEN user clicks submit THEN the system SHALL validate the form"
- **Poor**: "WHEN user clicks submit THEN the system SHALL validate the form AND save the data AND redirect to confirmation page"

### 5. Avoid Ambiguous Terms
- **Avoid**: "appropriate", "reasonable", "adequate", "user-friendly"
- **Use**: Specific, measurable terms

## Practical Examples

### User Authentication System
1. **Ubiquitous**: "The system SHALL require user authentication for all protected resources"
2. **Event-Driven**: "WHEN a user enters incorrect credentials three times THEN the system SHALL lock the account for 15 minutes"
3. **State-Driven**: "WHILE a user session is active the system SHALL refresh the authentication token every 30 minutes"
4. **Conditional**: "IF a user's session expires THEN the system SHALL redirect to the login page"

### E-commerce Shopping Cart
1. **Ubiquitous**: "The system SHALL maintain cart contents during a user session"
2. **Event-Driven**: "WHEN a user adds an item to cart THEN the system SHALL update the cart total"
3. **State-Driven**: "WHILE viewing the cart the system SHALL display shipping options"
4. **Conditional**: "IF inventory is insufficient THEN the system SHALL display an out-of-stock message"

### API Response Handling
1. **Ubiquitous**: "The system SHALL return responses in JSON format"
2. **Event-Driven**: "WHEN an API request fails THEN the system SHALL return an appropriate HTTP status code"
3. **State-Driven**: "WHILE processing a request the system SHALL maintain transaction isolation"
4. **Conditional**: "IF authentication fails THEN the system SHALL return HTTP 401 Unauthorized"

## Common Pitfalls to Avoid

### 1. Combining Multiple Requirements
- **Wrong**: "WHEN user submits form THEN system SHALL validate data AND save to database AND send email"
- **Right**: Split into separate requirements for each action

### 2. Using Vague Language
- **Wrong**: "The system SHALL provide good performance"
- **Right**: "The system SHALL respond to user requests within 2 seconds"

### 3. Missing Trigger Conditions
- **Wrong**: "The system SHALL display error message"
- **Right**: "WHEN validation fails THEN the system SHALL display error message"

### 4. Mixing Requirements with Design
- **Wrong**: "The system SHALL use PostgreSQL to store user data"
- **Right**: "The system SHALL persist user data across sessions"

## Integration with Spec Workflow

### In Requirements Phase
- Use EARS templates to structure all functional requirements
- Each user story should have corresponding EARS-formatted acceptance criteria
- Validate that each requirement is testable and specific

### In Design Phase
- Map EARS requirements to technical solutions
- Ensure design addresses all WHEN/THEN conditions
- Verify that state transitions are properly handled

### In Testing Phase
- Use EARS requirements as test case templates
- WHEN/THEN statements directly translate to test scenarios
- Validate that all conditions and states are tested

## Tools and Tips

### Requirement Validation Checklist
- [ ] Does the requirement use proper EARS syntax?
- [ ] Is the requirement testable?
- [ ] Are all conditions clearly specified?
- [ ] Is the system response clearly defined?
- [ ] Are there any ambiguous terms?

### Common EARS Keywords
- **Triggers**: WHEN, IF, WHERE, WHILE
- **Actions**: SHALL, SHOULD, MAY
- **Responses**: THEN, the system SHALL
- **Conditions**: AND, OR, NOT

### Review Questions
1. Can this requirement be tested?
2. Is the trigger condition clear?
3. Is the system response specific?
4. Are there any missing edge cases?
5. Does this requirement conflict with others?

## Benefits of Using EARS

### For Development Teams
- **Clarity**: Reduces misunderstandings and ambiguity
- **Testability**: Requirements directly translate to test cases
- **Completeness**: Structured approach ensures comprehensive coverage
- **Traceability**: Clear link between requirements and implementation

### For Stakeholders
- **Understanding**: Standardized format is easier to review
- **Validation**: Clear acceptance criteria for feature approval
- **Communication**: Common language for discussing requirements
- **Quality**: Structured approach improves requirement quality

### For AI-Assisted Development
- **Parsing**: Structured format enables better AI understanding
- **Implementation**: Clear requirements guide code generation
- **Testing**: EARS format directly supports test case creation
- **Validation**: Structured criteria enable automated requirement checking