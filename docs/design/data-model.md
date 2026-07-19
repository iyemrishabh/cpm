# Data Model

This document describes the logical data model and schema definitions for the CPM project.

## Entities

### User
Represents an authenticated user within the system.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | UUID | Unique identifier |
| `username`| String | Unique login name |
| `email` | String | User's contact email |
| `created_at`| Timestamp | Creation date and time |

### Resource
Represents a managed domain entity.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | UUID | Unique identifier |
| `owner_id`| UUID | Reference to User who owns the resource |
| `name` | String | User-friendly resource name |
| `metadata`| JSON | Extensible configuration properties |
