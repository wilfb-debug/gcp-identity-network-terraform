nano observability/alerting-notes.md
# Alerting Notes

## Alerting Design

This project uses log-based alerting instead of VM-level metrics.

### Why log-based alerts?
- Works even when applications are lightweight
- No agents required
- Tied directly to application behavior

### Alert trigger
- Logs containing `STEP3_TEST`
- Resource: private VM only
- Alert fires when log count > 0

### Purpose
This validates:
- Logs are ingested correctly
- Monitoring is identity-aware
- Alerts can be triggered without public exposure

## Why the metric-based alert may not email immediately
- Log-based metrics can take time to emit Monitoring time series after creation.
- Threshold configuration must match how the metric reports values.
- The metric filter must match the exact log field and message content.

## Recommended approach for this lab
Use a log-based alert policy:
- Filter: match `jsonPayload.message:("STEP3_TEST")`
- Condition: matched log entries > 0
- Notification: email (or SMS if needed)

This is the most direct way to confirm end-to-end observability.
