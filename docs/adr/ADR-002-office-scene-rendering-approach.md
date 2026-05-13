# ADR-002: Office Scene Rendering Approach (Nexus)

## Title

Render the office scene with accessible DOM/SVG first, with an upgrade path

## Status

- Proposed

## Context

Nexus must visualize progress using an “office scene” metaphor:
- zones (planning/build/review/ops),
- agents as sprites,
- and social cues (handoffs, approvals, blockers, escalations).

The visualization must remain meaningful with reduced motion and must not degrade the usability of the command panel, board snapshot, and timeline.

We need a rendering approach that is:
- implementable early (docs-first → foundation build),
- accessible by default,
- and performance-safe for incremental animation.

## Decision

Use a **DOM/SVG-first approach**:

- Represent the office scene layout using semantic DOM + SVG for zones and routes.
- Implement motion as progressive enhancement:
  - Phase 1: static layout + subtle transitions
  - Phase 2: sprite presence + handoffs with limited animation primitives
  - Phase 3: richer cues if performance remains acceptable
- Treat reduced-motion mode as a first-class equivalent:
  - state changes use non-motion cues (position, color, iconography, labels)
  - all cues remain readable and screen-reader describable.

If event volume and animation complexity outgrow DOM/SVG performance, evaluate a move to Canvas/WebGL while keeping the same scene-state model.

## Alternatives Considered

- **Canvas/WebGL from day one**
  - Pros: high-performance animation, flexible effects.
  - Cons: higher complexity for accessibility and semantics; harder to iterate quickly.

- **Pure CSS/HTML without SVG**
  - Pros: simplest stack.
  - Cons: harder to represent paths/handoffs and spatial relationships cleanly.

- **Third-party game engine**
  - Pros: fast iteration on sprite animation.
  - Cons: heavier dependencies and tooling; increased integration risk before the product backbone exists.

## Consequences

- The office scene should have a clear “scene state” derived from activity events so rendering remains swappable.
- Accessibility constraints will shape the design system and motion rules (see PRD-06).
- Visual cues must remain mapped to real workflow state and review gates (avoid decorative animations).

## Follow-ups

- Define a minimal “scene state” schema (derived from `ActivityEvent`) to drive rendering.
- Document motion tokens and reduced-motion fallbacks in the design system work (PRD-06).

