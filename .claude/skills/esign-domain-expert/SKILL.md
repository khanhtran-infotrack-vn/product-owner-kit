---
name: esign-domain-expert
description: Specialized eSign product domain knowledge including electronic signature types (Simple, Advanced, Qualified), compliance frameworks (eIDAS, ESIGN Act, UETA, GDPR, 21 CFR Part 11), signature workflows, PDF standards (PDF/A, PAdES), audit trail requirements, and regulatory compliance. Use for compliance validation, security requirements, workflow design, or integration patterns related to electronic signature products.
---

# eSign Domain Expert

## Core Expertise

### Electronic Signature Types
- **Simple**: Basic e-signature (checkbox, typed name)
- **Advanced**: Certificate-based, cryptographic
- **Qualified**: Highest level, government-issued certificates (eIDAS)

### Compliance Validation

When reviewing features for compliance:

```markdown
## Compliance Assessment: [Feature Name]

### eIDAS Requirements
✓ [Requirement met]
⚠ [Needs attention]
✗ [Missing/not compliant]

### ESIGN Act Requirements
✓ [Requirement met]
⚠ [Needs validation]

### Data Protection (GDPR)
✓ [Compliant aspect]
⚠ [Requires consent flow update]

### Recommendations
1. [Action item with priority]
2. [Legal review needed for...]
```

### Security Requirements Checklist

```markdown
## Security Checklist: [Feature Name]

**Authentication:**
- [ ] Multi-factor authentication for high-value docs
- [ ] Session timeout after inactivity
- [ ] Strong password requirements

**Authorization:**
- [ ] Role-based access control (RBAC)
- [ ] Document-level permissions
- [ ] Field-level access control

**Data Protection:**
- [ ] Encryption at rest (AES-256)
- [ ] Encryption in transit (TLS 1.3)
- [ ] Secure key management (HSM/KMS)
- [ ] PII masking in logs

**Audit:**
- [ ] Comprehensive audit logging
- [ ] Tamper-evident log storage
- [ ] Log retention policy (7 years typical)
- [ ] SIEM integration

**Compliance:**
- [ ] SOC 2 Type II certification
- [ ] Regular penetration testing
- [ ] Vulnerability scanning
- [ ] Incident response plan
```

## Reference Files

For detailed domain knowledge, see:
- **[domain-knowledge.md](references/domain-knowledge.md)**: Complete reference on signature types, compliance frameworks (eIDAS, ESIGN, UETA, GDPR, 21 CFR Part 11), workflows, audit trail requirements, PDF standards (PDF/A, PAdES), integration patterns, use cases, and regulatory updates

## When to Use This Skill

- Validating feature compliance with eSign regulations
- Designing signature workflows (simple, sequential, parallel, delegation, in-person)
- Defining audit trail requirements
- Selecting appropriate signature types for use cases
- Reviewing security requirements for eSign features
- Understanding PDF technical standards
- Planning integration with eSign providers (DocuSign, Adobe Sign, HelloSign)
- Assessing regulatory impacts of feature changes
