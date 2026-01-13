# ADR-0003: Minimal Data Collection

## Status

**Accepted** - This is a fundamental architectural decision that guides all data collection design.

## Context

Data minimization is a core principle of privacy by design and is required by regulations like GDPR and LGPD. The principle states that we should collect only the data that is:

- Necessary for the stated purpose
- Adequate for the purpose (not excessive)
- Relevant to the purpose
- Limited to what is needed

Many monitoring platforms collect excessive data "just in case" or for "future features." This creates:
- Privacy risks
- Compliance violations
- Storage costs
- Security exposure
- Trust issues

We need to decide on our data collection philosophy.

## Decision

**We will practice strict data minimization - collecting only the minimum data necessary for productivity analysis and compliance reporting.**

The platform will:

1. **Collect only necessary data** for stated purposes
2. **Aggregate data** when possible instead of storing granular events
3. **Exclude personal data** that is not necessary
4. **Delete data** when no longer needed
5. **Review data collection** regularly to ensure minimization
6. **Document data necessity** for each data point

## Consequences

### Positive

✅ **Privacy Protection**: Minimizes privacy exposure  
✅ **Compliance**: Aligns with GDPR, LGPD data minimization requirements  
✅ **Security**: Less data = less security exposure  
✅ **Cost Efficiency**: Reduced storage and processing costs  
✅ **Trust Building**: Demonstrates respect for privacy  
✅ **Legal Safety**: Reduces legal and compliance risks  

### Negative

❌ **Limited Analytics**: Some analytics may not be possible  
❌ **Future Limitations**: May limit future feature development  
❌ **Aggregation Challenges**: Aggregation may lose some detail  
❌ **Competitive Disadvantage**: Competitors may offer "more data"  

### Mitigation

- Focus on productivity metrics that don't require granular data
- Use aggregated analytics instead of raw event analysis
- Emphasize privacy as competitive advantage
- Regular review to balance privacy and utility
- Clear documentation of data necessity

## Implementation

### Data Collection Scope

**What We Collect:**
- Application usage (name, category, timestamp, duration)
- Window focus events (application, timestamp, duration)
- System state (idle/active, timestamp)
- Network activity volume (not content)
- Aggregated productivity metrics

**What We Do NOT Collect:**
- Keystrokes (see ADR-0001)
- Screen content
- File contents
- Personal communications
- Passwords
- Personal browsing
- Biometric data

### Data Aggregation

**Strategy:**
- Aggregate events into time periods (e.g., hourly, daily)
- Calculate metrics instead of storing raw events
- Store summaries for long-term retention
- Delete raw events after aggregation period

**Benefits:**
- Reduced storage
- Privacy protection
- Performance improvement
- Cost reduction

### Data Retention

**Policy:**
- Raw events: 90 days
- Daily aggregates: 1 year
- Monthly aggregates: 3 years
- Annual summaries: 7 years (for compliance)

**Enforcement:**
- Automated deletion jobs
- Retention policy enforcement
- Regular data purging
- Secure deletion

### Regular Review

**Process:**
- Annual review of data collection
- Assessment of data necessity
- Removal of unnecessary data points
- Documentation of decisions
- Privacy impact assessment

## Data Necessity Justification

### Application Usage Data

**Necessity:**
- Required for productivity analysis
- Required for time tracking
- Required for compliance reporting
- Cannot be derived from other data

**Minimization:**
- Only application name and category (not content)
- Only timestamps and duration (not detailed activity)
- Aggregated when possible

### Window Focus Events

**Necessity:**
- Required for activity tracking
- Required for productivity measurement
- Required for time distribution analysis

**Minimization:**
- Only application and duration (not window content)
- Aggregated analysis
- No sensitive content capture

### System State

**Necessity:**
- Required for productivity calculation
- Required for time tracking
- Required for activity patterns

**Minimization:**
- Only idle/active state (not detailed activity)
- Aggregated metrics
- Privacy-preserving

### Network Activity

**Necessity:**
- Required for network usage analysis
- Required for productivity correlation
- Required for resource monitoring

**Minimization:**
- Only volume metrics (not content)
- No URL tracking
- No packet inspection
- Aggregated analysis

## Privacy Impact

### Risk Reduction

- Less data = less privacy risk
- Aggregation reduces identifiability
- Minimization reduces exposure
- Regular deletion reduces risk

### User Trust

- Transparent data collection
- Clear necessity explanation
- User-accessible data
- Privacy-first approach

## Related Decisions

- [ADR-0001: No Keylogging](./0001-no-keylogging.md)
- [ADR-0002: Explicit Consent Required](./0002-explicit-consent-required.md)
- [Data Collection Boundaries](../diagrams/data-collection-boundaries.md)

## References

- [Privacy by Design](../docs/privacy-by-design.md)
- [Data Retention Policy](../docs/data-retention-policy.md)
- [Product Vision](../docs/product-vision.md)

---

**Date**: 2024  
**Deciders**: Icarus Nova Architecture Team  
**Status**: Accepted
