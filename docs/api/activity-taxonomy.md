# Activity Taxonomy

## Roles

- `planner`
- `builder`
- `reviewer`
- `operator`

## Action Types

- `task_created`
- `run_started`
- `run_state_changed`
- `review_requested`
- `review_approved`
- `retry_requested`
- `escalation_requested`
- `run_cancelled`
- `patch_deployed`
- `incident_opened`
- `incident_resolved`

## Status Values

- `queued`
- `in_progress`
- `review_pending`
- `completed`
- `failed`
- `cancelled`

## Severity Values

- `info`
- `warning`
- `critical`

## Correlation Rules

- Every command action must include a `correlation_id`
- All downstream events from that command must reuse the same `correlation_id`
- Cross-service tracing should key on (`correlation_id`, `event_id`)
