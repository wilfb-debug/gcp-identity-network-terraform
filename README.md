# Identity-First Cloud Network (Terraform) + Observability

This project builds an identity-first networking pattern on Google Cloud using Terraform, then validates telemetry (logs) from a 
private VM and sets up alerting.

## What this demonstrates
- Private VM access via IAP (no public IP required)
- IAM-first approach (least privilege)
- Centralized logging (Cloud Logging)
- Log-based metric + alerting (Cloud Monitoring)

## Architecture (high level)
- VPC + subnets (private workload subnet)
- Private VM (no public IP)
- IAP TCP forwarding to SSH into the VM
- Cloud Logging ingests syslog/app logs from the VM
- Log-based metric counts matching events (STEP3_TEST)
- Cloud Monitoring alert notifies when threshold is met

## Validation evidence
- Logs appear in Cloud Logging under `jsonPayload.message`
- Filter used: see `observability/log-filter.txt`
- Metric created: `step3_test_count` (log-based metric)
- Alert policy created: `TEST ALERT`

## Repo structure
- `terraform/` - Terraform IaC
- `architecture/` - architecture diagrams and write-ups
- `observability/` - log filter, metric + alert notes
- `screenshots/` - screenshots as proof/evidence
