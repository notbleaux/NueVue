# Planning and Decision Artifacts (OKR, PRD, ARD, ADR, CRIT, Splits)

This document defines *what* planning/decision artifacts exist in NueVue and *when* they are required. The goal is to reduce ambiguity, keep decisions auditable, and make agent-driven execution predictable and easy to visualize in the Nexus office simulation.

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

## Agent + Surface Model (IDE, Terminal, Chat)

NueVue’s “office” visualization works best when all interaction surfaces emit the same activity model:
- **IDE**: code actions, edits, test runs, PR creation (Builder/Reviewer heavy).
- **Terminal**: task execution, scripts, builds, migrations, incident actions (Builder/Operator heavy).
- **Chat** (Nexus): planning, clarifications, approvals, CRIT decisions (Planner/Reviewer heavy).

Guideline: every meaningful state change should map to an activity event with a `correlation_id` so the UI can animate progress across surfaces without losing continuity.

## Office Visualization Mapping (Recommended)

Represent work as an animated office with social cues that reflect real delivery stages (not decoration):
- **Rooms**: Planning (OKR/PRD), Architecture (ARD/ADR), Build Bay (implementation), Review Desk (CRIT/PR review), Ops War Room (release/incident).
- **Cues**: presence (who is “at” a task), handoffs (agent walks documents between rooms), approvals (stamp animation), blockers (red folder/alert), escalations (manager NPC).
- **Progress**: visible WIP limits per room, queue visualization for `queued -> in_progress -> review_pending -> completed`.

If animation is too heavy early on, start with a static office layout + subtle transitions, then layer richer animation later.

