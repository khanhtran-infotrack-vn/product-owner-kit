# eSign Domain Knowledge Reference

## Electronic Signature Types

### Simple Signature
- Basic e-signature (checkbox, typed name)
- No cryptographic verification
- Suitable for low-risk transactions
- Examples: Clicking "I agree", typing name in a form

### Advanced Signature
- Certificate-based, cryptographic
- Links signature to signer uniquely
- Detects tampering
- Requires certificate from trusted provider
- Use cases: Business contracts, financial documents

### Qualified Signature
- Highest level under eIDAS
- Government-issued certificates
- Legally equivalent to handwritten signature
- Requires qualified signature creation device
- Use cases: Legal documents, government forms, high-value transactions

## Compliance Frameworks

### eIDAS (EU)
- Electronic Identification and Trust Services Regulation
- Three signature levels: Simple, Advanced, Qualified
- Trust service providers must be qualified by member states
- Cross-border recognition required
- Audit trail requirements
- Timestamp requirements (RFC 3161)

### ESIGN Act (US)
- Electronic Signatures in Global and National Commerce Act
- Validates electronic signatures and records
- Requirements:
  - Intent to sign
  - Consent to electronic transactions
  - Record retention
  - Accurate representation

### UETA (US)
- Uniform Electronic Transactions Act
- State-level implementation
- Similar to ESIGN but focused on interstate commerce
- Defines electronic signature validity

### 21 CFR Part 11 (FDA)
- Pharmaceutical and medical device regulations
- Requirements for:
  - Electronic signatures must be unique
  - Biometric and non-biometric methods
  - Two-factor authentication for critical operations
  - Audit trails with timestamps

### GDPR
- Data protection and privacy
- Requirements for eSign:
  - Consent for processing personal data
  - Right to erasure (with exceptions for legal documents)
  - Data minimization
  - Encryption requirements
  - Breach notification

## Signature Workflows

### 1. Simple Signing
- Single signer, one document
- Steps: Upload → Place fields → Send → Sign → Complete

### 2. Sequential Signing
- Multiple signers in specific order
- Workflow: Signer 1 → Signer 2 → Signer 3
- Each signer receives document after previous completes

### 3. Parallel Signing
- Multiple signers, any order
- All receive document simultaneously
- Complete when all have signed

### 4. Delegation
- Original signer delegates to another person
- Maintains audit trail of delegation
- Delegatee signs on behalf of delegator

### 5. In-Person Signing
- Face-to-face signing ceremony
- Witness may be required
- Host guides signer through process
- Higher assurance level

## Audit Trail Requirements

Required elements for legally valid audit trails:

### Identity Verification
- Authentication method used (email, SMS, ID verification)
- User credentials and verification timestamp
- Multi-factor authentication records

### Document Integrity
- Document hash/checksum (SHA-256 or stronger)
- Hash calculated before and after signing
- Detection of any modifications

### Timestamps
- RFC 3161 compliant timestamps
- From trusted timestamp authority
- Applied to each significant event

### Metadata
- IP address and geolocation
- Device information (browser, OS)
- Signature certificate chain
- Certificate validation status

### Event Log
- Document uploaded
- Fields placed
- Invitation sent
- Document opened
- Document signed
- Document completed
- Any rejections or declines

### Consent Records
- Terms of service acceptance
- Electronic signature consent
- Data processing consent (GDPR)

## PDF Technical Standards

### PDF/A (Archival)
- **PDF/A-1**: Based on PDF 1.4, basic archival
- **PDF/A-2**: Based on PDF 1.7, improved features
- **PDF/A-3**: Allows file attachments
- **Requirements**:
  - Self-contained (all fonts embedded)
  - No encryption
  - No external dependencies
  - Device-independent rendering

### PAdES (Advanced Electronic Signatures)
- **PAdES-B**: Basic signature with certificate
- **PAdES-T**: With timestamp from TSA
- **PAdES-LT**: Long-term validation data included
- **PAdES-LTA**: Long-term archival with periodic timestamps
- Signature validation:
  - Certificate chain validation
  - Revocation checking (OCSP/CRL)
  - Timestamp validation

### Field Types for eSigning

**Signature**: Main signature capture
- Visual representation
- Certificate-based or biometric
- Mandatory fields

**Initial**: Abbreviated signature
- Used for page acknowledgment
- Smaller visual representation

**Date**: Auto-filled signing date
- Timestamp of signature application
- Cannot be manually altered

**Text**: Signer-entered text
- Name, title, company
- Free-form input

**Checkbox**: Agreement confirmation
- Yes/no acceptance
- Initial terms agreement

**Attachment**: Upload supporting docs
- ID documents
- Supporting evidence
- Additional contracts

## Integration Patterns

### Common eSign API Providers

#### DocuSign
- Market leader
- Extensive REST API
- Features: Templates, bulk send, webhooks
- Compliance: eIDAS, ESIGN, UETA

#### Adobe Sign
- Enterprise focus
- PDF expertise and native integration
- Features: Workflows, mega sign
- Strong compliance certifications

#### HelloSign/Dropbox Sign
- Developer-friendly API
- Simple integration
- Embedded signing flows

#### PandaDoc
- Document + payment workflows
- Proposal and contract focus
- CRM integrations

### Interoperability Considerations

```markdown
| Feature | DocuSign | Adobe Sign | Custom System |
|---------|----------|------------|---------------|
| REST API | ✓ | ✓ | ✓ |
| Webhooks | ✓ | ✓ | ✓ |
| Templates | ✓ | ✓ | ✓ |
| Bulk send | ✓ | ✓ | Planned |
| Advanced signatures | ✓ | ✓ | ✓ |
| Qualified signatures | Via partners | Via partners | eIDAS compliant |
```

## Use Cases

### Contract Management
1. Sales rep uploads contract template
2. Auto-tag detects signature blocks
3. Client info auto-fills from CRM
4. Sequential routing: Manager → Legal → Client
5. Signed contract archived with audit trail
6. CRM updated with signed contract link

### HR Onboarding
1. HR uploads offer letter, I-9, W-4, handbook
2. Multiple signature fields auto-detected
3. Parallel signing: Employee + Manager + HR
4. Documents stored in employee record
5. Compliance reporting generated

### Real Estate Transaction
1. Escrow officer uploads disclosure forms
2. Auto-tag identifies seller/buyer signature zones
3. In-person signing with notary witness
4. Qualified signature for legal validity
5. County recorder integration for filing

## Regulatory Updates to Monitor

### Recent Changes (2025-2026)
- eIDAS 2.0 implementation timeline
- ESIGN Act modernization proposals
- State-level digital signature laws (various US states)
- GDPR enforcement priorities
- Sector-specific requirements (healthcare, finance)
