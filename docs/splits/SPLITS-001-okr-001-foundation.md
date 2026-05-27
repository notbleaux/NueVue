# SPLITS-001: OKR-001 Foundation (Work Breakdown)

This document turns `OKR-001` into reviewable, vertically-sliced work units.

## Notes (Naming)

- **NeXeZ**: website + authenticated web app experience (includes Nexus).
- **Nexus**: the authenticated web app module (command center + office scene).
- **NuMuN**: platform services (API + orchestration + realtime) powering NeXeZ.

## Split A: Activity Backbone (Contracts + Replay Correctness)

- Scope:
  - Confirm activity taxonomy coverage for office cues (presence/handoff/approval/blocker/escalation)
  - Confirm event ordering + dedupe rules (`event_id`)
  - Define replay window + retention policy requirement
- Definition of done:
  - ADR-001 follow-ups answered (replay window, transport decision for Phase 2)
  - No contract-breaking changes to `ActivityEvent` schema
- Validation:
  - Documented examples of event sequences for a full workflow (`queued -> in_progress -> review_pending -> completed`)
- Rollback:
  - Keep existing schema and taxonomy; additions must be backwards-compatible only

## Split B: NeXeZ (Nexus) Office Scene Phase 1 (Static + Meaningful)

- Scope:
  - Static office scene layout (zones: planning/build/review/ops)
  - Mapping from lifecycle state → zone + cue
  - Reduced-motion equivalent rendering plan
- Definition of done:
  - ADR-002 accepted with concrete “Phase 1” constraints
  - PRD-01 office scene requirement is satisfied at a minimal viable level (static, meaningful)
- Validation:
  - Documented “state → cue” table and reduced-motion equivalence rules
- Rollback:
  - Feature-flag office scene; timeline remains primary UI

## Split C: NeXeZ (Nexus) Timeline + Filters (Operator Usability)

- Scope:
  - Timeline filters by role/severity/status/project
  - Correlation continuity display (`correlation_id`)
- Definition of done:
  - Timeline can be hydrated from replay (`since`) and can show cross-surface continuity
- Validation:
  - Example: extension submission → orchestration transitions share one `correlation_id`
- Rollback:
  - Filters can be reduced to role + severity without breaking core timeline

## Split D: Phase 2 (Push Delivery) Readiness (Design-Only)

- Scope:
  - Decide SSE vs WebSocket for push
  - Ensure replay remains authoritative correctness path
- Definition of done:
  - ADR-001 updated to reflect the chosen push transport
- Validation:
  - Document reconnect flow: push disconnect → replay catch-up → resume push
- Rollback:
  - Push remains optional; polling continues to work
