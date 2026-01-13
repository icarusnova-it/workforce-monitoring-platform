# Audit Log Example

> **Icarus Nova** | Conceptual example of audit logging for compliance and security (NOT production code).

## Overview

This document illustrates the audit logging system in the Workforce Monitoring Platform. Audit logs are critical for compliance, security, and transparency. This is a **conceptual example** for educational purposes.

## Audit Log Categories

### 1. Consent Events

**Consent Provided:**
```json
{
  "auditId": "audit-001",
  "eventType": "consent_provided",
  "timestamp": "2024-01-15T10:00:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "consent_provided",
  "details": {
    "consentId": "consent-abc123",
    "consentVersion": "1.0",
    "consentMethod": "web",
    "ipAddress": "192.168.1.100",
    "deviceInfo": {
      "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
      "platform": "Windows"
    }
  },
  "result": "success",
  "actor": {
    "type": "user",
    "id": "user-12345",
    "email": "user@example.com"
  }
}
```

**Consent Withdrawn:**
```json
{
  "auditId": "audit-002",
  "eventType": "consent_withdrawn",
  "timestamp": "2024-06-01T14:30:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "consent_withdrawn",
  "details": {
    "consentId": "consent-abc123",
    "withdrawalMethod": "web",
    "withdrawalReason": "user_requested",
    "ipAddress": "192.168.1.100",
    "deviceInfo": {
      "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
      "platform": "Windows"
    }
  },
  "result": "success",
  "actor": {
    "type": "user",
    "id": "user-12345",
    "email": "user@example.com"
  }
}
```

### 2. Data Access Events

**User Data Access:**
```json
{
  "auditId": "audit-003",
  "eventType": "data_access",
  "timestamp": "2024-01-15T11:00:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "data_access",
  "details": {
    "accessType": "user_self_access",
    "dataType": "activity_data",
    "dateRange": {
      "start": "2024-01-01",
      "end": "2024-01-15"
    },
    "ipAddress": "192.168.1.100",
    "userAgent": "Mozilla/5.0..."
  },
  "result": "success",
  "actor": {
    "type": "user",
    "id": "user-12345",
    "email": "user@example.com"
  }
}
```

**Manager Data Access:**
```json
{
  "auditId": "audit-004",
  "eventType": "data_access",
  "timestamp": "2024-01-15T12:00:00Z",
  "userId": "manager-67890",
  "organizationId": "org-67890",
  "action": "data_access",
  "details": {
    "accessType": "manager_team_access",
    "dataType": "aggregated_metrics",
    "teamId": "team-xyz",
    "dateRange": {
      "start": "2024-01-01",
      "end": "2024-01-15"
    },
    "ipAddress": "192.168.1.200",
    "userAgent": "Mozilla/5.0..."
  },
  "result": "success",
  "actor": {
    "type": "manager",
    "id": "manager-67890",
    "email": "manager@example.com"
  }
}
```

**Admin Data Access:**
```json
{
  "auditId": "audit-005",
  "eventType": "data_access",
  "timestamp": "2024-01-15T13:00:00Z",
  "userId": "admin-99999",
  "organizationId": "org-67890",
  "action": "data_access",
  "details": {
    "accessType": "admin_organization_access",
    "dataType": "user_data",
    "targetUserId": "user-12345",
    "dateRange": {
      "start": "2024-01-01",
      "end": "2024-01-15"
    },
    "ipAddress": "192.168.1.300",
    "userAgent": "Mozilla/5.0...",
    "reason": "compliance_review"
  },
  "result": "success",
  "actor": {
    "type": "admin",
    "id": "admin-99999",
    "email": "admin@example.com"
  }
}
```

### 3. System Configuration Events

**Policy Update:**
```json
{
  "auditId": "audit-006",
  "eventType": "policy_update",
  "timestamp": "2024-01-20T09:00:00Z",
  "userId": "admin-99999",
  "organizationId": "org-67890",
  "action": "policy_updated",
  "details": {
    "policyId": "policy-001",
    "policyType": "monitoring_policy",
    "previousVersion": "1.0",
    "newVersion": "1.1",
    "changes": [
      {
        "field": "dataRetentionPeriod",
        "oldValue": "90",
        "newValue": "120"
      }
    ],
    "ipAddress": "192.168.1.300",
    "userAgent": "Mozilla/5.0..."
  },
  "result": "success",
  "actor": {
    "type": "admin",
    "id": "admin-99999",
    "email": "admin@example.com"
  }
}
```

**User Management:**
```json
{
  "auditId": "audit-007",
  "eventType": "user_management",
  "timestamp": "2024-01-15T10:30:00Z",
  "userId": "admin-99999",
  "organizationId": "org-67890",
  "action": "user_created",
  "details": {
    "targetUserId": "user-54321",
    "targetUserEmail": "newuser@example.com",
    "role": "employee",
    "ipAddress": "192.168.1.300",
    "userAgent": "Mozilla/5.0..."
  },
  "result": "success",
  "actor": {
    "type": "admin",
    "id": "admin-99999",
    "email": "admin@example.com"
  }
}
```

### 4. Security Events

**Authentication Success:**
```json
{
  "auditId": "audit-008",
  "eventType": "authentication",
  "timestamp": "2024-01-15T09:00:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "authentication_success",
  "details": {
    "authMethod": "oauth2",
    "ipAddress": "192.168.1.100",
    "userAgent": "Mozilla/5.0...",
    "sessionId": "session-abc123"
  },
  "result": "success",
  "actor": {
    "type": "user",
    "id": "user-12345",
    "email": "user@example.com"
  }
}
```

**Authentication Failure:**
```json
{
  "auditId": "audit-009",
  "eventType": "authentication",
  "timestamp": "2024-01-15T09:05:00Z",
  "userId": null,
  "organizationId": "org-67890",
  "action": "authentication_failure",
  "details": {
    "authMethod": "oauth2",
    "ipAddress": "192.168.1.100",
    "userAgent": "Mozilla/5.0...",
    "failureReason": "invalid_credentials",
    "attemptedEmail": "user@example.com"
  },
  "result": "failure",
  "actor": {
    "type": "unknown",
    "id": null,
    "email": null
  }
}
```

**Authorization Failure:**
```json
{
  "auditId": "audit-010",
  "eventType": "authorization",
  "timestamp": "2024-01-15T11:30:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "authorization_failure",
  "details": {
    "resource": "/api/v1/teams/team-xyz/metrics",
    "requiredRole": "manager",
    "userRole": "employee",
    "ipAddress": "192.168.1.100",
    "userAgent": "Mozilla/5.0..."
  },
  "result": "failure",
  "actor": {
    "type": "user",
    "id": "user-12345",
    "email": "user@example.com"
  }
}
```

### 5. Data Operations

**Data Export:**
```json
{
  "auditId": "audit-011",
  "eventType": "data_export",
  "timestamp": "2024-01-15T15:00:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "data_export",
  "details": {
    "exportType": "user_self_export",
    "dataType": "activity_data",
    "dateRange": {
      "start": "2024-01-01",
      "end": "2024-01-15"
    },
    "format": "json",
    "ipAddress": "192.168.1.100",
    "userAgent": "Mozilla/5.0..."
  },
  "result": "success",
  "actor": {
    "type": "user",
    "id": "user-12345",
    "email": "user@example.com"
  }
}
```

**Data Deletion:**
```json
{
  "auditId": "audit-012",
  "eventType": "data_deletion",
  "timestamp": "2024-06-15T16:00:00Z",
  "userId": "user-12345",
  "organizationId": "org-67890",
  "action": "data_deletion",
  "details": {
    "deletionType": "retention_policy",
    "dataType": "raw_events",
    "dateRange": {
      "start": "2024-01-01",
      "end": "2024-04-01"
    },
    "recordsDeleted": 125000,
    "ipAddress": "system",
    "triggeredBy": "automated_job"
  },
  "result": "success",
  "actor": {
    "type": "system",
    "id": "system",
    "email": null
  }
}
```

## Audit Log Structure

### Standard Audit Log Fields

```json
{
  "auditId": "unique-audit-id",
  "eventType": "event_category",
  "timestamp": "ISO-8601-timestamp",
  "userId": "user-id-or-null",
  "organizationId": "organization-id",
  "action": "specific_action",
  "details": {
    "event-specific-details": "..."
  },
  "result": "success|failure",
  "actor": {
    "type": "user|admin|system|unknown",
    "id": "actor-id",
    "email": "actor-email"
  },
  "metadata": {
    "ipAddress": "ip-address",
    "userAgent": "user-agent",
    "sessionId": "session-id",
    "requestId": "request-id"
  }
}
```

## Audit Log Retention

### Retention Policy

- **Security Events**: 2 years
- **Consent Events**: 7 years (legal compliance)
- **Data Access Events**: 1 year
- **Configuration Events**: 3 years
- **Data Operations**: 1 year
- **Compliance Logs**: 7 years

## Audit Log Access

### Access Controls

**Who Can Access:**
- **Auditors**: Full access to audit logs
- **Admins**: Access to organization audit logs
- **Users**: Access to own audit trail only
- **System**: Automated access for compliance

**Access Logging:**
- All audit log access is logged
- Access events are immutable
- Access requires authorization
- Access is auditable

## Compliance Reporting

### Audit Report Example

```json
{
  "reportId": "audit-report-001",
  "reportType": "compliance_audit",
  "organizationId": "org-67890",
  "period": {
    "start": "2024-01-01",
    "end": "2024-01-31"
  },
  "summary": {
    "totalEvents": 125000,
    "consentEvents": 500,
    "dataAccessEvents": 15000,
    "securityEvents": 2000,
    "configurationEvents": 50
  },
  "findings": {
    "consentCompliance": "compliant",
    "dataAccessCompliance": "compliant",
    "securityCompliance": "compliant",
    "issues": []
  },
  "generatedAt": "2024-02-01T00:00:00Z",
  "generatedBy": "auditor-001"
}
```

## Key Takeaways

1. **Comprehensive Logging**: All significant events are logged
2. **Immutable Logs**: Audit logs cannot be modified
3. **Access Control**: Audit log access is controlled and logged
4. **Compliance**: Audit logs support regulatory compliance
5. **Security**: Audit logs help detect security issues
6. **Transparency**: Audit logs provide transparency

## Related Documents

- [Threat Model](../docs/threat-model.md)
- [Privacy by Design](../docs/privacy-by-design.md)
- [Backend Architecture](../backend/architecture.md)

---

**Note:** This is a conceptual example for educational purposes. Production implementations should include proper error handling, security, compliance, and performance optimizations specific to your environment.

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team
