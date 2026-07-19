# ADR-0005: Event-Driven Control Plane

## Status
Accepted

## Context
Deployments, policy checks, resource drift events, and audit logging happen asynchronously across many different accounts and regions. Coupling these flows synchronously results in poor responsiveness and timeouts.

## Decision
CPM will use an **Event-Driven Architecture** for its control plane, centered around **Amazon EventBridge**.
- All lifecycle phases (e.g., onboarding requested, deploy started, deploy succeeded, drift detected) will publish events to a central EventBus.
- Subsystems (e.g., notification engines, audit logs, billing calculators) will subscribe to events asynchronously.

## Consequences
- **Pros**:
  - Loose coupling between core orchestration logic and side-effect services (e.g., Slack notifications, compliance auditing).
  - High resilience and easy extension.
- **Cons**:
  - Debugging async event flows is more difficult than debugging synchronous request/response pipelines.
  - Event schemas must be strictly versioned and governed.
