# Launch Gates and Risk Controls

## Gate A: Foundation

Required:

- Core Command Hub APIs published and versioned
- Orchestration state machine operational
- Nexus homepage shell with command panel and board snapshot
- Documentation baseline complete (PRDs, architecture, API contracts)

Exit checks:

- Contract validation for core APIs
- Baseline health endpoints available

## Gate B: Internal Beta

Required:

- Realtime activity stream active in Nexus timeline
- Role-based workflow actions enabled (approve/retry/escalate/cancel)
- Patch pipeline and regression checklist active

Exit checks:

- End-to-end workflow validation across all role transitions
- Alerting for failed workflows and stale streams enabled

## Gate C: Early Access Live

Required:

- Monitoring dashboards and on-call runbook in use
- Controlled rollout policy active
- Release notes and rollback criteria enforced for each deployment

Exit checks:

- Error budgets defined and tracked
- Incident response exercises completed

## Risk Controls

- Contract tests between Nexus and APIs
- Idempotent command processing
- Retry plus dead-letter handling in orchestration
- Stream freshness alerting
- Documentation-update requirement in same cycle as API/service changes
