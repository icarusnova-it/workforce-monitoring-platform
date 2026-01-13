# Agent Capabilities

> **Icarus Nova** | Clear definition of what the monitoring agent can and cannot do.

## Overview

This document clearly defines the capabilities and limitations of the Monitoring Agent. It explicitly states what the agent can do, what it cannot do, and the boundaries that protect user privacy.

## What the Agent CAN Do

### ✅ Activity Monitoring

**Application Usage Tracking:**
- Monitor which applications are running
- Track application launch and close events
- Identify application category (e.g., Productivity, Development)
- Measure application usage duration
- Track application usage patterns

**Window Focus Tracking:**
- Monitor which window has focus
- Track window focus changes
- Measure focus duration
- Identify active application

**System State Monitoring:**
- Detect system idle state
- Detect system active state
- Track idle/active transitions
- Measure idle and active durations

**Network Activity Monitoring:**
- Monitor network traffic volume (bytes)
- Track network activity direction (inbound/outbound)
- Identify general protocol types
- Measure network usage patterns

### ✅ Data Collection

**Collected Data:**
- Application names and categories
- Window focus events
- System state changes
- Network activity volume
- Timestamps and durations

**Data Characteristics:**
- Minimal and necessary only
- Aggregated when possible
- Privacy-preserving
- User-accessible

### ✅ Secure Communication

**Backend Communication:**
- Secure data transmission to backend
- Certificate-based authentication
- Encrypted data transmission
- Automatic retry on failure
- Offline buffering

**Security Features:**
- TLS 1.3+ encryption
- Certificate pinning
- Mutual TLS (mTLS)
- End-to-end encryption

### ✅ Consent Enforcement

**Consent Management:**
- Check consent status before data collection
- Enforce consent boundaries
- Stop data collection when consent withdrawn
- Validate consent version
- Handle consent updates

### ✅ Configuration Management

**Configuration:**
- Receive policy updates from backend
- Apply configuration changes
- Store configuration securely
- Validate configuration

### ✅ Updates

**Update Capabilities:**
- Check for updates automatically
- Download and verify updates
- Install updates securely
- Rollback on failure

## What the Agent CANNOT Do

### ❌ Keylogging

**Explicitly Excluded:**
- Cannot capture keystrokes
- Cannot monitor keyboard input
- Cannot analyze typing patterns
- Cannot capture passwords
- Cannot track keyboard activity

**Rationale:**
- Extreme privacy violation
- Security risk
- Not necessary for productivity analysis
- Legal and ethical concerns

### ❌ Screen Capture

**Explicitly Excluded:**
- Cannot capture screenshots
- Cannot record screen content
- Cannot capture visual content
- Cannot analyze screen images
- Cannot monitor screen activity visually

**Rationale:**
- Complete privacy violation
- Captures sensitive information
- Not necessary for productivity
- Legal and compliance issues

### ❌ File Access

**Explicitly Excluded:**
- Cannot read file contents
- Cannot access file data
- Cannot analyze documents
- Cannot scan file systems
- Cannot access file metadata beyond name/type

**Rationale:**
- Privacy violation
- Intellectual property concerns
- Not necessary for monitoring
- Legal risks

### ❌ Personal Communications

**Explicitly Excluded:**
- Cannot access email content
- Cannot read chat messages
- Cannot monitor instant messaging
- Cannot access social media content
- Cannot track personal communications

**Rationale:**
- Extreme privacy violation
- Personal communication protection
- Legal requirements (wiretap laws)
- Ethical boundaries

### ❌ Credential Capture

**Explicitly Excluded:**
- Cannot capture passwords
- Cannot access credentials
- Cannot monitor authentication
- Cannot store security tokens
- Cannot access password managers

**Rationale:**
- Security risk
- Privacy violation
- Legal liability
- Ethical violation

### ❌ Personal Browsing

**Explicitly Excluded:**
- Cannot track personal websites
- Cannot monitor personal browsing
- Cannot track personal searches
- Cannot analyze personal online activity

**Rationale:**
- Privacy protection
- Personal activity separation
- Legal considerations
- Ethical boundaries

### ❌ Biometric Data

**Explicitly Excluded:**
- Cannot capture biometric data
- Cannot use fingerprint readers
- Cannot use facial recognition
- Cannot capture voice data
- Cannot access biometric sensors

**Rationale:**
- Privacy concerns
- Regulatory restrictions
- Not necessary for monitoring
- Ethical considerations

## Technical Limitations

### Resource Constraints

**Performance Limits:**
- Minimal CPU usage (< 1%)
- Minimal memory usage (< 50 MB)
- Minimal network usage (< 1 MB/hour)
- Minimal disk I/O

**Impact:**
- Limits data collection frequency
- Requires efficient implementation
- Batch operations necessary
- Resource-aware design

### Platform Limitations

**Platform-Specific:**
- Platform API limitations
- Permission requirements
- Security restrictions
- Compatibility constraints

**Impact:**
- Platform-specific implementations
- Permission management
- Security considerations
- Compatibility testing

### Privacy Boundaries

**Enforced Boundaries:**
- Consent requirements
- Data minimization
- Privacy-preserving collection
- User control

**Impact:**
- Limited data collection scope
- Aggregation necessary
- Privacy-first design
- User empowerment

## Capability Matrix

| Capability | Status | Notes |
|------------|--------|-------|
| Application Usage Tracking | ✅ Enabled | With consent |
| Window Focus Tracking | ✅ Enabled | With consent |
| System State Monitoring | ✅ Enabled | With consent |
| Network Volume Tracking | ✅ Enabled | Volume only, not content |
| Keystroke Capture | ❌ Disabled | Explicitly excluded |
| Screen Capture | ❌ Disabled | Explicitly excluded |
| File Content Access | ❌ Disabled | Explicitly excluded |
| Personal Communications | ❌ Disabled | Explicitly excluded |
| Credential Capture | ❌ Disabled | Explicitly excluded |
| Personal Browsing | ❌ Disabled | Explicitly excluded |
| Biometric Data | ❌ Disabled | Explicitly excluded |

## Privacy Protections

### Consent Enforcement

- No data collection without consent
- Immediate stop on consent withdrawal
- Consent version validation
- Policy enforcement

### Data Minimization

- Collect only necessary data
- Aggregate when possible
- Exclude personal data
- Privacy-preserving collection

### User Control

- User access to own data
- Consent management
- Data export capability
- Deletion requests

## Security Features

### Authentication

- Certificate-based authentication
- Device certificates
- Certificate pinning
- Mutual TLS

### Encryption

- Local encryption
- Transport encryption
- End-to-end encryption
- Secure key management

### Protection

- Code signing
- Integrity checks
- Tamper detection
- Self-protection

## Related Documents

- [Agent Architecture](./architecture.md)
- [Data Collection Boundaries](../diagrams/data-collection-boundaries.md)
- [ADR-0001: No Keylogging](../adr/0001-no-keylogging.md)
- [ADR-0003: Minimal Data Collection](../adr/0003-minimal-data-collection.md)

---

**Last Updated:** 2024  
**Maintained by:** Icarus Nova Architecture Team  
**Version:** 1.0
