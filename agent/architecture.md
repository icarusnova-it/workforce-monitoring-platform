# Agent Architecture

> **Icarus Nova** | Detailed architecture of the monitoring agent component.

## Overview

The Monitoring Agent is a native, lightweight application that runs on user devices to collect activity data for productivity analysis. This document describes the agent's architecture, components, and design decisions.

## Architecture Principles

### 1. Privacy by Design
- Consent enforcement at agent level
- Minimal data collection
- No invasive monitoring
- User control and transparency

### 2. Security First
- Certificate-based authentication
- End-to-end encryption
- Tamper-resistant design
- Secure communication

### 3. Performance Optimized
- Minimal resource usage
- Efficient event collection
- Batch operations
- Background operation

### 4. Reliability
- Automatic retry mechanisms
- Offline mode support
- Error recovery
- Health monitoring

## Component Architecture

```
┌─────────────────────────────────────────┐
│         Monitoring Agent                 │
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────────────────────────────┐  │
│  │   Consent Manager                │  │
│  │   - Consent status checking      │  │
│  │   - Consent enforcement           │  │
│  │   - Policy validation             │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │   Data Collector                  │  │
│  │   - Application monitoring         │  │
│  │   - Window focus tracking          │  │
│  │   - System state monitoring        │  │
│  │   - Network activity (volume)      │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │   Encryption Module               │  │
│  │   - Local encryption              │  │
│  │   - Key management                │  │
│  │   - Secure storage                │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │   Communication Module            │  │
│  │   - Backend communication         │  │
│  │   - Certificate management        │  │
│  │   - Retry logic                   │  │
│  │   - Offline buffering             │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │   Configuration Manager           │  │
│  │   - Policy management             │  │
│  │   - Configuration updates          │  │
│  │   - Local storage                 │  │
│  └──────────────────────────────────┘  │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │   Update Manager                  │  │
│  │   - Update checking                │  │
│  │   - Secure updates                 │  │
│  │   - Rollback capability            │  │
│  └──────────────────────────────────┘  │
│                                         │
└─────────────────────────────────────────┘
```

## Core Components

### Consent Manager

**Responsibilities:**
- Check consent status before data collection
- Enforce consent boundaries
- Validate consent version
- Handle consent withdrawal
- Stop data collection when consent withdrawn

**Implementation:**
- Periodic consent status checks
- Immediate stop on consent withdrawal
- Consent version validation
- Policy enforcement

### Data Collector

**Responsibilities:**
- Monitor application usage
- Track window focus events
- Monitor system state (idle/active)
- Track network activity volume
- Collect activity data

**Data Collected:**
- Application name and category
- Window focus events
- System idle/active state
- Network activity volume (not content)

**Data NOT Collected:**
- Keystrokes
- Screen content
- File contents
- Personal communications
- Passwords

**Implementation:**
- Platform-specific APIs
- Efficient event collection
- Minimal resource usage
- Privacy-preserving collection

### Encryption Module

**Responsibilities:**
- Encrypt data before transmission
- Manage encryption keys
- Secure key storage
- Local data encryption

**Implementation:**
- AES-256 encryption
- GCM mode for authenticated encryption
- Secure key storage (OS keychain)
- Efficient encryption operations

### Communication Module

**Responsibilities:**
- Secure backend communication
- Certificate-based authentication
- Data transmission
- Retry logic and error handling
- Offline buffering

**Implementation:**
- TLS 1.3+ for transport
- Certificate pinning
- Mutual TLS (mTLS)
- Automatic retry with exponential backoff
- Local buffer for offline operation

### Configuration Manager

**Responsibilities:**
- Manage agent configuration
- Handle policy updates
- Store configuration locally
- Validate configuration

**Implementation:**
- Secure local storage
- Configuration versioning
- Policy update mechanism
- Configuration validation

### Update Manager

**Responsibilities:**
- Check for updates
- Download and verify updates
- Install updates securely
- Rollback on failure

**Implementation:**
- Secure update server
- Signed update packages
- Integrity verification
- Automatic update mechanism
- Rollback capability

## Data Flow

### Normal Operation Flow

1. **Consent Check**: Consent Manager checks consent status
2. **Data Collection**: If consent active, Data Collector collects activity data
3. **Local Encryption**: Encryption Module encrypts data
4. **Buffering**: Data stored in local encrypted buffer
5. **Transmission**: Communication Module sends data to backend
6. **Acknowledgment**: Backend acknowledgment received
7. **Buffer Clear**: Encrypted buffer cleared after successful transmission

### Consent Withdrawal Flow

1. **Withdrawal Notification**: Backend notifies agent of consent withdrawal
2. **Immediate Stop**: Data Collector stops data collection
3. **Buffer Handling**: Existing buffered data handled per policy
4. **Confirmation**: Agent confirms stop to backend
5. **Status Update**: Agent updates internal status

### Offline Operation Flow

1. **Connectivity Loss**: Network connectivity lost
2. **Local Buffering**: Data Collector continues, data buffered locally
3. **Encryption**: Buffered data encrypted
4. **Retry**: Communication Module retries periodically
5. **Transmission**: When connectivity restored, buffered data transmitted
6. **Buffer Clear**: Buffer cleared after successful transmission

## Platform-Specific Implementation

### Windows

**APIs Used:**
- Windows API for application monitoring
- Event hooks for window focus
- System state APIs
- Network activity APIs

**Implementation:**
- Native Windows application
- Windows service or background process
- Code signing with Authenticode
- Windows-specific security features

### macOS

**APIs Used:**
- macOS APIs for application monitoring
- Accessibility APIs (with permissions)
- System state APIs
- Network activity APIs

**Implementation:**
- Native macOS application
- Background daemon or agent
- Code signing and notarization
- macOS-specific security features

### Linux

**APIs Used:**
- Linux-specific APIs
- X11/Wayland integration
- System state APIs
- Network activity APIs

**Implementation:**
- Native Linux application
- Systemd service or daemon
- Package management integration
- Linux-specific security features

## Security Architecture

### Authentication

- Certificate-based authentication
- Device certificates
- Certificate pinning
- Mutual TLS (mTLS)

### Encryption

- Local encryption (AES-256)
- Transport encryption (TLS 1.3+)
- End-to-end encryption
- Secure key management

### Protection

- Code signing
- Integrity checks
- Tamper detection
- Self-protection mechanisms

## Performance Architecture

### Resource Management

**CPU Usage:**
- Target: < 1% average
- Peak: < 5%
- Efficient event collection
- Minimal processing

**Memory Usage:**
- Target: < 50 MB baseline
- Peak: < 100 MB
- Efficient data structures
- Minimal memory footprint

**Network Usage:**
- Target: < 1 MB/hour
- Peak: < 10 MB/hour
- Efficient data transmission
- Batch transmission

### Optimization Strategies

- Efficient event collection
- Batch operations
- Minimal processing
- Background operation
- Resource-aware design

## Error Handling

### Network Errors

- Automatic retry with exponential backoff
- Offline buffering
- Error logging
- User notification (if required)

### Consent Violations

- Immediate stop on violation
- Error logging
- Audit trail
- Administrator notification

### System Errors

- Graceful error handling
- Error recovery
- Error logging
- Health monitoring

## Monitoring and Observability

### Agent Metrics

- Resource usage
- Data collection rate
- Transmission success rate
- Error rates
- Consent status

### Logging

- Operational logs
- Error logs
- Security events
- Performance metrics
- Minimal logging (privacy-preserving)

## Related Documents

- [Agent Capabilities](./capabilities.md)
- [ADR-0004: Agent Architecture](../adr/0004-agent-architecture.md)
- [Non-Functional Requirements](../docs/non-functional-requirements.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
