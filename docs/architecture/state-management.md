# State Management

| Field | Value |
|--------|-------|
| Project | Cloud Platform Manager (CPM) |
| Version | 1.0 |
| Status | Draft |
| Owner | Platform Engineering Team |

---

# 1. Purpose

This document defines the state management architecture for Cloud Platform Manager (CPM).

CPM maintains its own platform state independently of Terraform. While Terraform tracks infrastructure resources, CPM tracks the operational lifecycle of packages and components.

The platform state enables deployment orchestration, lifecycle management, health monitoring, upgrades, rollbacks, and operational visibility.

---

# 2. Objectives

The State Management system is designed to:

- Maintain a single source of truth for deployed components
- Track deployment lifecycle and operational status
- Support upgrades and rollbacks
- Record deployment history
- Enable health monitoring
- Provide reliable state recovery
- Support future scalability

---

# 3. Design Principles

The State Management system follows these principles:

- Single source of truth
- Consistent state transitions
- High availability
- Idempotent updates
- Event-driven synchronization
- Minimal operational overhead

---

# 4. Terraform State vs CPM State

Terraform and CPM manage different types of state.

| Terraform State | CPM State |
|-----------------|-----------|
| Infrastructure resources | Platform components |
| Resource attributes | Component lifecycle |
| Resource dependencies | Package and component status |
| Infrastructure configuration | Deployment metadata |
| Managed by Terraform | Managed by CPM |

Terraform remains responsible for infrastructure provisioning.

CPM remains responsible for platform lifecycle management.

---

# 5. State Architecture

```
                    CPM Orchestrator
                            │
                            ▼
                    State Manager
                            │
                            ▼
                       Amazon DynamoDB
                            │
                            ▼
                  Platform Deployment State
```

The Orchestrator updates the state after every lifecycle operation.

---

# 6. State Store

CPM uses Amazon DynamoDB as the platform state store.

Reasons for choosing DynamoDB include:

- Fully managed
- High availability
- Low operational overhead
- Millisecond latency
- Native AWS integration
- Automatic scaling

Terraform state is intentionally stored separately and is not replaced by CPM.

---

# 7. State Model

Each deployed component maintains a state record.

Example:

```yaml
component: iam

package: security

environment: dev

accountId: 123456789012

version: 1.2.0

status: Healthy

health: Passed

lastDeployment: 2026-07-20T10:30:00Z

lastUpdated: 2026-07-20T10:35:00Z

operation: Install
```

The exact implementation may evolve, but every state record must contain sufficient information to determine the current lifecycle status of a deployed component.

---

# 8. Component States

A component may exist in one of the following states.

| State | Description |
|--------|-------------|
| Registered | Component is available for deployment |
| Deploying | Deployment is in progress |
| Validating | Health validation is running |
| Healthy | Deployment completed successfully |
| Upgrading | Component upgrade is in progress |
| Rolling Back | Rollback is executing |
| Failed | Deployment failed |
| Retired | Component has been removed |

Only one lifecycle state may be active at a time.

---

# 9. State Transitions

The normal lifecycle follows the sequence below.

```
Registered
      │
      ▼
Deploying
      │
      ▼
Validating
      │
      ▼
Healthy
```

If an operation fails:

```
Deploying
      │
      ▼
Failed
      │
      ▼
Rolling Back
      │
      ▼
Healthy
```

State transitions are managed exclusively by the CPM Orchestrator.

---

# 10. State Updates

The state is updated after every lifecycle operation.

Examples include:

- Component installation
- Package installation
- Upgrade completion
- Rollback completion
- Health validation
- Component retirement

Direct modification of platform state outside the Orchestrator is not supported.

---

# 11. Deployment History

CPM records deployment history for operational visibility.

Examples include:

- Deployment timestamp
- Operation type
- Target version
- Deployment result
- Error information (if applicable)

Historical information supports troubleshooting and future audit requirements.

---

# 12. Health Tracking

Component health is tracked independently from deployment status.

Examples of health indicators include:

- Healthy
- Warning
- Unhealthy

Health is updated after validation and may be refreshed during future health checks.

---

# 13. Consistency

CPM follows an eventual consistency model.

The Orchestrator updates the state only after lifecycle operations complete successfully.

If an operation fails, the recorded state reflects the last known valid condition until recovery or rollback is completed.

---

# 14. Recovery

If the Orchestrator is interrupted during deployment, the persisted state enables recovery.

Recovery actions may include:

- Resume deployment
- Retry validation
- Initiate rollback
- Mark deployment as failed

Recovery behavior ensures that platform state remains consistent with completed lifecycle operations.

---

# 15. Security

Platform state may contain operational metadata.

The state store should be protected using:

- IAM least-privilege access
- Encryption at rest
- Encryption in transit
- Audit logging

Sensitive values such as passwords, secrets, or credentials must never be stored in the platform state.

Secrets should be managed using AWS Secrets Manager or AWS Systems Manager Parameter Store.

---

# 16. Future Enhancements

Future versions of CPM may extend state management with:

- State versioning
- Multi-account state aggregation
- Advanced querying
- Drift detection
- Historical analytics
- Dashboard visualization

These enhancements are outside the scope of CPM v1.

---

# 17. Summary

The State Management system provides the operational source of truth for Cloud Platform Manager.

By separating platform state from Terraform state, CPM can reliably manage deployments, upgrades, rollbacks, health monitoring, and lifecycle operations while maintaining a clear separation between infrastructure provisioning and platform orchestration.