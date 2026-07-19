# Operations Runbook

This document serves as the operations guide for hosting, upgrading, and managing the CPM application.

## Common Operations

### 1. Manual Deployment
To deploy manually using the Makefile:
```bash
make build
# Follow environment deployment instructions
```

### 2. Database Backup & Restore

#### Backup Command
```bash
# Example backup command
pg_dump -U username dbname > backup.sql
```

#### Restore Command
```bash
# Example restore command
psql -U username dbname < backup.sql
```

### 3. Scaling Services
- To scale up services in production, adjust replica counts in Terraform configs or run:
  ```bash
  kubectl scale deployment/cpm-service --replicas=5
  ```
