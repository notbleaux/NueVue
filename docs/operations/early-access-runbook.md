# Early Access Runbook

## Purpose

Define operating procedure for live early access while active development and patching continue.

## Daily Operations

1. Check command hub service health (`/services/health`)
2. Review critical activity events from `/activity/stream`
3. Validate launch rail status (`/releases/status`)
4. Confirm no stale realtime streams or blocked workflow runs

## Incident Response

1. Detect from alerting or critical events
2. Assign operator owner and open incident event
3. Triage impact scope (workspace, project, service)
4. Mitigate (retry/escalate/cancel and patch as needed)
5. Verify recovery with health and activity checks
6. Publish incident summary and follow-up tasks

## Patch Procedure

1. Scope fix and affected services
2. Run regression checklist for changed surface
3. Deploy patch with release note
4. Monitor activity and error rates for 30 minutes minimum
5. Trigger rollback if thresholds are exceeded

## Rollback Triggers

- Service status degrades to `down`
- Error budget burn exceeds configured threshold
- Workflow completion latency exceeds SLO for sustained window
