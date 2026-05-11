# PRD-04: Docs and Operations (Onboarding, Runbooks, Release Process)

## Objective

Ensure architecture, operations, and release practices remain documented and executable through foundation and early access launch cycles.

## Required Documentation

- Architecture overview
- API contracts and event taxonomy
- Role-based operating model (Planner, Builder, Reviewer, Operator)
- Incident and patch runbook
- Early-access onboarding guide

## Operational Requirements

- Continuous patching cadence during active development cycles
- Regression checks per service update
- Release notes for every deployment
- Rollback criteria and procedures for every release tier
- Documentation updates in the same cycle as service/API changes

## Acceptance Criteria

- All required docs are discoverable from one index
- Incident and patch response steps are actionable by operators
- Every release stage includes explicit go/no-go criteria
