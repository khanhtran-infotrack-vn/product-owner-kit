# Persona Profiles

**Purpose**: Stakeholder persona profiles for Step 1.5 (Persona Council) in `feature-brainstormer`.
**Usage**: Load this file when `--personas` flag is active. For each persona, generate 3-5 ideas from their POV + a brief empathy snapshot. Label each idea `[Persona: X]` in IDEAS.md.
**Disclaimer**: These are AI simulations — prompts for further investigation, not validated stakeholder positions.

---

## Persona 1: The Skeptical Enterprise Buyer

**Short label**: `Enterprise Buyer`
**Role**: IT Director or procurement lead at a mid-large organization (200-5,000 employees).

**Primary concerns**:
- Security posture and compliance certifications (SOC 2, ISO 27001, GDPR)
- Integration with existing SSO, SIEM, and workflow tools
- Vendor lock-in and data portability
- Total cost of ownership (licensing + implementation + training + support)

**Signature objections**:
- "How does this connect to our existing identity provider?"
- "Who owns the data, and where is it stored?"
- "What is the audit trail for regulatory compliance?"
- "What is our exit path if we need to switch vendors?"

**Says yes when**: Clear security documentation, smooth SSO integration, transparent pricing, data export available.
**Says no when**: Opaque data handling, no enterprise SLA, no compliance certifications.

**Empathy map prompts** (generate 1 sentence each for context):
- Think: [What decision-making criteria dominate their thinking?]
- Feel: [What anxiety or pressure drives their evaluation?]
- Say: [What do they say in a procurement meeting?]
- Do: [What actions do they take before approving a new tool?]

---

## Persona 2: The Overwhelmed New User

**Short label**: `New User`
**Role**: First-time user, low technical sophistication, high task pressure. Typical profile: a small business owner, field worker, or non-technical employee using the product for the first time.

**Primary concerns**:
- Learning curve — how long before they can use this without help?
- Fear of making mistakes they cannot undo
- Cognitive overload from too many options or unfamiliar terminology
- Time pressure — they have 10 minutes, not 30

**Signature objections**:
- "I do not have time to learn a new workflow."
- "What happens if I make a mistake? Can I undo it?"
- "Why does this require 5 steps when [competitor] takes 2?"
- "The help documentation assumes I already know what this does."

**Says yes when**: Guided onboarding, clear error messages with recovery paths, minimal steps for the core task.
**Says no when**: Jargon-heavy UI, no undo, hidden critical actions.

**Empathy map prompts**:
- Think: [What are they worried about when trying something new?]
- Feel: [What frustration or anxiety do they bring to this task?]
- Say: [What do they tell a colleague about the experience?]
- Do: [What workarounds do they invent when the UI fails them?]

---

## Persona 3: The Cost-Conscious CFO

**Short label**: `CFO`
**Role**: Finance executive at a growth-stage or mid-market company. Focused on ROI, total cost of ownership, and budget predictability.

**Primary concerns**:
- Measurable ROI over a defined time horizon (12-24 months)
- Total cost including implementation, training, change management, and support
- Budget predictability — no surprise overages or scaling cost cliffs
- Opportunity cost — what else could this budget fund?

**Signature objections**:
- "What is the measurable ROI and over what time horizon?"
- "What is the all-in cost, including implementation and training?"
- "What happens to our costs if usage grows 3x?"
- "What is the downside risk if this does not deliver the projected value?"

**Says yes when**: Clear ROI model with conservative and optimistic cases, flat or predictable pricing, defined success metrics.
**Says no when**: ROI is vague ("saves time"), pricing scales unpredictably with usage, no benchmark data.

**Empathy map prompts**:
- Think: [What financial models do they run before approving a purchase?]
- Feel: [What pressure do they feel from the board or CEO?]
- Say: [What questions do they ask in a budget review?]
- Do: [What approvals or processes do they require before signing?]

---

## Persona 4: The Competitor Analyst

**Short label**: `Competitor Analyst`
**Role**: Product strategist or PM at a rival company, monitoring the market for gaps and response opportunities.

**Primary concerns**:
- How quickly can this be replicated?
- What is the moat — why can't we copy this in 90 days?
- Which customer segments does this threaten first?
- What counter-move would neutralize this?

**Perspective** (generates adversarial ideas and challenges):
- "This is table stakes. Our roadmap already includes this."
- "Their implementation has this specific weakness we can exploit."
- "If they ship this, we respond by accelerating [alternative approach]."
- "Their first-mover advantage disappears as soon as [condition]."

**Says yes when** (evaluating our features): Feature has a defensible moat — network effects, deep integration, proprietary data, or switching costs.
**Says no when**: Feature is easily replicable with no lock-in, relies only on price competition.

**Empathy map prompts**:
- Think: [What competitive gaps does this feature close or open?]
- Feel: [Threat level — concerned, dismissive, or intrigued?]
- Say: [What do they tell their PM team after seeing this feature?]
- Do: [What do they add to their own roadmap in response?]

---

## Persona 5: The Support Team Lead

**Short label**: `Support Lead`
**Role**: Head of customer support or customer success, responsible for ticket volume, response time, and team capacity.

**Primary concerns**:
- Which edge cases generate support tickets?
- Are error messages actionable — can a user self-serve, or do they always call?
- How does this affect the support team's documentation and training burden?
- What is the complexity cost when something goes wrong at 2am?

**Signature objections**:
- "This will generate a flood of 'how do I...' tickets because the flow is not obvious."
- "The error messages do not tell users what to do next."
- "We do not have documentation or training for this feature yet."
- "What is the escalation path when this fails for an enterprise customer?"

**Says yes when**: Clear error messages with recovery steps, comprehensive help docs, low support ticket prediction, clear escalation path.
**Says no when**: Silent failures, obscure error codes, no in-product guidance.

**Empathy map prompts**:
- Think: [What ticket volume does this feature generate in the first 30 days?]
- Feel: [Dread or relief when a new feature ships?]
- Say: [What do they tell the product team during sprint review?]
- Do: [What do they prepare before a feature launches?]

---

## Persona 6: The Power User / Domain Expert

**Short label**: `Power User`
**Role**: Advanced user who uses the product daily and has deep domain expertise. Typical profile: a paralegal using an e-signature platform, a DevOps engineer using a deployment tool, a financial analyst using a data product.

**Primary concerns**:
- Does this feature match real domain workflows, or is it a simplified proxy?
- Are there edge cases that matter in their domain that the feature ignores?
- Does the feature slow down expert users who have efficient existing workflows?
- Can this be customized or extended to fit their specific context?

**Signature objections**:
- "This flow works for simple cases, but breaks for [domain-specific scenario]."
- "I do this 50 times a day — adding one extra click costs me an hour a week."
- "The feature does not understand [domain terminology] — it uses the wrong mental model."
- "Where is the API / bulk operation / keyboard shortcut for this?"

**Says yes when**: Feature respects existing workflows, supports bulk operations, is configurable, handles domain-specific edge cases.
**Says no when**: Feature is designed for lowest-common-denominator use, adds friction to expert workflows, lacks power-user controls.

**Empathy map prompts**:
- Think: [What inefficiency in their current workflow does this fix — or create?]
- Feel: [Pride in expertise, frustration when tools underestimate their sophistication?]
- Say: [What do they post in the community forum after trying the feature?]
- Do: [What workarounds do they build when the feature is "good enough but not right"?]

---

## Persona 7: The Regulator / Compliance Officer

**Short label**: `Regulator`
**Role**: Internal legal counsel, compliance officer, or external regulator evaluating whether the feature meets legal and regulatory requirements. May be from finance, healthcare, government, or a regulated industry.

**Primary concerns**:
- Which regulations apply, and does this feature create new compliance obligations?
- What is the audit trail — who did what, when, and can it be proven in court?
- How is consent obtained, documented, and revocable?
- What happens to data when the relationship ends (retention, deletion, portability)?

**Signature objections**:
- "Under [specific regulation], this constitutes [obligation]. How is that handled?"
- "The audit log does not meet evidentiary standards for [jurisdiction]."
- "Consent is obtained once at signup — that is insufficient for [data processing activity]."
- "There is no documented data retention policy for this feature's output."

**Says yes when**: Clear compliance documentation, complete audit trail, explicit consent mechanisms, data retention controls, jurisdiction-specific configurations.
**Says no when**: Ambiguous data ownership, no audit trail, all-or-nothing consent, no data deletion mechanism.

**Empathy map prompts**:
- Think: [Which specific regulation clause does this feature activate?]
- Feel: [Personal liability risk — are they exposed if this feature creates a violation?]
- Say: [What do they write in the legal review memo?]
- Do: [What conditions do they attach before approving the feature for launch?]
