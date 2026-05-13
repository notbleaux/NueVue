# CRIT-001: Foundation Design CRIT (Office Scene + Activity Backbone)

## What Is Being Reviewed

Foundation design for the Nexus office scene visualization and the activity transport/replay backbone that powers it.

## Stage

- Design CRIT (before build)

## Inputs

- OKR: `docs/okr/OKR-001-foundation.md`
- PRDs:
  - `docs/prd/PRD-01-nexus-web-app.md`
  - `docs/prd/PRD-02-platform-services.md`
  - `docs/prd/PRD-03-browser-extension.md`
  - `docs/prd/PRD-06-design-system-and-visualization-kit.md`
  - `docs/prd/PRD-08-guided-onboarding-and-learning-quests.md`
- ARD:
  - `docs/ard/ARD-001-nexus-office-scene-and-activity-backbone.md`
- ADRs:
  - `docs/adr/ADR-001-activity-transport-and-replay.md`
  - `docs/adr/ADR-002-office-scene-rendering-approach.md`

## Checklist

- Requirements are clear and testable
- Scope boundaries are explicit
- Contracts/schemas have compatibility plan
- Risks and mitigations documented
- Rollout/rollback plan exists
- Ownership and review gates are assigned

## Decision

- Approved with changes

## Notes

- Define the minimum replay window and retention policy for activity events (Phase 1 correctness requirement).
- Confirm Phase 2 push transport choice (SSE vs WebSocket) without changing the event model.
- Keep the office scene DOM/SVG-first with reduced-motion equivalence as a non-negotiable acceptance constraint.

