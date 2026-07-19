# Glossary

| Field | Value |
|--------|-------|
| Project | Cloud Platform Manager (CPM) |
| Version | 1.0 |
| Status | Draft |
| Owner | Platform Engineering Team |

---

# 1. Overview

This glossary defines the terminology used throughout the Cloud Platform Manager (CPM) project.

The purpose of this document is to ensure consistent understanding of concepts, components, and architectural terms used across documentation, implementation, and discussions.

---

# 2. Terms

## AWS Account

An isolated AWS environment used to host workloads, platform services, or shared infrastructure.

---

## Bootstrap

The process of preparing a newly created AWS account for platform deployment.

Typical bootstrap activities include:

- Creating deployment IAM roles
- Configuring Terraform backend
- Setting up GitHub OIDC
- Creating required S3 buckets
- Creating DynamoDB tables
- Configuring KMS keys

Bootstrap is performed only once for an account.

---

## Component

A modular platform capability that provides a specific function.

Examples:

- IAM
- Networking
- Monitoring
- EventBridge
- Lambda
- Governance

Each component is independently deployable and versioned.

---

## Component Registry

A catalog containing metadata about all platform components, including their versions, dependencies, and deployment status.

---

## Control Plane

The centralized system responsible for managing the lifecycle of platform components.

CPM acts as the control plane.

---

## Data Plane

The AWS resources and services deployed and managed by CPM.

Examples:

- VPC
- IAM Roles
- Lambda Functions
- CloudWatch Alarms

---

## Deployment

The process of installing or updating one or more platform components in an AWS account.

---

## Drift Detection

The process of identifying differences between the desired infrastructure configuration and the actual deployed infrastructure.

---

## Event

A significant occurrence that triggers a platform workflow.

Examples:

- New account registered
- Deployment completed
- Deployment failed
- Upgrade requested

---

## Event-Driven Architecture

An architectural style where workflows are initiated by events rather than manual execution.

---

## Governance

Processes and controls that ensure AWS environments comply with organizational policies and standards.

---

## Infrastructure as Code (IaC)

Managing infrastructure through declarative configuration files rather than manual actions.

Terraform is the primary IaC tool used by CPM.

---

## Lifecycle

The complete operational journey of a platform component.

Typical stages include:

- Install
- Configure
- Upgrade
- Monitor
- Rollback
- Retire

---

## Multi-Account

An AWS architecture where infrastructure is distributed across multiple AWS accounts.

---

## Observability

The ability to understand the internal state of the platform through logs, metrics, traces, and events.

---

## Orchestrator

The CPM service responsible for coordinating deployments, upgrades, retries, and rollback across platform components.

---

## Platform Component

A reusable building block that delivers a specific platform capability.

Examples include:

- IAM
- Monitoring
- Networking
- Security
- FinOps

---

## Platform Lifecycle Management

The process of managing platform components from initial deployment through upgrades, monitoring, rollback, and retirement.

---

## Rollback

Restoring a platform component to a previously known stable version after a failed deployment or upgrade.

---

## State

The current recorded status of a deployment or platform component.

Examples:

- Pending
- Running
- Successful
- Failed
- Rolled Back

---

## Terraform

An Infrastructure as Code tool used to provision and manage AWS infrastructure.

CPM orchestrates Terraform but does not replace it.

---

## Version

A numbered release of a platform component.

CPM follows Semantic Versioning.

Example:

```
1.2.0
```

---

## Workflow

A sequence of automated tasks executed to achieve a platform operation.

Examples:

- Bootstrap Workflow
- Deployment Workflow
- Upgrade Workflow
- Rollback Workflow

---

# 3. Acronyms

| Acronym | Meaning |
|----------|---------|
| ADR | Architecture Decision Record |
| API | Application Programming Interface |
| AWS | Amazon Web Services |
| CI/CD | Continuous Integration / Continuous Delivery |
| CPM | Cloud Platform Manager |
| ECS | Elastic Container Service |
| IAM | Identity and Access Management |
| IaC | Infrastructure as Code |
| KMS | Key Management Service |
| OIDC | OpenID Connect |
| PRD | Product Requirements Document |
| REST | Representational State Transfer |
| S3 | Simple Storage Service |
| SDK | Software Development Kit |
| SNS | Simple Notification Service |
| SQS | Simple Queue Service |
| VPC | Virtual Private Cloud |

---

# 4. Summary

This glossary serves as the common vocabulary for the CPM project.

All project documentation, design discussions, implementation, and future contributions should use these definitions to maintain consistency across the platform.