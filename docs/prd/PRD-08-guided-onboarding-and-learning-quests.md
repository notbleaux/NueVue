# PRD-08: Guided Onboarding + Learning Quests (In-App)

## Objective

Turn onboarding into an interactive, role-aligned experience inside Nexus so new users can learn the delivery workflow (plan → build → review → operate) with clear progression cues.

## Users

- New workspace owner
- New contributor
- Project manager learning the platform

## Core Functional Requirements

1. **Guided Onboarding Checklist**
   - Show a step-by-step onboarding path inside the web app
   - Track completion state per user/workspace

2. **Learning Quests**
   - Provide small “quests” that teach concepts:
     - creating workspaces/projects/milestones/tasks,
     - starting an orchestration run,
     - requesting review,
     - approving/retrying/escalating/cancelling,
     - reading release/health status
   - Each quest includes completion criteria and a short explanation of “why it matters”

3. **Role-Aligned Coaching**
   - Surface tips depending on the user’s role (planner/builder/reviewer/operator)
   - Require explicit confirmation for irreversible actions (operator guardrails)

4. **Progress Visualization**
   - Display quest progression in the office scene using meaningful cues (folders moved, stamps, alerts)
   - Emit activity events for quest milestones for timeline coherence

## Non-Functional Requirements

- No dark patterns: user retains control; quests are skippable
- Accessibility: supports reduced motion and screen readers
- Localization-ready quest content

## Acceptance Criteria

- A new user can complete a “first workflow” dry run without external documentation
- Quest milestones are visible in the timeline and office scene with correlation IDs
- Operators are guided into safe release/incident procedures with explicit confirmation gates

