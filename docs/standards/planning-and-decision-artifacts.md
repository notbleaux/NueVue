# Planning and Decision Artifacts (OKR, PRD, ARD, ADR, CRIT, Splits)

This document defines *what* planning/decision artifacts exist in NueVue and *when* they are required. The goal is to reduce ambiguity, keep decisions auditable, and make agent-driven execution predictable and easy to visualize in the Nexus office simulation.

## Canonical Naming (Use These Terms)

- **PixelOffice**: the inspiration and product philosophy (not a module name in this repo).
- **NueVue**: this repository/workspace program name.
- **Nexus**: the authenticated web app surface (dashboard + command center).
- **Command Hub API**: the backend API contract consumed by Nexus and the browser extension.
- **Office scene**: the visualization metaphor (zones + sprites) used by Nexus to show progress and social cues.

If a document needs to mention older or alternative names, define them once and then use the canonical terms for the rest of the document.

## Artifact Glossary

### OKR (Objectives and Key Results)
Defines outcome-level direction for a timebox (quarter/month/sprint).

Required fields:
- Objective (plain language)
- Key results (measurable, time-bound)
- Owner (human)
- Scope boundaries (explicit non-goals)
- Risks/assumptions

Template: `docs/standards/templates/OKR-template.md`

### PRD (Product Requirement Document)
Defines the product change: users, capabilities, acceptance criteria.

Template: existing PRDs in `docs/prd/`.

### ARD (Architecture Requirements Document)
Bridges PRD → architecture by turning product needs into engineering constraints and system requirements. Use ARD when a change affects architecture, contracts, reliability, or security.

Required fields:
- Scope and interfaces (services/modules impacted)
- Non-functional requirements (latency, reliability, security, privacy)
- Data and event requirements (schemas, taxonomy impacts)
- Observability requirements (logs/metrics/traces)
- Rollout and rollback constraints

Template: `docs/standards/templates/ARD-template.md`

### ADR (Architecture Decision Record)
Records a decision and its rationale so the team can move forward without re-litigating.

Use ADR when choosing:
- a storage/eventing approach,
- a service boundary,
- a contract/schema change strategy,
- an interaction model (agent roles, review gates),
- UI architecture (rendering approach, animation tech, accessibility tradeoffs).

Template: `docs/standards/templates/ADR-template.md`

### CRIT (Critical Review and Integration Track)
Structured review checkpoint to validate readiness before building (design critique) and before shipping (integration critique). CRIT is where “this is good enough to proceed” is explicitly stated.

CRIT is required at:
- Gate A exit (Foundation readiness)
- Any contract change (API or event schema)
- Any change that adds an irreversible action (delete, deploy, billing, credential use)

Template: `docs/standards/templates/CRIT-template.md`

### Splits (Work Splits)
Converts a PRD/ARD into trackable work units (milestones → tasks → subtasks) with clear acceptance criteria, ownership, and review expectations.

Rules:
- Every split task has: definition of done, test/validation note, rollback note (if applicable).
- Prefer vertical slices (thin end-to-end capability) over horizontal layers.
- Keep tasks small enough to review quickly; if a task needs more than ~1–2 focused PRs, split again.

## Required Flow (Before Actioning)

1. OKR created (or referenced) for the goal.
2. PRD written/updated for the user-facing change.
3. ARD written if architecture/contracts are impacted.
4. ADR written for any key decision with alternatives/tradeoffs.
5. CRIT held to approve the approach and constraints.
6. Splits created with acceptance criteria and role assignment.
7. Implementation proceeds with the Planner/Builder/Reviewer/Operator loop.

## Minimum Artifact Set (Avoid Over-Processing)

Not all work needs all artifacts. Use the smallest set that preserves clarity and safety.

### ADR/CRIT Threshold Rules (Quick Check)

ADR is **required** when a change includes a decision that would be costly to reverse or re-litigate later, including:
- choosing between viable alternatives (e.g., SSE vs WebSocket, DOM/SVG vs Canvas),
- introducing a new service boundary or dependency with operational tradeoffs,
- changing contract/schema strategy (even if backwards-compatible),
- adopting a new safety/review gate or irreversible action pattern.

CRIT is **required** when the work is Tier 2, crosses a contract boundary, or changes a safety-critical workflow (auth, deploy/rollback, incident actions, billing, credential use). For Tier 1 work, CRIT is optional and should be used when risk or ambiguity is high.

### Tier 0: Low-Risk / Trivial Change

Examples: typo fixes, rewording, small formatting changes, purely internal refactors with no behavior change.

Required:
- None beyond the change itself.

### Tier 1: Standard Feature Work (Within Existing Boundaries)

Examples: new UI panel behavior, new non-breaking endpoint, small workflow tweak that does not change contracts/schemas.

Required:
- PRD (new or updated)
- Splits (task breakdown + definition of done)

Optional (recommended when the choice is non-obvious):
- ADR (if there is a meaningful tradeoff or alternative)
- CRIT (design CRIT when risk is unclear)

### Tier 2: Architecture / Contract / Safety Work

Examples: any API/event schema change, new service boundary, auth/authz changes, irreversible actions, release/incident workflow changes.

Required:
- PRD
- ARD
- ADR (for the key decision points)
- CRIT (design CRIT before build, integration CRIT before ship)
- Splits

## Agent + Surface Model (IDE, Terminal, Chat)

NueVue’s “office” visualization works best when all interaction surfaces emit the same activity model:
- **IDE**: code actions, edits, test runs, PR creation (Builder/Reviewer heavy).
- **Terminal**: task execution, scripts, builds, migrations, incident actions (Builder/Operator heavy).
- **Chat** (Nexus): planning, clarifications, approvals, CRIT decisions (Planner/Reviewer heavy).

Guideline: every meaningful state change should map to an activity event with a `correlation_id` so the UI can animate progress across surfaces without losing continuity.

## Office Visualization Mapping (Recommended)

Represent work as an animated office with social cues that reflect real delivery stages (not decoration):
- **Zones**: Planning (OKR/PRD), Architecture (ARD/ADR), Build (implementation), Review (CRIT/PR review), Ops (release/incident).
- **Cues**: presence (who is “at” a task), handoffs (agent walks documents between zones), approvals (stamp animation), blockers (red folder/alert), escalations (manager NPC).
- **Progress**: visible WIP limits per zone, queue visualization for `queued -> in_progress -> review_pending -> completed`.

If animation is too heavy early on, start with a static office layout + subtle transitions, then layer richer animation later.
