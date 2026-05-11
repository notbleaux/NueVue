# PRD-03: Browser Extension (Context Capture + Task Handoff)

## Objective

Enable users to capture in-browser context and send actionable proposals into the Command Hub without leaving their current workflow.

## Functional Requirements

1. Capture page metadata (URL, title, selected text, notes)
2. Map captured context to existing workspace/project/task scope
3. Submit task proposal to Command Hub in one click ("Send to Hub")
4. Emit traceable activity event for each submission
5. Show submission result and correlation ID to user

## Security and Privacy Requirements

- Enforce workspace permission checks before submission
- Restrict capture to user-approved domains or contexts
- Redact sensitive fields before transmission when configured
- Record consent and submission source in event payload

## Acceptance Criteria

- One-click submission creates task proposal in project scope
- Submission generates a traceable activity event with correlation ID
- Unauthorized submissions are blocked with explicit error messaging
