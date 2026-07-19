# ADR-0003: Terraform First Engine

## Status
Accepted

## Context
Various infrastructure-as-code (IaC) tools exist in the ecosystem (e.g., Terraform, Pulumi, CloudFormation, AWS CDK). Platform teams already have a significant investment in Terraform modules, and require a robust, open ecosystem for managing multi-cloud or AWS infrastructure.

## Decision
CPM will use **Terraform** as the primary engine for infrastructure execution and provisioning. CPM will orchestrate Terraform commands (e.g., init, plan, apply, destroy) in a secure, isolated runner container (ECS Fargate) and manage backend states centrally.

## Consequences
- **Pros**:
  - Leverages a massive ecosystem of existing community modules.
  - Consistent state management paradigm.
  - Easy integration with existing platform tooling.
- **Cons**:
  - Requires orchestrating external processes (Terraform CLI) inside container environments, which requires additional container orchestration logic compared to using pure SDKs.
