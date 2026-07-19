# ADR-0004: Component-Based Architecture

## Status
Accepted

## Context
Deploying full infrastructure stacks in a single monolithic Terraform workspace leads to slow runtimes, large blast radiuses, and complex merge conflicts.

## Decision
CPM will enforce a **Component-Based Architecture**. Infrastructure will be divided into modular, independent "components" (e.g., networking, identity, storage).
- Each component will have its own code, configuration, and separate Terraform state.
- CPM will track dependencies between components and automatically orchestrate the correct execution order (DAG - Directed Acyclic Graph).

## Consequences
- **Pros**:
  - Small, isolated blast radiuses for updates.
  - Faster pipeline execution times.
  - Reusable module templates.
- **Cons**:
  - Requires maintaining a stateful dependency graph within the control plane.
  - Passing outputs from one component to another (e.g., VPC ID to Database) must be handled explicitly by CPM.
