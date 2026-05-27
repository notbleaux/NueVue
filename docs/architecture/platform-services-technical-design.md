# Platform Services Technical Design (NueVue, PixelOffice-inspired)

## System Overview

NueVue command operations use a hybrid model:

- **Synchronous APIs** for command and query actions
- **Asynchronous events** for lifecycle updates and live UI refresh

## Service Responsibilities

### API Service

- Owns canonical records for users, workspaces, projects, milestones, tasks, releases
- Performs request validation and authorization checks
- Persists command requests and returns command IDs/correlation IDs

### Orchestration Service

- Consumes command requests
- Executes role-based state machine:
  - `queued -> in_progress -> review_pending -> completed`
  - Terminal failure path: `failed` (with retry/escalation options)
- Produces lifecycle events for each state transition

### Realtime Service

- Subscribes to event bus
- Fans out project-scoped activity streams to clients
- Supports replay windows for recent history to hydrate dashboards

## Data Flow

1. User submits command in Nexus or Extension
2. API validates and stores request
3. Orchestration processes request and emits events
4. Realtime service broadcasts events to subscribed clients
5. Nexus updates command panel, timeline, and board state

## Reliability and Observability

## Local Dev and Deployment Baseline

- **Local dev**: use Docker Compose to run NuMuN services together (API + orchestration + realtime) with a shared contracts version pinned for the workspace.
- **Web surfaces**: deploy NeXeZ website/web app to Vercel.
- **Services**: deploy NuMuN services to Railway or Render (environment separation per release stage).

- Idempotency keys required on write commands
- Retries with bounded exponential backoff
- Dead-letter queue for unprocessable orchestration events
- Health endpoints required for all services
- SLO metrics:
  - API success rate
  - Orchestration completion latency
  - Realtime delivery latency

## Security Controls

- AuthN/AuthZ on all service routes
- Workspace-scoped authorization for all command actions
- Immutable audit log for command and orchestration lifecycle events
