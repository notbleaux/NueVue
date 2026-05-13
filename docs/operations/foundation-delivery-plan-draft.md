# Foundation Delivery Plan (Draft): NeXeZ + NuMuN Polyrepo

This is a draft continuation plan after the current docs-first phase. It is designed to keep NeXeZ (web surfaces) and NuMuN (platform services) aligned as independent vertical slices that integrate cleanly over time.

## Guiding Decisions (Confirmed)

- Build a unified platform aligned with the PixelOffice-inspired target, then expand with NueVue-specific needs.
- Use **REST** contracts as the baseline API surface.
- Use **PixiJS** as the preferred path for richer office-scene rendering when DOM/SVG is insufficient, while preserving reduced-motion equivalence.
- Use **Docker Compose** for local multi-service development.
- Baseline deployment targets: **Vercel** (NeXeZ surfaces) + **Railway/Render** (NuMuN services).
- Use a **simplified ADR** format and keep decisions lightweight and auditable.

## Portfolio Integration Rules

- Shared contracts are the integration primitive (OpenAPI + JSON schema + taxonomy).
- `correlation_id` is mandatory across surfaces; replay remains authoritative for correctness.
- Backwards-compatible changes are additive; breaking changes require explicit versioning and CRIT review.

## Must Haves vs Nice to Haves

Use `docs/standards/component-prioritization-scorecard.md` to score components (1–5) across 13 questions, then classify:

- **Must Haves**: complete in the first waves before expanding experimentation.
- **Nice to Haves**: order by utility vs cost/risk and harden progressively without destabilizing live usage.

## Early Sprints (Draft Targets)

### Sprint 0: Portfolio Scaffold + Contracts

- Establish polyrepo boundaries (NeXeZ surfaces, NuMuN services, shared contracts).
- Publish initial versioned contracts (OpenAPI + activity event schema + taxonomy).
- Define local dev baseline (Docker Compose plan) and deployment targets (Vercel + Railway/Render).

### Sprint 1: Activity Backbone (Replay-First Correctness)

- Implement `GET /activity/stream` replay hydration as the correctness path (ordering + dedupe rules).
- Define replay window + retention policy and acceptance constraints.
- Ensure traceability via `correlation_id` across command submission → orchestration transitions → activity stream.

### Sprint 2: NeXeZ Web App Shell (Nexus)

- Build the command-center shell with timeline + filters backed by replay.
- Add reduced-motion/high-contrast modes with “meaning preserved” constraints.

### Sprint 3: Office Scene Phase 1 (Meaningful, Not Decorative)

- DOM/SVG baseline office layout (zones: planning/build/review/ops).
- Document state → cue mapping and reduced-motion equivalents.

### Sprint 4: Command Safety and Release Discipline

- Idempotency keys for write operations and safe retries.
- Health + release status endpoints surfaced in the NeXeZ dashboard.
- Patch + rollback workflow validated against the runbook.

## Phase Plan (After Foundation)

- **Internal Beta**: add push delivery (SSE/WebSocket) without changing the event model; keep replay authoritative.
- **Early Access Live**: harden release gates, incident ops, and contract compatibility checks across repos.
- **Later experiments**: incubate SATOR-inspired framework exploration after core platform stability is proven.

