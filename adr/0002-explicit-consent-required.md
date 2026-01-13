# ADR-0002: Explicit Consent Required

## Status

**Accepted** - This is a fundamental architectural decision that cannot be changed without significant impact.

## Context

Workforce monitoring raises significant privacy and legal concerns. Different jurisdictions have varying requirements for employee monitoring:

- **GDPR (EU)**: Requires explicit consent or legitimate interest
- **LGPD (Brazil)**: Requires explicit consent for personal data processing
- **US State Laws**: Varying requirements for notice and consent
- **Employment Law**: Collective bargaining agreements may require consent

Many monitoring solutions operate with implied consent or minimal notice. This creates:
- Legal risks
- Privacy violations
- Trust issues
- Compliance problems

We need to decide whether consent is optional, implied, or explicit.

## Decision

**Explicit consent is REQUIRED for the platform to operate. No monitoring will occur without explicit, documented consent.**

The platform will:

1. **Require explicit consent** before any data collection begins
2. **Document consent** with timestamp, version, and method
3. **Enforce consent** at the agent level (agent will not collect data without active consent)
4. **Support consent withdrawal** with immediate effect
5. **Version consent** when policies change
6. **Maintain audit trails** of all consent actions

## Consequences

### Positive

✅ **Legal Compliance**: Meets GDPR, LGPD, and other privacy regulations  
✅ **Risk Mitigation**: Reduces legal and compliance risks  
✅ **Trust Building**: Demonstrates respect for user privacy  
✅ **Ethical Positioning**: Positions platform as ethical and responsible  
✅ **Audit Trail**: Comprehensive consent records for compliance  
✅ **User Control**: Empowers users with control over monitoring  

### Negative

❌ **Adoption Friction**: Users must actively consent (may reduce adoption)  
❌ **Consent Management**: Requires robust consent management system  
❌ **Operational Complexity**: Consent versioning and management adds complexity  
❌ **Potential Opt-Outs**: Some users may choose not to consent  

### Mitigation

- Clear, user-friendly consent process
- Transparent explanation of monitoring scope
- Emphasize benefits of consent (productivity insights)
- Support for consent education and communication
- Regular consent reminders and re-confirmation

## Implementation

### Consent Capture

**Methods:**
- Web-based consent form
- Application-based consent
- Signed consent document (for sensitive cases)
- Multi-step consent process

**Requirements:**
- Clear explanation of what is monitored
- Clear explanation of what is NOT monitored
- Information about data usage
- Information about user rights
- Easy withdrawal process

### Consent Storage

**Database:**
- Immutable consent records
- Timestamp and version tracking
- Consent method documentation
- User identification
- IP address and device information

**Encryption:**
- Consent records encrypted at rest
- Access controls on consent data
- Audit logging of access

### Consent Enforcement

**Agent Level:**
- Agent checks consent status before data collection
- Agent stops collection if consent withdrawn
- Agent validates consent version
- Agent enforces consent boundaries

**Backend Level:**
- Backend validates consent before processing data
- Backend rejects data if consent not active
- Backend logs consent violations
- Backend notifies administrators

### Consent Withdrawal

**Process:**
- User initiates withdrawal
- Confirmation requested
- Withdrawal processed immediately
- Monitoring stops
- User notified

**Data Handling:**
- Existing data retained per retention policy
- No new data collection
- User retains access to historical data

## Legal Considerations

### GDPR Compliance

- **Lawful Basis**: Explicit consent
- **Freely Given**: No coercion
- **Specific**: Clear purpose
- **Informed**: Full information provided
- **Unambiguous**: Clear affirmative action
- **Withdrawable**: Easy withdrawal

### Other Jurisdictions

- **LGPD (Brazil)**: Explicit consent required
- **US State Laws**: Varying requirements, explicit consent safest
- **Employment Law**: Collective agreements may require consent
- **Regional Variations**: Local law compliance

## Related Decisions

- [ADR-0001: No Keylogging](./0001-no-keylogging.md)
- [ADR-0003: Minimal Data Collection](./0003-minimal-data-collection.md)
- [Consent Model](../docs/consent-model.md)

## References

- [Legal Considerations](../docs/legal-considerations.md)
- [Privacy by Design](../docs/privacy-by-design.md)
- [Product Vision](../docs/product-vision.md)

---

**Date**: 2024  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
