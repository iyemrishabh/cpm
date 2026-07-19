# Security Model

This document outlines the security architecture, risk controls, and compliance targets for the CPM application.

## Authentication & Authorization
- **Authentication**: Stateless JWT-based authentication.
- **Authorization**: Role-Based Access Control (RBAC) to enforce permissions.

## Data Protection
- **Encryption in Transit**: TLS 1.3 is enforced for all external endpoints.
- **Encryption at Rest**: Databases and persistent storage volumes must use AES-256 encryption.

## Vulnerability Management
- Dependency scanning is run automatically on every build via GitHub Actions.
- Secrets must never be committed to repository files; use environment variables or secret vaults.
