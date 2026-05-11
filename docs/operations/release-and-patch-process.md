# Release and Patch Process

## Cadence

- Foundation stage: weekly release cycle
- Internal beta: twice-weekly release cycle
- Early access live: scheduled release cycle + emergency patch lane

## Required Checks Per Release

1. API contract compatibility review
2. Regression checks for touched services
3. Health endpoint verification
4. Updated release notes
5. Rollback plan attached

## Change Control

- Every deployment includes a release identifier
- Every command/action-impacting change must include idempotency validation
- Every API or event schema change must update docs in same cycle

## Go/No-Go Criteria

- **Go**: no critical unresolved incidents, SLOs within threshold, regression checks pass
- **No-Go**: critical issue open, rollback path unverified, unresolved contract incompatibility
