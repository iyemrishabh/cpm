# Repository Strategy

This document details the branching, versioning, and repository management guidelines for CPM.

## Branching Model

We follow a modified **GitHub Flow** model:
- **`main`**: The primary branch. Code here must always build successfully and pass all tests. Direct pushes to `main` are disabled; changes must be submitted via Pull Requests (PRs).
- **Feature Branches (`feature/*`)**: Used for developing new features.
- **Bugfix Branches (`bugfix/*` or `hotfix/*`)**: Used for fixing bugs.

## Commits & Pull Requests

- **Conventional Commits**: Commit messages should adhere to the Conventional Commits specification.
  - *Format*: `<type>(<scope>): <description>`
  - *Examples*: `feat(auth): add MFA support`, `fix(api): handle empty payload validation`
- **PR Code Review**: At least one approval from a designated code owner is required before merging.
