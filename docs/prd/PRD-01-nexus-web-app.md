# PRD-01: NueVue Web App (Nexus Command Hub Deluxe Homepage + UI)

## Objective

Deliver a premium command-center homepage that gives project managers and agent operators one place to monitor project health, trigger actions, and confirm launch readiness.

## Users

- Workspace owner
- Project manager
- AI agent operator

## Core Functional Requirements

1. **Hero Command Panel**
   - Show workspace health score
   - Show active milestones count
   - Show launch state (Foundation, Internal Beta, Early Access Live)
   - Provide quick actions to start orchestration runs and escalate blockers

2. **Live Activity Timeline**
   - Show planner, builder, reviewer, and operator events in chronological order
   - Filter by project, role, severity, and status
   - Support near-real-time updates from activity stream

3. **Office Scene Visualization (Animated)**
   - Visualize agent presence and handoffs as an office scene (planning/build/review/ops zones)
   - Provide visual + social cues for progression (approvals, blockers, escalations, WIP/queues)
   - Reflect work happening across surfaces (IDE, terminal, chat) in one coherent timeline using correlation IDs

4. **Project Board Snapshot**
   - Show milestone progress bars
   - Show blocker cards and SLA risk indicators
   - Provide direct action links to approve/retry/escalate/cancel workflows

5. **Service Health Cards**
   - Show API service status
   - Show orchestration service status
   - Show realtime service status
   - Show uptime and latest incidents

6. **Release Rail**
   - Show current version
   - Show patch status
   - Show test pass trend
   - Show rollback readiness state

## Non-Functional Requirements

- Homepage first render target: <= 2 seconds at p50 on broadband
- Activity stream latency target: <= 3 seconds from event creation to UI update
- Role-based access control by workspace membership
- Audit trail for all command actions

## Success Criteria

- User can detect blockers in under 2 minutes
- User can trigger workflow actions from one hub
- Homepage remains synchronized with service lifecycle events in near-real-time

## Dependencies

- Command Hub API endpoints
- Realtime activity stream
- Service health and release status feeds
