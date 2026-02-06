# Brainstorming Session: AI-Powered Document Preparation for Mobile

**Date**: February 6, 2026
**Facilitator**: Feature Brainstormer Agent
**Context**: HIGH priority feature based on user research - 35% of signatures on mobile, users frustrated with document preparation experience

---

## Context Summary
- **Current Pain**: 62% of mobile users switch to desktop for document preparation
- **Key Insight**: Users want AI to auto-detect signature fields and streamline mobile document prep
- **User Quote**: "The mobile app feels like an afterthought. I can sign, but preparing documents is painful."
- **Business Impact**: Mobile users 2.3x more likely to abandon signing process

---

## Brainstorming Technique 1: SCAMPER

### Substitute
**S1. Replace Manual Field Placement with Computer Vision**
Use ML model trained on millions of documents to detect where signatures, dates, initials typically appear. Mobile camera takes photo of document, AI instantly places fields.

**S2. Voice Instead of Touch**
"Hey SignApp, add a signature field for John Doe here" - use voice commands to place fields hands-free. Ideal for on-site scenarios (real estate showings, client meetings).

**S3. Template Auto-Selection Instead of Manual Choice**
AI analyzes document content and automatically suggests the best template. "This looks like an NDA, applying your standard NDA template."

### Combine
**C1. Camera + AI + Guided Workflow**
Point phone camera at paper document → AI detects document type → Suggests signer workflow → Converts to digital with fields already placed.

**C2. Document Understanding + Contact Intelligence**
AI reads contract, extracts names/roles ("Buyer", "Seller"), auto-matches to contacts in phone, suggests signing order based on role hierarchy.

**C3. Offline AI + Cloud Sync**
On-device ML model for instant field detection even without internet. Syncs to cloud when connected for advanced features.

### Adapt
**A1. Instagram Story-Style Document Prep**
Swipe-based interface: Take photo → Swipe to place signature → Swipe to add date → Swipe to review → Send. Familiar mobile UX pattern.

**A2. Adapt Gaming "Snap to Grid" for Field Placement**
Fields automatically snap to detected text blocks. Haptic feedback when field aligns. Makes touch-based placement precise on small screens.

**A3. Smart Compose from Gmail**
AI suggests next field to add based on document type and context. "Looks like you need a date field next to this signature."

### Modify
**M1. Change Document Upload to "Scan & Prep"**
Single button that: Scans document → Detects fields → Suggests signers → Ready to send. One-tap document preparation.

**M2. Progressive Enhancement for Field Detection**
Start with high-confidence fields auto-placed. Show suggestions for medium-confidence. Let user manually add low-confidence areas.

**M3. Turn Static Preview into Interactive AR**
Hold phone over paper document, AR overlay shows where digital signature fields will appear. "Point and shoot" to finalize.

### Put to Other Uses
**P1. Use Field Detection for Contract Review**
Same AI that detects signature fields could highlight key terms, risks, or missing clauses. "This NDA is missing a confidentiality term definition."

**P2. Repurpose for Bulk Document Prep**
Upload 50 employee contracts → AI detects all signature fields across all docs → Bulk apply template → Send to everyone.

**P3. Use Document Intelligence for Analytics**
AI that reads documents could extract metadata: contract value, parties, dates. Auto-populate custom fields for reporting.

### Eliminate
**E1. Remove Need to "Place Fields"**
AI is so good that users never manually place fields. Just: Upload → Review AI suggestions → Send.

**E2. Eliminate Document Type Selection**
AI automatically detects document category (NDA, employment agreement, lease) without user input.

**E3. Remove "Prepare" vs "Sign" Mode Distinction**
Unified experience: AI detects if you're the signer or sender, adapts interface accordingly.

### Reverse/Rearrange
**R1. Signer-First Preparation**
Instead of sender preparing doc, AI guides signer through filling fields in optimal order. "Sign here, then here, then date."

**R2. Start with Complete AI Draft, Let User Edit Down**
AI creates "maximal" field placement (every possible field). User removes what's unnecessary. Faster than building up.

**R3. Preparation Happens During Upload**
Processing bar becomes prep bar: "Uploading... Detecting fields... Placing signatures... Ready!" Document prepared before upload completes.

---

## Brainstorming Technique 2: "How Might We" Questions

### HMW #1: Make document prep faster than ordering coffee?
**Idea 1A. Prep-in-Progress**
Document prepares in background while user does other tasks. Push notification: "Your contract is ready to send."

**Idea 1B. Pre-Prep Based on Calendar**
AI sees "Client meeting at 2pm" in calendar, asks "Want me to prep the standard sales contract for your meeting?" One-tap confirm.

**Idea 1C. Shortcuts Integration (iOS)**
Siri Shortcut: "Prep my NDA" → Automatically creates document from template, ready to assign signers.

### HMW #2: Make mobile prep better than desktop?
**Idea 2A. Location-Aware Smart Defaults**
At office: Full control, all options. On-site with client: Streamlined, smart defaults, quick send. AI adapts to context.

**Idea 2B. Gesture-Based Power Features**
Shake phone to undo, pinch to zoom to field, swipe three fingers to duplicate fields. Power users stay on mobile.

**Idea 2C. Mobile-First AI Features**
Features that ONLY work on mobile: Camera scan, AR preview, voice commands, location context, contact integration.

### HMW #3: Help users trust AI field detection?
**Idea 3A. Confidence Scores + Visual Indicators**
Green checkmark for 95%+ confidence, yellow for 70-95%, red for <70%. Users know where to review carefully.

**Idea 3B. "AI Apprentice" Mode**
First 5 documents: AI suggests, user approves, AI learns from corrections. After training period, AI works autonomously.

**Idea 3C. Explain Why**
Tap any AI-placed field to see: "I placed this signature field here because it appears next to 'Signature:' and is at the bottom of page 3, consistent with 98% of contracts."

### HMW #4: Support users in low-connectivity scenarios?
**Idea 4A. Smart Offline Queue**
Prep documents offline, they queue for sending. AI predicts when you'll be online, optimizes send timing.

**Idea 4B. Lite Mode**
Reduced-quality document processing that works on poor connections. "Processing in lite mode, will enhance when online."

**Idea 4C. Offline-First ML Models**
Core field detection runs entirely on device. Advanced features (document understanding, routing suggestions) require connection.

### HMW #5: Reduce cognitive load during document prep?
**Idea 5A. Wizard Mode for Complex Documents**
"I'll guide you through this step-by-step." Multi-screen flow with progress bar. Each screen: one decision.

**Idea 5B. Smart Defaults Everywhere**
Every setting has an AI-suggested default. Users can accept default or customize. "Most users send this document to 2 signers in sequential order."

**Idea 5C. Natural Language Input**
Text field: "Send to John Smith and Jane Doe for signatures, then Mary Johnson for final approval." AI parses and configures workflow.

---

## Brainstorming Technique 3: Crazy 8s (Rapid Ideation)

**Idea C1. Holographic Document Preview**
Use phone's depth sensor to create 3D holographic preview of document floating above desk. Place fields in 3D space.

**Idea C2. Collaborative Prep Mode**
Two people on-site, both open app, shake phones together to pair. Collaborate on document prep in real-time.

**Idea C3. AI Negotiation Assistant**
AI analyzes contract terms, suggests modifications: "Buyers typically negotiate payment terms. Suggest 60-day net instead of 30?"

**Idea C4. Biometric Field Assignment**
"Place your thumb here" → Phone captures thumbprint → Assigns signature field to that person based on biometric ID.

**Idea C5. Smart Document Assembly**
"I need an NDA with non-compete clause" → AI assembles custom document from clause library, pre-populated with fields.

**Idea C6. Real-Time Translation + Signing**
Document in English, signer speaks Spanish. AI translates, shows bilingual version, captures legally-binding signature.

**Idea C7. Document Health Score**
AI rates document: "This contract has 3 potential legal issues, missing 2 standard clauses, and unclear payment terms. Score: 6/10."

**Idea C8. Predictive Send Timing**
"Based on analysis of 10,000 similar contracts, send this on Tuesday at 10am for 23% higher completion rate."

---

## Brainstorming Technique 4: Analogies & Metaphors

### Analogy 1: Document Prep as Photo Editing
**Idea A1. Filter-Style Templates**
Apply template to document like applying Instagram filter. Instantly see what document looks like with fields placed.

**Idea A2. Auto-Enhance Button**
One button that applies AI improvements: optimal fields, smart routing, best practices. Like "Auto" button in photo apps.

**Idea A3. Before/After Slider**
Slide to compare raw document vs AI-prepared version. Visual confidence builder.

### Analogy 2: Document Prep as Navigation (GPS)
**Idea A4. Turn-by-Turn Document Guidance**
"In 2 pages, add signature field" → "Add signature field here" → "Next, add date field" → "You've arrived! Document ready to send."

**Idea A5. Route Options**
AI suggests multiple preparation approaches: "Fastest route (2 fields, 1 signer)", "Most thorough route (8 fields, 3 signers)", "Recommended route (5 fields, 2 signers)."

**Idea A6. Traffic-Style Bottleneck Warnings**
"This signing workflow typically takes 5 days due to bottleneck at approver stage. Suggest parallel approval to reduce to 2 days?"

### Analogy 3: Document Prep as Online Shopping
**Idea A7. One-Click Send**
Saved "checkout" profiles for common scenarios. "Send NDA to vendor" is literally one tap.

**Idea A8. Frequently Bought Together**
"Users who add signature field also add date field and initial field." AI suggests related fields.

**Idea A9. Save for Later**
Partially-prepped documents auto-save. Return anytime to finish. "You have 3 documents in draft."

---

## Brainstorming Technique 5: Reverse Thinking

### What would make mobile doc prep WORSE?
- Make user place every field manually with tiny touch targets
- Require 10-step setup before uploading document
- Force landscape mode only
- No offline support
- Require typing email addresses manually

### Now flip it to make it BETTER:
**Idea RT1. Zero-Touch Field Placement**
AI places all fields automatically. User interaction is only to review/approve. "Tap anywhere to see details, tap checkmark to approve."

**Idea RT2. Single-Screen Document Prep**
Everything fits on one screen: document preview, field list, signer assignment, send button. No scrolling, no navigation.

**Idea RT3. Portrait-First Design**
Every feature optimized for one-handed, portrait-mode use. Can prep entire document with thumb.

**Idea RT4. Offline-First Architecture**
App assumes you're offline. All core features work without connection. Syncs opportunistically.

**Idea RT5. Contact Integration Everywhere**
Never type an email. All signers come from phone contacts, recent signers, or AI suggestions.

---

## Brainstorming Technique 6: User Journey Mapping

### Critical Moments in Mobile Document Prep Journey

**Moment 1: Initial Upload**
Current: User must choose photo/file, navigate file system
**Ideas**:
- **UJ1**: Quick Actions widget on home screen: "Scan Document" launches directly to camera
- **UJ2**: Share sheet integration: Share PDF from any app → Prep in SignApp
- **UJ3**: Apple Watch complication: "Prep Last Document" for instant access

**Moment 2: Field Detection**
Current: User manually places each field
**Ideas**:
- **UJ4**: Instant detection: Fields appear during document upload progress bar
- **UJ5**: Interactive tutorial: First-time users see "AI found 4 signature spots. Tap to review."
- **UJ6**: Confidence animation: Fields fade in with certainty - high confidence appear solid, low confidence pulsate

**Moment 3: Signer Assignment**
Current: Manual email entry
**Ideas**:
- **UJ7**: Smart contact suggestions: "This looks like a vendor contract. Send to Sarah (Procurement)?"
- **UJ8**: Bump to share: Physical phone bump transfers signer info between devices
- **UJ9**: Role-based assignment: Label fields as "Buyer" and "Seller", AI maps to contacts based on role history

**Moment 4: Review Before Send**
Current: Users uncertain if setup is correct
**Ideas**:
- **UJ10**: AI Pre-Flight Check: "✓ All required fields assigned, ✓ Signing order logical, ✓ Expiration date set"
- **UJ11**: Preview as Signer: "See what John will see when he receives this"
- **UJ12**: Completion Probability: "Based on similar documents, 87% likely to be signed within 2 days"

**Moment 5: Send & Track**
Current: No visibility after sending
**Ideas**:
- **UJ13**: Smart notifications: "John opened the document 2 minutes ago" with option to "Send him a quick message"
- **UJ14**: Live Activity (iOS): Signing progress visible on lock screen
- **UJ15**: Proactive suggestions: "Document has been pending for 3 days. Send reminder? [Yes] [No]"

---

## Wild Card Ideas (High Risk, High Reward)

**W1. AI Document Lawyer**
Built-in legal AI that reviews contracts for red flags, suggests clauses, warns about risky terms. Premium feature for legal teams.

**W2. Blockchain Signature Verification**
Every signature recorded on blockchain for immutable proof. Marketing angle: "More secure than DocuSign."

**W3. Document Comparison AI**
Upload two versions of contract, AI highlights every change, explains impact: "Payment terms changed from 30 to 60 days, impacts cash flow."

**W4. Multi-Document Intelligence**
AI finds patterns across all your contracts: "You're offering 30-day payment terms to Enterprise clients but 60-day to SMB. Consider standardizing."

**W5. Voice-Memo to Contract**
Record voice memo explaining deal terms → AI generates contract draft → Review and send. "Sales teams can create contracts while driving home."

**W6. AR Room Scanning**
Scan office with phone, AI detects all paper documents, creates digital signing queue: "Found 12 unsigned contracts on your desk. Want me to process them?"

**W7. Signing Party Mode**
Multiple people in room need to sign, AI detects faces, assigns signature fields, guides each person through signing in turn. Conference room scenario.

**W8. Smart Document Expiration**
AI predicts when unsigned document should be cancelled vs extended based on communication patterns, historical data, signer relationship.

---

## Ideas Organized by User Need

### Need: Speed (Fastest Possible Prep)
- S1: Computer Vision Field Detection
- R3: Prep During Upload
- E1: Eliminate Manual Field Placement
- UJ1: Quick Actions Widget
- UJ4: Instant Detection During Upload

### Need: Accuracy (Trustworthy AI)
- M2: Progressive Enhancement with Confidence Levels
- 3A: Confidence Scores + Visual Indicators
- 3B: AI Apprentice Mode
- 3C: Explainable AI
- UJ10: AI Pre-Flight Check

### Need: Convenience (Minimal Effort)
- S2: Voice Commands
- C2: Document Understanding + Contact Intelligence
- 1C: Siri Shortcuts
- 5A: Wizard Mode
- RT1: Zero-Touch Field Placement

### Need: Context Awareness (Smart Defaults)
- S3: Template Auto-Selection
- 2A: Location-Aware Smart Defaults
- 1B: Calendar-Based Pre-Prep
- UJ7: Smart Contact Suggestions
- A8: Frequently Bought Together

### Need: Offline Support
- C3: Offline AI + Cloud Sync
- 4A: Smart Offline Queue
- 4C: Offline-First ML Models
- RT4: Offline-First Architecture

### Need: Mobile-Native Experience
- A1: Instagram Story-Style UX
- A2: Snap to Grid
- 2B: Gesture-Based Power Features
- RT3: Portrait-First Design
- UJ13: Live Activity

---

## Total Ideas Generated: 65+

### Breakdown by Category:
- **AI/ML Powered**: 28 ideas
- **UX/Interface**: 18 ideas
- **Mobile-Native Features**: 12 ideas
- **Workflow/Automation**: 7 ideas
- **Wild Card/Future**: 8 ideas

### Breakdown by Technique:
- SCAMPER: 18 ideas
- How Might We: 15 ideas
- Crazy 8s: 8 ideas
- Analogies: 9 ideas
- Reverse Thinking: 5 ideas
- User Journey: 15 ideas
- Wild Cards: 8 ideas

---

## Next Steps
1. Evaluate ideas across dimensions (User Value, Business Impact, Feasibility, Effort)
2. Select top 10-15 ideas for deeper exploration
3. Create rough prioritization matrix
4. Recommend ideas for immediate prototyping
5. Identify ideas requiring further user validation
