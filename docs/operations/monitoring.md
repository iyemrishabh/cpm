# Monitoring & Alerting

This document outlines the observability strategy, metrics, and alerting thresholds for CPM.

## Observability Pillars

### 1. Metrics (Prometheus / CloudWatch)
We track standard golden signals:
- **Latency**: Time taken to service requests.
- **Traffic**: A measure of demand (requests per second).
- **Errors**: Rate of requests that fail.
- **Saturation**: Resource utilization (CPU, memory, disk).

### 2. Logs
- Logs are output in structured JSON format to stdout.
- Log aggregator: *[e.g., Datadog / ELK Stack]*

### 3. Traces (APM)
- Distributed tracing is enabled for all inter-service requests using *[e.g., OpenTelemetry]*.

---

## Alerting Thresholds

| Metric | Condition | Severity | Action |
| ------ | --------- | -------- | ------ |
| CPU Utilization | > 85% for 5m | Warning | Auto-scale triggered |
| Error Rate (5xx) | > 2% for 2m | Critical | Page on-call team |
| Disk Free Space | < 10% | Warning | Open ticket |
