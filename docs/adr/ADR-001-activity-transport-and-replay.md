# ADR-001: Activity Transport and Replay Strategy

## Title

Activity transport and replay for Nexus office scene + timeline

## Status

- Proposed

## Context

Nexus needs near-real-time activity to drive:
- the timeline feed, and
- the office scene visualization (presence, handoffs, approvals, blockers).

The repository already defines:
- an activity event schema (`docs/api/activity-event-schema.json`),
- a taxonomy (`docs/api/activity-taxonomy.md`),
- a query endpoint (`GET /activity/stream`) with an optional `since` cursor (`docs/api/command-hub-openapi.yaml`),
- a Realtime Service that “fans out” activity streams (`docs/architecture/platform-services-technical-design.md`).

We need a transport plan that is reliable, replayable after reconnect, and easy to validate early, while remaining compatible with a richer realtime implementation later.

## Decision

Adopt a phased activity delivery strategy:

1. **Phase 1 (Foundation): HTTP replay + polling**
   - Use `GET /activity/stream?project_id=...&since=...` for:
     - initial hydration (no `since` or `since` = last known cursor),
     - reconnect recovery (use last seen `timestamp`),
     - periodic polling for updates.
   - The UI deduplicates events by `event_id` and preserves ordering by (`timestamp`, `event_id`).

2. **Phase 2 (Internal Beta): push delivery via Realtime Service**
   - Add a push channel (SSE or WebSocket) that streams the same `ActivityEvent` objects.
   - Push is best-effort; replay via `GET /activity/stream` remains the correctness path.

3. **Phase 3 (Early Access Live): snapshot + stream (optional)**
   - If event volume or hydration time requires it, add a snapshot endpoint to seed the office-scene state quickly, then apply stream deltas.

## Alternatives Considered

- **WebSocket-only realtime**
  - Pros: lowest latency, bidirectional.
  - Cons: reconnect correctness is harder without a first-class replay path; more operational complexity early.

- **SSE-only realtime**
  - Pros: simple server → client streaming, works well for timelines.
  - Cons: still requires replay for reconnect; some environments need careful proxy configuration.

- **Polling-only (no realtime service)**
  - Pros: simplest operationally.
  - Cons: higher perceived latency and wasted requests; less “alive” office scene experience.

## Consequences

- Nexus must treat replay as authoritative and push as opportunistic.
- Contracts must keep `event_id` stable and always include `correlation_id` for cross-surface continuity.
- Realtime Service can be introduced without changing the event model (only the transport).

## Follow-ups

- Define the minimum replay window and retention policy (referenced in `docs/ard/ARD-001-nexus-office-scene-and-activity-backbone.md`).
- Decide whether push transport is SSE or WebSocket for Phase 2.

