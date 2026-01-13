# ADR-0004: Agent Architecture

## Status

**Accepted** - This architectural decision defines the agent design and implementation approach.

## Context

The monitoring agent is a critical component that runs on user devices. We need to decide on:

- **Architecture**: Native application vs. web-based vs. hybrid
- **Resource Usage**: Performance impact on user devices
- **Security**: Protection against tampering and compromise
- **Deployment**: Installation and update mechanisms
- **Compatibility**: Platform support (Windows, macOS, Linux)

Key considerations:
- **Performance**: Must have minimal impact on user devices
- **Security**: Must be tamper-resistant and secure
- **Privacy**: Must enforce consent and data boundaries
- **Reliability**: Must operate reliably without user intervention
- **Maintainability**: Must be updateable and maintainable

## Decision

**We will implement a native, lightweight agent application with the following characteristics:**

1. **Native Application**: Platform-specific native code (not web-based)
2. **Lightweight Design**: Minimal resource usage (< 1% CPU, < 50 MB memory)
3. **Tamper-Resistant**: Code signing, integrity checks, self-protection
4. **Consent-Enforced**: Agent will not operate without active consent
5. **Secure Communication**: Certificate-based authentication, TLS encryption
6. **Cross-Platform**: Support for Windows, macOS, and Linux
7. **Auto-Updates**: Secure, automatic update mechanism

## Consequences

### Positive

✅ **Performance**: Native code provides optimal performance  
✅ **Resource Efficiency**: Minimal impact on user devices  
✅ **Security**: Native code allows better security controls  
✅ **Reliability**: Native applications are more reliable  
✅ **User Experience**: Minimal disruption to user workflow  
✅ **Platform Integration**: Better integration with OS features  

### Negative

❌ **Development Complexity**: Requires platform-specific development  
❌ **Maintenance Overhead**: Multiple platform versions to maintain  
❌ **Testing Complexity**: Testing across multiple platforms  
❌ **Deployment Complexity**: Platform-specific installation packages  

### Mitigation

- Use cross-platform frameworks where possible (e.g., Go, Rust)
- Shared core logic with platform-specific adapters
- Automated testing across platforms
- Standardized deployment processes
- Platform abstraction layers

## Implementation

### Architecture

**Core Components:**
- **Data Collector**: Platform-specific activity monitoring
- **Consent Manager**: Consent status checking and enforcement
- **Encryption Module**: Local encryption and secure communication
- **Communication Module**: Secure backend communication
- **Configuration Manager**: Policy and configuration management
- **Update Manager**: Secure update mechanism

**Platform Abstraction:**
- Platform-specific APIs for activity monitoring
- Cross-platform core logic
- Platform-specific UI (minimal)
- Platform-specific installation

### Technology Choices

**Language Options:**
- **Go**: Cross-platform, efficient, good for system programming
- **Rust**: Memory-safe, performant, modern
- **C++**: Maximum performance, platform-specific
- **Java**: Cross-platform but higher resource usage

**Recommendation**: Go or Rust for cross-platform efficiency and security.

### Resource Management

**CPU Usage:**
- Target: < 1% average CPU usage
- Peak: < 5% CPU usage during active monitoring
- Efficient event collection
- Minimal processing overhead

**Memory Usage:**
- Target: < 50 MB baseline
- Peak: < 100 MB during active monitoring
- Efficient data structures
- Minimal memory footprint

**Disk I/O:**
- Minimal disk I/O (logging only)
- No significant disk impact
- Efficient logging

**Network Usage:**
- Target: < 1 MB/hour normal operation
- Peak: < 10 MB/hour high activity
- Efficient data transmission
- Batch transmission

### Security

**Code Signing:**
- All agent binaries code-signed
- Platform-specific signing (Windows, macOS)
- Certificate validation
- Tamper detection

**Integrity Protection:**
- Integrity checks on startup
- Self-protection mechanisms
- Tamper detection and response
- Secure storage for sensitive data

**Authentication:**
- Certificate-based authentication
- Device certificate management
- Certificate pinning
- Mutual TLS (mTLS)

### Consent Enforcement

**Agent-Level Enforcement:**
- Agent checks consent before data collection
- Agent stops collection if consent withdrawn
- Agent validates consent version
- Agent enforces data boundaries

**Implementation:**
- Consent status checked on startup
- Periodic consent validation
- Immediate stop on consent withdrawal
- No data collection without active consent

### Communication

**Protocol:**
- HTTPS/TLS 1.3+ for all communication
- Certificate pinning
- Mutual TLS for agent authentication
- Efficient data transmission

**Reliability:**
- Automatic retry on failure
- Exponential backoff
- Local buffering
- Offline mode support

### Updates

**Mechanism:**
- Secure update server
- Signed update packages
- Automatic update checks
- User notification (optional)
- Rollback capability

**Security:**
- Update package signing
- Integrity verification
- Secure download
- Update authentication

## Platform Support

### Windows

**Requirements:**
- Windows 10/11
- .NET Framework or native code
- Windows service or background process
- Code signing with Authenticode

**APIs:**
- Windows API for activity monitoring
- Event hooks for application/window events
- System state APIs

### macOS

**Requirements:**
- macOS 10.15+
- Native macOS application
- Background daemon or agent
- Code signing and notarization

**APIs:**
- macOS APIs for activity monitoring
- Accessibility APIs (with permissions)
- System state APIs

### Linux

**Requirements:**
- Major Linux distributions
- Systemd service or daemon
- Native Linux application
- Package management integration

**APIs:**
- Linux-specific APIs
- X11/Wayland integration
- System state APIs

## Deployment

### Installation

**Methods:**
- MSI installer (Windows)
- DMG/PKG installer (macOS)
- DEB/RPM packages (Linux)
- Enterprise deployment tools (SCCM, MDM)

**Requirements:**
- Administrative privileges
- User consent during installation
- Clear installation instructions
- Uninstall capability

### Configuration

**Initial Configuration:**
- Device registration
- Certificate installation
- Consent capture
- Policy configuration
- Backend connection

**Runtime Configuration:**
- Policy updates
- Configuration changes
- Consent updates
- Feature toggles

## Monitoring and Observability

### Agent Metrics

- Resource usage (CPU, memory, disk, network)
- Data collection rate
- Transmission success rate
- Error rates
- Consent status
- Update status

### Logging

- Operational logs
- Error logs
- Security events
- Performance metrics
- Minimal logging (privacy-preserving)

## Related Decisions

- [ADR-0002: Explicit Consent Required](./0002-explicit-consent-required.md)
- [ADR-0005: Data Encryption Strategy](./0005-data-encryption-strategy.md)
- [Agent Architecture](../agent/architecture.md)

## References

- [Non-Functional Requirements](../docs/non-functional-requirements.md)
- [Threat Model](../docs/threat-model.md)
- [Agent Capabilities](../agent/capabilities.md)

---

**Date**: 2026  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
