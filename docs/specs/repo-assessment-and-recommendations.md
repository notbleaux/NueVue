# Repo Assessment and Recommendations (Docs-First Phase)

This repo is currently in a **docs-first** stage: it establishes product intent, PRDs, architecture direction, and operational expectations before implementation is scaffolded.

## Current Strategic Alignment (NeXeZ + NuMuN Polyrepo)

The current portfolio direction is:

- **NeXeZ**: premium website + authenticated web app experience (Nexus) as the user-facing command center and visualization surface.
- **NuMuN platform services**: unified backend systems (API + orchestration + realtime) that power NeXeZ and other clients.
- **Shared contracts**: versioned OpenAPI + JSON schema + taxonomy are the integration primitive across repos.

This is recorded as an accepted decision in `docs/adr/ADR-003-polyrepo-and-shared-contracts.md`.

## What’s Working Well

- Single index (`docs/specs/INDEX.md`) makes core docs discoverable.
- PRDs cover the three major surfaces (web app, platform services, extension) plus docs/ops.
- Architecture and operations docs define staged delivery (launch gates) and release discipline.
- Activity taxonomy + event schema provide a workable baseline for live visualization.
- “Before actioning” artifacts now exist (standard + templates + initial instances) and are linked from the index.

## Remaining Gaps / Risks

- **Artifact adoption risk**: OKR/ARD/ADR/CRIT/Splits exist, but they must be used consistently (especially for Tier 2 contract/safety work) or the process will drift.
- **Office visualization scope risk**: the office scene requirement is now explicit, but it needs a phased definition of “meaningful” vs “decorative” cues with reduced-motion equivalence.
- **Event taxonomy is lifecycle-focused**; it will likely need additional action types as planning and review artifacts become first-class events.
- **Execution scaffold is not present** yet (no polyrepo repos and no shared-contract packaging/release plan). That is fine for docs-first, but it blocks implementation until a clear handoff point is defined.

## Recommendations (Concrete Next Steps)

1. Adopt `docs/standards/planning-and-decision-artifacts.md` as the “before actioning” checklist for any work that affects architecture/contracts/reliability.
2. Use the initial artifacts already created as the baseline for Gate A work:
   - `docs/okr/OKR-001-foundation.md`
   - `docs/ard/ARD-001-nexus-office-scene-and-activity-backbone.md`
   - `docs/adr/ADR-001-activity-transport-and-replay.md`
   - `docs/adr/ADR-002-office-scene-rendering-approach.md`
   - `docs/crit/CRIT-001-foundation-design.md`
   - `docs/splits/SPLITS-001-okr-001-foundation.md`
3. Extend `docs/api/activity-taxonomy.md` when planning/review artifacts need to be visible in the office UI (keep backwards-compatibility).
4. For the office visualization, implement in phases:
   - Phase 1: static office layout + subtle transitions + strong information hierarchy
   - Phase 2: sprite presence + handoff animations tied to correlation IDs
   - Phase 3: richer social cues (WIP limits, escalations, approvals) and accessibility refinements
5. Define the scaffold “go” point (Gate A exit) where repo structure and baseline build/test tooling are introduced (per the onboarding standards), and record it as an ADR when chosen.

## Short-Term Actionable Tasks (Next Planning Sessions)

These are designed to be completed quickly and unblock Sprint 0–1 planning in `docs/operations/foundation-delivery-plan-draft.md`.

1. **Define replay window + retention policy** (ADR-001 follow-up)
   - Output: add concrete “minimum replay window” and a retention target to `docs/adr/ADR-001-activity-transport-and-replay.md`.
2. **Choose Phase 2 push transport (SSE vs WebSocket)** (ADR-001 follow-up)
   - Output: update ADR-001 with the chosen transport and reconnect correctness flow.
3. **Define a minimal “scene state” schema** (ADR-002 follow-up)
   - Output: a small schema (derived from `ActivityEvent`) that can drive DOM/SVG Phase 1 and PixiJS later without changing event contracts.
4. **Decide how shared contracts are versioned and consumed**
   - Output: a short appendix in `docs/adr/ADR-003-polyrepo-and-shared-contracts.md` describing “contracts repo vs package” and a recommended versioning scheme.
5. **Run the scorecard on the first wave components**
   - Output: fill a 1–5 scorecard for (a) Activity Backbone, (b) NeXeZ web app shell, (c) Office scene Phase 1, and record the Must Have/Nice to Have classification.

## Alternatives (If You Want Less Process)

- Replace ARD with a single “Architecture Notes” section inside each PRD until the first contract boundary is introduced.
- Replace CRIT with lightweight RFC review comments in the PRD/ADR, but keep a clear “approved to proceed” marker.
