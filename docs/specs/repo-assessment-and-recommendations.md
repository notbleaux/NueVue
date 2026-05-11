# Repo Assessment and Recommendations (Docs-First Phase)

This repo is currently in a **docs-first** stage: it establishes product intent, PRDs, architecture direction, and operational expectations before implementation is scaffolded.

## What’s Working Well

- Single index (`docs/specs/INDEX.md`) makes core docs discoverable.
- PRDs cover the three major surfaces (web app, platform services, extension) plus docs/ops.
- Architecture and operations docs define staged delivery (launch gates) and release discipline.
- Activity taxonomy + event schema provide a workable baseline for live visualization.

## Gaps / Problems

- **No explicit “before actioning” flow** connecting OKRs → PRDs → ARD/ADR → CRIT → Splits.
- **No templates** in-repo for OKR/ARD/ADR/CRIT, which increases variance and rework.
- **Office visualization requirements** (animated, social cues, multi-surface coherence) were implied in intent but not explicitly captured in a PRD requirement until now.
- **Event taxonomy is lifecycle-focused**; it will likely need additional action types as planning and review artifacts become first-class events.
- **Repo scaffold is not present** yet (no `apps/`, `services/`, `packages/`, build/test tooling). That is fine for docs-first, but it blocks execution unless a clear handoff point is defined.

## Recommendations (Concrete Next Steps)

1. Adopt `docs/standards/planning-and-decision-artifacts.md` as the “before actioning” checklist for any work that affects architecture/contracts/reliability.
2. Start using templates in `docs/standards/templates/` immediately (even before code exists) for:
   - an initial OKR,
   - the first ARD for the Nexus office visualization + activity stream integration,
   - ADRs for key early architectural choices (event bus, storage, animation/rendering approach),
   - CRIT checkpoints at each launch gate.
3. Extend `docs/api/activity-taxonomy.md` when planning/review artifacts need to be visible in the office UI (keep backwards-compatibility).
4. For the office visualization, implement in phases:
   - Phase 1: static office layout + subtle transitions + strong information hierarchy
   - Phase 2: sprite presence + handoff animations tied to correlation IDs
   - Phase 3: richer social cues (WIP limits, escalations, approvals) and accessibility refinements
5. Define the scaffold “go” point (Gate A exit) where repo structure and baseline build/test tooling are introduced (per the onboarding standards).

## Alternatives (If You Want Less Process)

- Replace ARD with a single “Architecture Notes” section inside each PRD until the first contract boundary is introduced.
- Replace CRIT with lightweight RFC review comments in the PRD/ADR, but keep a clear “approved to proceed” marker.

