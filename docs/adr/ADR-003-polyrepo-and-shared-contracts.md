# ADR-003: Polyrepo Portfolio + Shared Contracts Strategy

## Title

Polyrepo delivery with versioned shared contracts and packages

## Status

- Accepted

## Context

NueVue is currently in a docs-first phase, but the product is intended to ship as a multi-surface system:

- **NeXeZ**: the premium website + authenticated web app experience (office visualization + command center UX).
- **NuMuN platform services**: API + orchestration + realtime activity backbone that powers NeXeZ and other clients.
- **Clients**: browser extension and future IDE/terminal integrations.

To keep these surfaces buildable and releasable independently while remaining integratable, we need a shared-code and shared-contract approach that prevents drift:

- API contracts must remain compatible across versions.
- Event schemas/taxonomy must stay stable while expanding.
- UI clients must not embed service internals.

## Decision

Adopt a **polyrepo portfolio** by default, backed by **versioned shared contracts**.

1. **Separate repos by deployable surface**
   - Website and web app (NeXeZ) are separate deployables.
   - Platform services (NuMuN API / orchestration / realtime) are separate deployables.
   - Extension is a separate deployable.

2. **One shared contracts source of truth**
   - Maintain OpenAPI, JSON schemas, and taxonomy documents as the canonical interface.
   - Publish contracts as a versioned package (or a dedicated contracts repo) so all consumers pin versions.
   - Backwards-compatible changes are additive; breaking changes require explicit versioning and a CRIT.

3. **Shared libraries are optional; shared contracts are mandatory**
   - Shared UI components and utilities can exist, but contracts and IDs are the required integration primitive:
     - `correlation_id` across surfaces
     - stable `event_id` for dedupe and replay

4. **Integration stays testable**
   - When implementation begins, prefer contract-driven validation between repos (OpenAPI + event schema).

## Consequences

- Feature work must explicitly list which contracts/taxonomies it touches.
- Any cross-repo change that affects contracts or safety workflows is Tier 2 and requires ADR + CRIT.
- This repo remains the planning/spec anchor until code repos are introduced; it should track canonical contracts and the portfolio plan.

