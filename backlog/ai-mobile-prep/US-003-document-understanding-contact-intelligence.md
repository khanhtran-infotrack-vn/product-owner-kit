# User Story: Document Understanding + Contact Intelligence

**Story ID**: US-003  
**Epic**: AI-Powered Document Preparation for Mobile  
**Priority**: HIGH  
**Status**: Ready for Development  
**Created**: February 6, 2026

---

## User Story

**As a** mobile user preparing a contract for signature  
**I want** the app to automatically extract signer names/roles from the document and match them to my contacts  
**So that** I don't have to manually assign signers and can send documents for signature in seconds

---

## Business Context

- **Problem**: After detecting fields, users still struggle with manually assigning signers and determining signing order
- **Opportunity**: Complete the end-to-end mobile workflow by automating signer assignment
- **User Impact**: Eliminates 3-5 minutes of manual data entry per document
- **Competitive Advantage**: First-to-market with contact intelligence + NLP document understanding on mobile

---

## Acceptance Criteria

### 1. Document Entity Extraction
- **Given** a user uploads a contract or agreement
- **When** the AI processes the document text (via OCR + NLP)
- **Then** the system extracts signer names with ≥85% accuracy
- **And** extracts roles/titles (e.g., "Buyer", "Seller", "Witness", "Employee") with ≥80% accuracy
- **And** identifies signing positions (e.g., "Party A", "Party B") with ≥75% accuracy

### 2. Contact Matching
- **Given** the AI has extracted names from the document
- **When** the system accesses the user's phone contacts (with permission)
- **Then** extracted names are automatically matched to contact entries
- **And** matches with ≥90% confidence are auto-populated
- **And** ambiguous matches (70-90% confidence) present suggestions for user confirmation
- **And** unmatched names allow user to search contacts or add manually

### 3. Signing Order Intelligence
- **Given** the AI has identified signer roles (e.g., "Manager", "Employee", "Witness")
- **When** determining signing order
- **Then** a logical sequence is suggested based on role hierarchy
- **And** common patterns are recognized (e.g., witness signs after primary parties)
- **And** user can reorder signers with drag-and-drop

### 4. Contact Information Population
- **Given** a contact has been matched or selected
- **When** the signer is added to the signing workflow
- **Then** name, email, and phone number are auto-populated from contact card
- **And** user can edit any field before sending
- **And** missing information (e.g., no email) triggers user prompt

### 5. Multi-Party Document Support
- **Given** a document with 3+ signing parties
- **When** processing the document
- **Then** all parties are correctly identified and extracted
- **And** duplicate names are handled intelligently (e.g., "John Smith" vs "John A. Smith")
- **And** supports documents with up to 10 unique signers

### 6. Privacy & Permissions
- **Given** the app needs access to phone contacts
- **When** the feature is first used
- **Then** a clear permission prompt explains why contact access is needed
- **And** user can deny permission and use manual entry instead
- **And** contacts are never uploaded to servers (processed on-device or anonymized)
- **And** user can revoke permissions at any time

### 7. Fallback & Error Handling
- **Given** the AI cannot extract names or roles with confidence
- **When** processing completes
- **Then** the system gracefully falls back to manual signer entry
- **And** a clear message explains what was unclear in the document
- **And** users can still use detected fields from US-001

---

## Definition of Done

### Development
- [ ] OCR engine integrated (Google ML Kit, Tesseract, or cloud API)
- [ ] NLP entity extraction model trained for name/role detection
- [ ] Contact access permissions implemented (iOS: Contacts framework, Android: Contacts Provider)
- [ ] Contact matching algorithm with fuzzy string matching
- [ ] Signing order logic implemented with role hierarchy rules
- [ ] Auto-population of signer details (name, email, phone)
- [ ] Manual override for all auto-detected information
- [ ] Unit tests for entity extraction and contact matching (≥85% coverage)
- [ ] Integration tests for full workflow

### Quality Assurance
- [ ] Tested on 100+ documents across 5+ contract types (NDA, employment, sales, real estate, service)
- [ ] Accuracy benchmarks met (≥85% name extraction, ≥80% role extraction)
- [ ] Contact matching tested with 50+ contact lists (small/medium/large)
- [ ] Edge cases tested (unusual names, missing contact info, multi-language documents)
- [ ] Privacy compliance validated (GDPR, CCPA considerations)
- [ ] Accessibility testing with screen readers

### Documentation
- [ ] API documentation for entity extraction endpoints
- [ ] Technical documentation for NLP model and contact matching logic
- [ ] User-facing help: "How contact intelligence works"
- [ ] Privacy policy update for contact access disclosure
- [ ] Analytics events for contact matching usage and accuracy

### Product
- [ ] Product Owner acceptance testing completed
- [ ] Legal/privacy review for contact data handling approved
- [ ] 10 beta users tested feature successfully
- [ ] User feedback on contact suggestions collected
- [ ] No P0 or P1 bugs remaining
- [ ] Feature flag configured for gradual rollout

---

## Dependencies

### Technical Dependencies
- **OCR Engine**: Google ML Kit, AWS Textract, Azure Computer Vision, or Tesseract
- **NLP Model**: Named Entity Recognition (NER) model for legal/contract documents
- **Contact API**: iOS Contacts framework / Android Contacts Provider
- **Fuzzy Matching Library**: Python `fuzzywuzzy` or JavaScript `fuse.js` equivalent

### Feature Dependencies
- **Parallel with US-001**: Can be developed in parallel with Computer Vision Field Detection
- **Integrates with US-001**: Combines field locations (US-001) with signer assignments (US-003)
- **Enables**: One-Tap Scan & Prep orchestration (Phase 1)

### External Dependencies
- **Legal/Privacy Review**: Approval for contact data access and handling
- **Platform Permissions**: iOS/Android contact permission flows
- **Design Team**: UX for contact matching suggestions and signing order UI

---

## Estimated Effort

### Story Points: 8 (Medium-Large)

### Breakdown by Discipline:
- **NLP/ML Engineering**: 3 weeks
  - OCR integration and testing: 1 week
  - NER model training for contract entities: 1.5 weeks
  - Contact matching algorithm: 0.5 week
  
- **Backend Engineering**: 1 week
  - Entity extraction API endpoints: 3 days
  - Signing order logic: 2 days
  
- **Mobile Engineering**: 2 weeks
  - iOS contact permission and access: 3 days
  - Android contact permission and access: 3 days
  - Contact matching UI and auto-population: 3 days
  - Signing order management UI: 2 days
  - Manual override flows: 2 days
  
- **QA**: 1 week
  - Test plan and edge case testing
  - Privacy/security testing

**Total Estimated Time**: 4-6 weeks (as per brainstorm summary)

---

## Technical Notes

### NLP Approach - Entity Extraction
- **OCR**: Extract all text from document pages
  - Options: Google ML Kit (on-device), AWS Textract, Azure Computer Vision
  - Required accuracy: ≥95% character accuracy
  
- **Named Entity Recognition (NER)**:
  - Model: Fine-tuned BERT, spaCy NER, or custom model trained on legal documents
  - Entities to extract:
    - PERSON (names of signers)
    - ROLE (titles like "Buyer", "Seller", "Manager", "Employee")
    - ORG (company names, if needed for B2B contracts)
  - Training data: Annotated contracts (in-house or synthetic)

- **Role Hierarchy Logic**:
  ```
  High authority: CEO, President, Director, Manager
  Medium authority: Employee, Contractor, Buyer, Seller
  Low authority (last): Witness, Notary
  ```

### Contact Matching Algorithm
- **Fuzzy String Matching**: Use Levenshtein distance to match extracted names to contact names
- **Confidence Scoring**:
  - Exact match: 100%
  - High similarity (≥90%): Auto-suggest
  - Medium similarity (70-89%): Present options
  - Low similarity (<70%): Require manual search
  
- **Privacy**: 
  - Option 1 (Preferred): On-device matching (contacts never leave device)
  - Option 2: Hash contact names before sending to cloud for matching
  - Never store raw contact data on servers

### Mobile Contact Access
- **iOS**: Use `Contacts` framework
  ```swift
  import Contacts
  let store = CNContactStore()
  store.requestAccess(for: .contacts) { granted, error in ... }
  ```
  
- **Android**: Use `ContactsContract` API
  ```kotlin
  val permission = Manifest.permission.READ_CONTACTS
  ActivityCompat.requestPermissions(...)
  ```

### Analytics Events
- `document_entities_extracted`: Count of successful extractions
- `contact_match_success`: % of names auto-matched
- `contact_match_confirmed`: User confirmed AI suggestion
- `contact_match_rejected`: User rejected AI suggestion
- `signing_order_modified`: User changed AI-suggested order

---

## Success Metrics (KPIs)

### Primary Metrics
- **Entity Extraction Accuracy**: ≥85% for names, ≥80% for roles (measured on test set)
- **Contact Match Success Rate**: ≥70% of extracted names auto-matched to contacts
- **Time Savings**: 60% reduction in signer assignment time (from 3-5 min to <2 min)

### Secondary Metrics
- **Feature Adoption**: 80%+ of users grant contact permission
- **User Acceptance**: 90%+ of auto-matched contacts are accepted without modification
- **Signing Order Accuracy**: 85%+ of suggested signing orders are kept unchanged

### Business Impact
- **Document Prep Completion Rate**: 80% of users complete prep without abandoning
- **Mobile-to-Desktop Switch Rate**: 70% reduction when combined with US-001
- **User Satisfaction**: 4.5+ rating on "assigning signers is easy" survey question

---

## INVEST Validation

✅ **Independent**: Can be developed in parallel with US-001 (field detection), integrates at workflow level  
✅ **Negotiable**: Entity extraction accuracy targets and contact matching thresholds can be adjusted based on feasibility  
✅ **Valuable**: Eliminates manual signer assignment, completes the AI-powered workflow vision  
✅ **Estimable**: Clear scope with 4-6 week estimate and defined NLP/contact integration work  
✅ **Small**: Fits within 2-3 sprint cycles (assuming 2-week sprints)  
✅ **Testable**: Clear acceptance criteria with measurable extraction accuracy and user acceptance rates

---

## Notes & Risks

### Risks
1. **Entity Extraction Accuracy Risk**: NER may struggle with non-standard contract formats
   - **Mitigation**: Train on diverse document types, provide manual override fallback
   
2. **Contact Permission Denial Risk**: Users may be hesitant to grant contact access
   - **Mitigation**: Clear permission prompt explaining value, manual entry as alternative
   
3. **Name Matching Ambiguity Risk**: Multiple contacts with similar names (e.g., "John Smith")
   - **Mitigation**: Show all matches with confidence scores, let user choose
   
4. **Multi-Language Documents Risk**: NER trained on English may fail on other languages
   - **Mitigation**: Start with English-only, expand to other languages in Phase 2

### Privacy Considerations
- **Minimize Data Collection**: Only access contact names/emails, not full contact card
- **On-Device Processing**: Preferred approach to avoid uploading contacts to cloud
- **User Transparency**: Clear messaging about how contacts are used
- **Opt-Out Option**: Always provide manual signer entry as alternative

### Open Questions
- [ ] On-device NER vs cloud API for entity extraction?
- [ ] Which OCR engine provides best accuracy/cost tradeoff?
- [ ] Should we support multiple languages in MVP or start with English only?
- [ ] How to handle corporate contacts (e.g., signer is an organization)?
- [ ] Should we learn from user corrections to improve matching over time?

---

## Related Stories

- **US-001**: Computer Vision Field Detection (parallel development, integrates at workflow level)
- **US-002**: Confidence Scores + Visual Indicators (dependent on US-001)
- **Future**: Template Auto-Selection (Phase 2) - could pre-populate expected roles
- **Future**: One-Tap Scan & Prep (Phase 1) - orchestrates US-001, US-002, US-003
- **Future**: AI Apprentice Mode (Phase 3) - learns user's frequent contacts

---

## User Experience Flow

```
1. User uploads/scans contract document
   ↓
2. AI detects signature fields (US-001) + extracts names/roles (US-003)
   ↓
3. [First time] Permission prompt: "Access contacts to auto-assign signers?"
   ↓
4. If granted: AI matches extracted names to phone contacts
   ↓
5. Display signer assignment screen:
   - Field 1: "Seller" → [Auto-matched] John Doe (john@example.com) ✓
   - Field 2: "Buyer" → [Suggested] Jane Smith (jane@example.com) - Tap to confirm
   - Field 3: "Witness" → [No match] - Search contacts or enter manually
   ↓
6. Suggested signing order: John Doe → Jane Smith → Witness
   ↓
7. User reviews, confirms, or edits
   ↓
8. Tap "Send for Signature"
```

---

## Acceptance Testing Scenarios

### Scenario 1: Perfect Match
- **Given**: Document with "John Smith" needs to sign, user has contact "John Smith"
- **Expected**: Auto-matched, name/email populated, user taps confirm and sends

### Scenario 2: Ambiguous Match
- **Given**: Document has "John Smith", user has 3 contacts with similar names
- **Expected**: Show all 3 options with confidence scores, user selects correct one

### Scenario 3: No Contact Match
- **Given**: Document has "Alice Johnson", not in user's contacts
- **Expected**: Show "No match found", allow search or manual entry

### Scenario 4: Multi-Party Document
- **Given**: Real estate contract with Buyer, Seller, Agent, Witness (4 parties)
- **Expected**: All 4 extracted, auto-matched where possible, logical signing order suggested

### Scenario 5: Contact Permission Denied
- **Given**: User denies contact access permission
- **Expected**: Graceful fallback to manual entry, no app crash or error

---

## References

- Brainstorm Summary: brainstorm/ai-mobile-document-prep/SUMMARY.md:68-80
- User Research Q1 2025 - Finding 1: Mobile Signing Friction
- User Research Q1 2025 - Finding 4: Users Want AI Assistance
- Product Vision - Strategic Goal: "Mobile-first AI experience"
