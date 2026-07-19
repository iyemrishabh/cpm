# ADR-0002: AWS-Native First Architecture

## Status
Accepted

## Context
CPM needs to run reliably and cost-effectively, scaling dynamically with deployment tasks without requiring heavy operational maintenance for container clusters or VMs when idle. It also requires tight integration with AWS APIs for multi-account governance.

## Decision
We will adopt an **AWS-Native First** architecture. The CPM control plane will leverage managed services:
- **Orchestration**: AWS Step Functions for stateful, dependency-aware workflows.
- **Compute**: AWS Lambda for short-lived task execution, and AWS ECS Fargate for longer-running deployment tasks.
- **Data Persistence**: Amazon DynamoDB for low-latency metadata store and Amazon S3 for state/artifact storage.

## Consequences
- **Pros**:
  - Extremely low idle cost (pay-per-use).
  - High availability and scalability managed by AWS.
  - Native integration with AWS Identity and Access Management (IAM) for cross-account execution.
- **Cons**:
  - Tight coupling with AWS services makes it harder to run CPM on other cloud providers (e.g., Azure, GCP) without modifications.
