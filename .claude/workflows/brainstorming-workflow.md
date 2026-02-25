# Brainstorming Workflow

## Overview
This workflow shows how to use the **feature-brainstormer agent** to generate, evaluate, and prioritize feature ideas systematically using creative brainstorming techniques.

**Time to Complete**: 1-2 hours  
**Agent**: feature-brainstormer  
**Output**: 15-30 evaluated ideas with implementation roadmap

---

## When to Use This Workflow

### ✅ Good Use Cases
- **New feature exploration**: "What should we build to solve X problem?"
- **Product discovery**: "How might we improve the mobile experience?"
- **Strategic planning**: "What AI capabilities should we add in Q2?"
- **Problem-solving**: "Users complain about Y, what are creative solutions?"
- **Innovation sessions**: "What would differentiate us from competitors?"

### ❌ Not Suitable For
- **Well-defined requirements**: If you already know exactly what to build, skip to requirements-analyst
- **Bug fixes**: For existing functionality issues, use debugging workflows
- **Simple enhancements**: Minor improvements don't need brainstorming

---

## Prerequisites

### Required Context (in `product_documents/`)
1. **Product vision** - What problem does your product solve? Who are your users?
2. **User research** - What pain points, needs, or opportunities exist?
3. **Strategic goals** - What are you trying to achieve this quarter/year?

### Optional Context (helpful but not required)
4. **Competitive landscape** - Who are competitors? What do they offer?
5. **Technical constraints** - Platform limitations, architecture decisions
6. **Business constraints** - Budget, timeline, team capacity

### Example Structure
```
product_documents/
├── product-vision.md           # Required
├── user-research-q1-2025.md    # Required
├── strategic-goals-2025.md     # Required
├── competitive-landscape.md    # Optional
└── technical-constraints.md    # Optional
```

---

## Step-by-Step Workflow

### Step 1: Prepare Your Context (15-30 minutes)

**1.1 Create or Update Product Documents**

If you don't have product documents yet, create these files in `product_documents/`:

**Minimum Viable Context**:
```markdown
# product-vision.md

## What We Do
[2-3 sentences describing your product]

## Target Users
1. [Primary user persona]
2. [Secondary user persona]

## Current Capabilities
- [Key feature 1]
- [Key feature 2]
- [Key feature 3]

## Pain Points (from user research)
1. [Pain point 1 with evidence]
2. [Pain point 2 with evidence]
3. [Pain point 3 with evidence]
```

**Pro Tip**: The more specific your context, the better the brainstorming output. Include:
- User quotes from interviews
- Quantitative data (metrics, survey results)
- Specific examples of user struggles
- Competitor capabilities to differentiate against

---

### Step 2: Invoke the Brainstormer Agent (5 minutes)

**2.1 Craft Your Brainstorming Prompt**

Use this template:
```
@feature-brainstormer - Brainstorm [specific topic/problem]

Context:
- [Key constraint or focus area]
- [Important user insight]
- [Strategic priority]

Generate ideas for: [specific outcome you want]
```

**Examples**:

**Example 1: Problem-Focused**
```
@feature-brainstormer - Brainstorm solutions for mobile document preparation

Context:
- 35% of signatures happen on mobile but users abandon due to friction
- 62% of mobile users switch to desktop for document prep
- Our strategic goal is "Mobile Excellence" for 2025

Generate ideas for: Making mobile document preparation faster and easier than desktop
```

**Example 2: Opportunity-Focused**
```
@feature-brainstormer - Brainstorm AI capabilities for our eSignature platform

Context:
- 89% of users interested in AI features
- Competitors (DocuSign, Adobe) are adding AI, but focused on desktop
- We want to differentiate with mobile-first AI

Generate ideas for: AI features that save time and reduce errors for mobile users
```

**Example 3: Strategic-Focused**
```
@feature-brainstormer - Brainstorm integration and automation features

Context:
- 68% of customers use 3+ connected tools (CRM, HRIS, project management)
- 82% of signature requests are part of larger business processes
- Current integrations are limited to Zapier (not real-time)

Generate ideas for: Deep integrations that embed signing into user workflows
```

**2.2 What Happens Next (Automatic)**

The agent will:
1. ✅ Read product context from `product_documents/`
2. ✅ Apply 6+ creative brainstorming techniques:
   - SCAMPER (Substitute, Combine, Adapt, Modify, Put to other uses, Eliminate, Reverse)
   - "How Might We" questions
   - Crazy 8s (rapid ideation)
   - Analogies (inspiration from other domains)
   - Reverse Thinking (what if we did the opposite?)
   - User Journey Mapping (ideas at each journey stage)
3. ✅ Generate 50-100+ raw ideas
4. ✅ Evaluate top 15-20 ideas across dimensions:
   - **User Value**: How much does this help users?
   - **Business Impact**: Revenue, retention, competitive advantage
   - **Technical Feasibility**: Can we build this?
   - **Effort**: How long will it take?
5. ✅ Create 3-phase implementation roadmap
6. ✅ Suggest next steps and agent collaborations

**Duration**: 30-60 minutes (agent processes in background)

---

### Step 3: Review Brainstorming Output (20-30 minutes)

**3.1 Output Location**
```
brainstorm/[feature-name]/
├── SUMMARY.md           # Top 15 ideas, evaluations, roadmap (read this first!)
├── IDEAS.md             # All 50+ raw ideas organized by technique
└── NEXT_STEPS.md        # Recommendations for moving forward
```

**3.2 What to Look For**

**In SUMMARY.md**:
- ✅ **Top 15 Prioritized Ideas**: Sorted by total score (User Value + Business Impact + Feasibility - Effort)
- ✅ **Evaluation Matrix**: 5-star ratings for each idea across 4 dimensions
- ✅ **Implementation Roadmap**: 3-phase plan (Quick Wins, Core Platform, Advanced Features)
- ✅ **Why It Matters**: Context for each idea (user pain point, competitive gap, strategic alignment)
- ✅ **Dependencies**: What must be built first

**In IDEAS.md**:
- ✅ **Raw Ideas by Technique**: See how different approaches generated different ideas
- ✅ **Wild Card Ideas**: Creative, unconventional ideas for future exploration
- ✅ **Ideas by User Journey Stage**: Pre-send, sending, post-send ideas

**In NEXT_STEPS.md**:
- ✅ **Immediate Actions**: What to do this week (validate, spike, prototype)
- ✅ **Short-Term Actions**: Next 2 weeks
- ✅ **Medium-Term Actions**: Next month
- ✅ **Agent Collaboration Plan**: Which agents to invoke next and how

**3.3 Review Checklist**

Ask yourself:
- [ ] Do the top ideas align with our strategic goals?
- [ ] Are the evaluation scores reasonable? (User Value, Business Impact, Feasibility, Effort)
- [ ] Are there any "obvious" ideas missing?
- [ ] Are there dependencies we haven't considered?
- [ ] Do the timeline estimates feel realistic?
- [ ] Are there quick wins we can ship soon?

---

### Step 4: Validate with Stakeholders (30-60 minutes)

**4.1 Stakeholder Review Session**

**Invite**:
- Product team (PMs, designers)
- Engineering leads (frontend, backend, ML)
- Business stakeholders (sales, marketing, customer success)

**Agenda** (45-60 minutes):
1. **Context recap** (5 min): Problem, user research, strategic goals
2. **Top 10 ideas** (20 min): Walk through SUMMARY.md, discuss evaluations
3. **Feedback capture** (15 min):
   - Which ideas resonate most?
   - Any concerns or blockers?
   - Ideas we should add or remove?
4. **Prioritization** (10 min): Align on top 3-5 ideas to pursue
5. **Next steps** (5 min): Who does what by when

**4.2 Capture Feedback**

Update SUMMARY.md with stakeholder input:
```markdown
## Stakeholder Feedback (Feb 6, 2026)

### Attendees
- Alice (PM), Bob (Eng Lead), Carol (Design), Dave (Sales)

### Key Decisions
- ✅ Prioritize Computer Vision Field Detection (unanimous support)
- ✅ Deprioritize Voice Commands (concerns about accuracy, privacy)
- 🔄 Need technical spike for Offline Mode (unknown complexity)

### Adjusted Priorities
1. Computer Vision Field Detection (was #1, stays #1)
2. Confidence Scores + Visual Indicators (was #2, stays #2)
3. Document Understanding + Contact Intelligence (was #3, stays #3)
4. One-Tap Scan & Prep (was #4, promoted due to marketing interest)
5. AI Pre-Flight Check (was #5, stays #5)

### Action Items
- [ ] Bob: Technical spike for ML model accuracy (2 days)
- [ ] Carol: Design prototype for One-Tap flow (3 days)
- [ ] Dave: Customer validation calls for top 3 features (1 week)
```

---

### Step 5: Next Steps - Choose Your Path

After validating ideas, you have several options:

#### Path A: Technical Validation (for novel/complex ideas)

Work with your engineering team to review `brainstorm/[feature-name]/SUMMARY.md`. Focus on:
- ML infrastructure requirements
- Mobile architecture (on-device vs cloud inference)
- API design
- Data privacy considerations

Output: Technical spike results or architecture document in `docs/technical/[feature-name]/`

#### Path B: User Validation (for customer-facing features)

Conduct user research to validate top concepts from `brainstorm/[feature-name]/SUMMARY.md`:
- Test top 5 concepts with 10 mobile-heavy users
- Use usability testing, prototype walkthroughs, or surveys

Output: Validation report with user feedback and recommendations in `product_documents/user-research-[feature]-validation.md`

#### Path C: Requirements & Backlog (for validated ideas)

```
Use requirements-analyst skill to create detailed requirements for Phase 1 features in
brainstorm/[feature-name]/SUMMARY.md

Then use backlog-manager skill to create INVEST-compliant user stories for Phase 1

Focus on 12-week delivery timeline
```

#### Path D: Competitive Analysis (for differentiation-critical features)

Research competitor AI capabilities manually or with web search. Reference context from `brainstorm/ai-mobile-document-prep/SUMMARY.md`:
- DocuSign, Adobe Sign, PandaDoc, HelloSign AI features
- How are they positioning AI? (marketing, pricing, demos)
- Gaps we can exploit for differentiation

Output: Competitive matrix and positioning recommendations in `product_documents/competitive-[feature-name].md`

#### Path E: Risk Assessment (for high-investment features)

Review risks for Phase 1 features with your team using `brainstorm/[feature-name]/SUMMARY.md`. Focus areas:
- Technical risks (ML accuracy, performance, infrastructure)
- Business risks (adoption, competitive response)
- Compliance risks — use **esign-domain-expert skill** for eSign compliance
- Timeline risks (dependencies, unknowns)

Output: Risk matrix with mitigation strategies in `docs/risks/[feature-name]-risks.md`

---

## Advanced Tips

### Tip 1: Run Multiple Brainstorming Sessions
**When**: Complex problem with multiple angles

**Example**:
```
Session 1: Brainstorm mobile document preparation (user perspective)
Session 2: Brainstorm mobile document preparation (technical architecture)
Session 3: Brainstorm mobile document preparation (business model/pricing)
```

**Why**: Different angles produce different ideas. Synthesize across sessions.

---

### Tip 2: Use Brainstorming to Refine Existing Ideas
**When**: You have a general idea but need to flesh out details

**Example**:
```
@feature-brainstormer - We've decided to build "Computer Vision Field Detection"
Brainstorm implementation approaches and UX variations for this feature

Context: brainstorm/ai-mobile-document-prep/SUMMARY.md (see idea #1)

Focus on:
- Different ML model approaches (on-device vs cloud, accuracy vs speed)
- UX variations (auto-apply vs preview-first, manual override options)
- Fallback strategies (what if detection fails?)
```

---

### Tip 3: Involve Domain Experts in Brainstorming
**When**: Specialized domain knowledge is critical

**Example** (for eSign platform):
```
Use the esign-domain-expert skill to review brainstorming output in
brainstorm/ai-mobile-document-prep/SUMMARY.md

Validate ideas against:
- Legal compliance (eIDAS, ESIGN Act, UETA)
- Industry standards (signature placement conventions)
- Security best practices (document integrity, audit trails)

Flag any compliance risks or missing considerations
```

---

### Tip 4: Iterate Based on User Feedback
**When**: You've shipped v1 and learned what works/doesn't work

**Example**:
```
@feature-brainstormer - Brainstorm improvements for Computer Vision Field Detection

Context:
- We shipped v1 two months ago
- User feedback: 85% accuracy is good but users want manual override
- Analytics: 45% of users edit AI-detected fields before sending
- Support tickets: Users confused when AI misses fields on complex documents

Generate ideas for: Improving v1 based on real user behavior
```

---

## Brainstorming Techniques Explained

The agent uses these techniques automatically, but understanding them helps you evaluate output:

### 1. SCAMPER
- **Substitute**: Replace component with alternative
- **Combine**: Merge features or capabilities
- **Adapt**: Adjust feature for different context
- **Modify**: Change attributes (bigger, smaller, faster)
- **Put to other uses**: Repurpose for new use case
- **Eliminate**: Remove unnecessary elements
- **Reverse**: Flip process or approach

### 2. "How Might We" (HMW)
Reframes problems as opportunities:
- Problem: "Users struggle with field placement"
- HMW: "How might we eliminate the need for field placement?"

### 3. Crazy 8s
Rapid ideation: 8 ideas in 8 minutes (forces quick, divergent thinking)

### 4. Analogies
Inspiration from other domains:
- "What if document preparation was like Instagram filters?" (one-tap, AI-powered)
- "What if signing was like Uber?" (real-time tracking, ETA predictions)

### 5. Reverse Thinking
Flip assumptions:
- Assumption: "Users must place fields"
- Reverse: "What if documents came pre-configured?"

### 6. User Journey Mapping
Ideas at each journey stage:
- Pre-send: Template selection, document upload
- Sending: Field placement, signer assignment, routing
- Post-send: Tracking, reminders, completion

---

## Common Pitfalls & Solutions

### Pitfall 1: Too Many Ideas, Can't Choose
**Problem**: Agent generates 50+ ideas, team overwhelmed

**Solution**:
- Focus on SUMMARY.md (top 15 pre-filtered ideas)
- Use evaluation scores to narrow to top 5
- Run stakeholder review to align on priorities
- Start with Quick Wins (low effort, high value)

### Pitfall 2: Ideas Are Too Generic
**Problem**: Output lacks specificity, could apply to any product

**Solution**:
- Add more specific context to product_documents/
- Include user quotes, metrics, pain points
- Provide competitor examples to differentiate
- Re-run brainstorming with refined prompt

### Pitfall 3: Ideas Are Too Technical/Product-Focused
**Problem**: Ideas focus on "how" instead of user value

**Solution**:
- Refocus on user pain points (not solutions)
- Ask agent to evaluate "User Value" more heavily
- Involve designers in review to focus on UX

### Pitfall 4: No Clear Next Steps
**Problem**: Great ideas but unclear how to move forward

**Solution**:
- Read NEXT_STEPS.md (agent provides recommendations)
- Choose a path: technical validation, user validation, or backlog creation
- Break down Phase 1 into smaller milestones (2-week iterations)

---

## Success Metrics

Track these metrics to measure brainstorming effectiveness:

### Process Metrics
- **Time to generate ideas**: Target < 2 hours (agent work + review)
- **Ideas generated**: Target 50-100 raw ideas, 15-20 evaluated
- **Stakeholder alignment**: Single meeting to prioritize top 5

### Outcome Metrics
- **Ideas shipped**: % of brainstormed ideas that reach production
- **User impact**: NPS, satisfaction scores for shipped features
- **Business impact**: Revenue, retention, engagement metrics

### Quality Metrics
- **Idea novelty**: Are ideas differentiated from competitors?
- **Idea feasibility**: Can we actually build this?
- **Idea desirability**: Do users actually want this?

---

## Related Workflows

- [Feature Development Workflow](./feature-development-workflow.md) - Complete feature delivery process
- [Sprint Planning Workflow](./sprint-planning-workflow.md) - Plan sprints after brainstorming is complete

---

## Questions & Feedback

If you have suggestions for improving this workflow, add them to:
`docs/workflows/workflow-feedback.md`
