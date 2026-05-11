# ARD-001: Nexus Office Scene + Activity Backbone

## Summary

Define the engineering requirements for the Nexus office scene visualization so it can reliably reflect real project progress using the activity stream and orchestration lifecycle events, while staying accessible and performant.

## Scope

- In scope:
  - Office scene zones (planning/build/review/ops) mapped to real workflow states and roles
  - Activity stream requirements (replay window, filters, correlation rules)
  - Contract requirements for orchestration lifecycle state changes to drive visualization
  - Accessibility and performance constraints for motion-heavy UI
- Out of scope:
  - Final sprite art pack production pipeline
  - Full auth provider selection/implementation (covered by PRD-05)

## Impacted Components

- Services/modules:
  - API Service (Command Hub API)
  - Orchestration Service (workflow state machine + actions)
  - Realtime Service (activity stream delivery + replay)
- Client surfaces:
  - Nexus (office scene + timeline + board)
  - Browser extension (“Send to Hub” submissions)
  - IDE/terminal integrations (later; must conform to same activity model)

## Contract and Data Requirements

- Event requirements:
  - Events MUST include `correlation_id` and be stable across downstream transitions.
  - Events MUST include `actor_role`, `action_type`, `status`, `severity`, and `timestamp`.
  - The taxonomy MUST remain backwards compatible; new action types extend rather than replace.
- Activity stream query requirements:
  - Filter by `project_id`, role, severity, and status (PRD-01).
  - Support `since` cursor for replay hydration (OpenAPI `/activity/stream`).
- Orchestration state requirements:
  - State machine remains: `queued -> in_progress -> review_pending -> completed` plus terminal states.
  - Role-based actions (approve/retry/escalate/cancel) MUST emit a `run_state_changed` activity event.

## Non-Functional Requirements

- Performance:
  - Office scene updates must not block core dashboard interactions.
  - Activity events should be batch-applied on the client to avoid frame drops.
- Reliability:
  - Realtime service supports a replay window sufficient to hydrate dashboards after reconnect.
  - Clients tolerate temporary stream gaps by re-querying with `since`.
- Security/privacy:
  - Workspace-scoped authorization for all activity stream access and orchestration actions.
  - Activity payloads must avoid leaking sensitive data by default (extension redaction).
- Accessibility:
  - Reduced-motion mode provides equivalent meaning without animation.
  - High-contrast mode maintains state distinction for `info/warning/critical`.

## Observability Requirements

- Logs:
  - Correlation logging keyed by `correlation_id` across API, orchestration, and realtime.
- Metrics:
  - Event delivery latency (p50/p95) for activity stream.
  - Dropped/failed event deliveries and reconnect rates.
  - Client hydration duration (time to populate timeline/office scene after open/reconnect).
- Tracing:
  - Trace spans across command submission → orchestration processing → event broadcast.
- Alerts:
  - Stream freshness (no events delivered beyond threshold) per project/workspace.
  - Orchestration workflows stuck in `in_progress` or `review_pending` beyond SLA.

## Rollout / Rollback Constraints

- Rollout:
  - Introduce office scene as a gated feature flag in Nexus (Phase 1 static layout → Phase 2 animated cues).
  - Event schema changes require compatibility review + CRIT.
- Rollback:
  - Office scene can fall back to timeline-only mode without losing core functionality.
  - Realtime stream can degrade to polling (`/activity/stream`) under incident conditions.

## Validation Plan

- Validate correlation continuity for a workflow across all transitions.
- Validate reduced-motion mode preserves the meaning of: queued, in progress, review pending, completed, failed, cancelled.
- Validate replay hydration produces consistent office scene state after reconnect.

## Open Questions

- What is the minimum replay window needed for a “session” (minutes/hours)?
- Should office scene state be derived purely from event history, or also from a snapshot endpoint?

