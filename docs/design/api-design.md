# API Design

This document details the REST API specifications, endpoints, and standards for CPM.

## General Guidelines
- All requests and responses must be in JSON format.
- Standard HTTP status codes must be used to represent success or failure.

## Endpoints

### Authentication

#### `POST /api/v1/auth/login`
Authenticates a user and returns a token.
- **Request Body**:
  ```json
  {
    "username": "user123",
    "password": "securepassword"
  }
  ```
- **Response (200 OK)**:
  ```json
  {
    "token": "eyJhbGciOi...",
    "expires_at": "2026-07-20T20:00:00Z"
  }
  ```

### Resources

#### `GET /api/v1/resources`
Retrieves a paginated list of resources.

#### `POST /api/v1/resources`
Creates a new resource.
