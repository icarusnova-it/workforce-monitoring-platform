# API Boundaries

> **Icarus Nova** | API design, security boundaries, and access controls for backend services.

## Overview

This document defines the API boundaries for the Workforce Monitoring Platform backend services. It specifies what APIs are exposed, what they do, what they don't do, and the security controls in place.

## API Design Principles

### 1. RESTful Design
- Resource-based URLs
- HTTP methods (GET, POST, PUT, DELETE)
- Stateless operations
- Standard HTTP status codes

### 2. Security First
- Authentication required for all endpoints
- Authorization based on roles
- Rate limiting
- Input validation

### 3. Privacy Protection
- Minimal data exposure
- User data access controls
- Consent verification
- Audit logging

### 4. Performance
- Efficient endpoints
- Caching where appropriate
- Pagination for large datasets
- Response optimization

## API Categories

### Public APIs (Authenticated)

These APIs require authentication but are available to authenticated users.

#### Agent APIs

**Endpoint**: `/api/v1/agent/data`
- **Method**: POST
- **Authentication**: Certificate-based (mTLS)
- **Purpose**: Receive activity data from agents
- **Access**: Agents only
- **Rate Limit**: Per agent, per organization

**Endpoint**: `/api/v1/agent/register`
- **Method**: POST
- **Authentication**: Certificate-based (mTLS)
- **Purpose**: Register new agent device
- **Access**: Agents only
- **Rate Limit**: Per agent

**Endpoint**: `/api/v1/agent/status`
- **Method**: GET
- **Authentication**: Certificate-based (mTLS)
- **Purpose**: Get agent status and configuration
- **Access**: Agents only
- **Rate Limit**: Per agent

#### User APIs

**Endpoint**: `/api/v1/users/me/data`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT
- **Purpose**: Get user's own monitoring data
- **Access**: User's own data only
- **Rate Limit**: Per user

**Endpoint**: `/api/v1/users/me/consent`
- **Method**: GET, POST, DELETE
- **Authentication**: OAuth 2.0 / JWT
- **Purpose**: Manage user's own consent
- **Access**: User's own consent only
- **Rate Limit**: Per user

**Endpoint**: `/api/v1/users/me/export`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT
- **Purpose**: Export user's own data
- **Access**: User's own data only
- **Rate Limit**: Per user, per day

### Manager APIs

**Endpoint**: `/api/v1/teams/{teamId}/metrics`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT
- **Purpose**: Get aggregated team productivity metrics
- **Access**: Team managers only
- **Rate Limit**: Per manager

**Endpoint**: `/api/v1/teams/{teamId}/reports`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT
- **Purpose**: Get team productivity reports
- **Access**: Team managers only
- **Rate Limit**: Per manager

### Admin APIs

**Endpoint**: `/api/v1/admin/organizations/{orgId}/users`
- **Method**: GET, POST, PUT, DELETE
- **Authentication**: OAuth 2.0 / JWT + MFA
- **Purpose**: Manage organization users
- **Access**: Organization admins only
- **Rate Limit**: Per admin

**Endpoint**: `/api/v1/admin/organizations/{orgId}/policies`
- **Method**: GET, POST, PUT, DELETE
- **Authentication**: OAuth 2.0 / JWT + MFA
- **Purpose**: Manage monitoring policies
- **Access**: Organization admins only
- **Rate Limit**: Per admin

**Endpoint**: `/api/v1/admin/organizations/{orgId}/consent`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT + MFA
- **Purpose**: View organization consent status
- **Access**: Organization admins only
- **Rate Limit**: Per admin

### Auditor APIs

**Endpoint**: `/api/v1/audit/logs`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT + MFA
- **Purpose**: Access audit logs
- **Access**: Auditors only
- **Rate Limit**: Per auditor

**Endpoint**: `/api/v1/audit/compliance`
- **Method**: GET
- **Authentication**: OAuth 2.0 / JWT + MFA
- **Purpose**: Generate compliance reports
- **Access**: Auditors only
- **Rate Limit**: Per auditor

## What APIs Expose

### ✅ Exposed Data

**User Data (Own Data Only):**
- User's own activity data
- User's own productivity metrics
- User's own consent records
- User's own audit trail

**Manager Data (Aggregated):**
- Team productivity metrics (aggregated)
- Team activity patterns (aggregated)
- Team compliance status
- Team reports

**Admin Data:**
- Organization-wide metrics
- User management
- Policy configuration
- System configuration

**Auditor Data:**
- Audit logs
- Compliance reports
- Consent records
- System events

### ❌ NOT Exposed

**Sensitive Data:**
- Individual user data to managers (only aggregated)
- Personal communications
- Credentials
- Encryption keys

**Internal Data:**
- Internal service communication
- Database schemas
- System internals
- Configuration details

**Prohibited Data:**
- Keystroke data (not collected)
- Screen content (not collected)
- File contents (not collected)
- Personal communications (not collected)

## Security Boundaries

### Authentication

**Methods:**
- OAuth 2.0 / OpenID Connect for users
- Certificate-based (mTLS) for agents
- JWT tokens for API access
- Multi-factor authentication for admins

**Enforcement:**
- All endpoints require authentication
- Token validation on every request
- Certificate validation for agents
- Session management

### Authorization

**Role-Based Access Control:**
- **User**: Own data only
- **Manager**: Aggregated team data
- **Admin**: Organization-wide data
- **Auditor**: Audit and compliance data

**Resource-Level Permissions:**
- Users can only access their own data
- Managers can only access their team's data
- Admins can only access their organization's data
- Auditors have read-only access to audit data

**Enforcement:**
- Authorization checks on every request
- Resource ownership validation
- Role verification
- Permission validation

### Rate Limiting

**Limits:**
- Per user: 1000 requests/hour
- Per agent: 100 requests/minute
- Per manager: 500 requests/hour
- Per admin: 2000 requests/hour
- Per auditor: 1000 requests/hour

**Enforcement:**
- API Gateway rate limiting
- Per-user rate limits
- Per-organization rate limits
- Automatic throttling

### Input Validation

**Validation:**
- Schema validation
- Data type validation
- Range validation
- Business rule validation
- Security validation (SQL injection, XSS, etc.)

**Enforcement:**
- Request validation middleware
- Schema validation
- Input sanitization
- Error handling

## API Versioning

### Version Strategy

- URL-based versioning (`/api/v1/`, `/api/v2/`)
- Backward compatibility maintained
- Deprecation notices
- Version migration support

### Current Version

- **v1**: Current stable version
- All new features in v1
- Backward compatibility maintained

## Error Handling

### Error Responses

**Standard Format:**
```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {},
    "timestamp": "2024-01-01T00:00:00Z"
  }
}
```

**HTTP Status Codes:**
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 429: Too Many Requests
- 500: Internal Server Error

## API Documentation

### Documentation Standards

- OpenAPI/Swagger specification
- Interactive API documentation
- Code examples
- Authentication guide
- Rate limiting information

### Documentation Access

- Public documentation (authenticated endpoints)
- Developer portal
- API reference
- Integration guides

## Monitoring and Observability

### API Metrics

- Request rates
- Response times
- Error rates
- Rate limit hits
- Authentication failures

### Logging

- All API requests logged
- Authentication events logged
- Authorization failures logged
- Error events logged
- Audit trail maintained

## Related Documents

- [Backend Architecture](./architecture.md)
- [C4 Container Diagram](../diagrams/c4-container-diagram.md)
- [Threat Model](../docs/threat-model.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
