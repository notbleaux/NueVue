# PRD-02: Platform Services (API, Orchestration, Realtime Activity)

## Objective

Provide reliable backend services for workspace/project management, multi-agent workflow execution, and live activity delivery to the Nexus Web App and extension clients.

## Service Scope

1. **API Service**
   - Manage users, workspaces, projects, milestones, tasks, releases
   - Expose versioned REST endpoints
   - Enforce authentication and authorization on every route

2. **Orchestration Service**
   - Route tasks to Planner, Builder, Reviewer, Operator roles
   - Execute state-machine workflows
   - Support retries, escalation, and cancellation
   - Emit auditable lifecycle events

3. **Realtime Service**
   - Publish activity events via event bus
   - Maintain presence channels by workspace/project
   - Offer subscription feeds for dashboards and extension clients

## Non-Functional Requirements

- AuthN/AuthZ on all routes
- Auditable event history for every command action
- Backward-compatible API versioning strategy
- Observable SLOs and defined error budgets
- Idempotency support for command actions

## Acceptance Criteria

- Command Hub endpoints are available and versioned
- Orchestration workflows expose deterministic state transitions
- Realtime activity feed supports project-scoped subscriptions
- Service health endpoints expose uptime and degradation state
