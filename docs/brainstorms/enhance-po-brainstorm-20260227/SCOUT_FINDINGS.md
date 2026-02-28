# Scout Findings: PO-Brainstorm & Feature-Brainstormer Analysis
**Date**: 2026-02-27
**Scope**: Complete inventory of po-brainstorm skill, feature-brainstormer agent, related references, and brainstorming ecosystem
**Status**: Complete

---

## Executive Summary

The ProductOwnerOrchestration codebase has a **mature, well-structured brainstorming system** with:
- 1 skill (po-brainstorm) serving as the entry point
- 1 agent (feature-brainstormer) handling the core brainstorming workflow
- 3 reference files providing frameworks and templates
- 1 meta-workflow agent (po-workflow-assistant) for strategic planning
- 1 architecture document explaining recent enhancements

**Current State**: The system is feature-complete with comprehensive Challenge & Critique phases, sub-agent support, writing review integration, and optional user story creation. **No critical gaps were found.**

**Enhancement Opportunities**: Areas for potential improvement include expanded analytics integration, stakeholder workflow templates, and session memory persistence.

---

## Part 1: Core Implementations

### 1.1 PO-Brainstorm Skill
**File**: `.claude/skills/po-brainstorm/SKILL.md` (102 lines)

**Purpose**: Entry point skill that routes brainstorming requests to the feature-brainstormer agent.

**Key Features**:
- **Mode Detection**: Parses mode flags (`--quick`, `--challenge`, `--idea`) from arguments
- **Pre-Discovery**: Asks ONE AT A TIME for missing context:
  - Target persona
  - Scope constraints
  - Session goal
- **Sub-Agent Delegation**: Uses Task() to invoke feature-brainstormer with full context
- **Review Gate**: Reads brainstorm output and surfaces follow-up questions to user
- **Next-Step Options**: Presents three paths:
  - `/po-brainstorm [topic] --challenge` (re-challenge)
  - `/po-research [topic]` (external research)
  - Done (no further action)

**Modes Supported**:
1. **Default (full)**: All phases (context → ideation → clustering → evaluation → challenge → documentation)
2. **--quick**: Skip clustering + challenge (ideation → evaluation → documentation)
3. **--challenge**: Challenge-only mode on existing ideas
4. **--idea**: Ideation + clustering only (skip challenge & evaluation)

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Clear mode detection logic
- Proper handling of missing context
- Correct sub-agent invocation pattern
- Accounts for sub-agent limitations (no AskUserQuestion)
- Proper review gate before surfacing to user

---

### 1.2 Feature-Brainstormer Agent
**File**: `.claude/agents/feature-brainstormer.md` (596 lines)

**Purpose**: Facilitates structured brainstorming sessions for new features and improvements.

**Auto-Trigger Keywords**:
- "brainstorm", "ideate", "generate ideas", "innovative features"
- "explore improvements", "challenge ideas", "stress-test", "critique"

**Core Workflow** (8 steps):
1. **Context Gathering**: Read product_documents/, search existing brainstorms
2. **Facilitated Ideation**: SCAMPER + "How Might We" + anti-bias domain rotation
3. **Idea Clustering**: Group into 4-8 themes, select top 5-7 for evaluation
4. **Evaluation**: Score User Value / Business Impact / Technical Feasibility (1-5)
5. **Challenge & Critique**: 6 sub-phases (pre-mortem, assumption stress-test, devil's advocate, constraint inversion, anti-bias, clustering stress-test)
6. **Ranking Reconciliation**: Revise rankings after challenge
7. **Documentation**: Write SUMMARY.md + IDEAS.md + optional user-stories/
8. **Optional User Stories**: Create draft INVEST-compliant stories with estimates

**Critical Constraints** (enforced):
- Do NOT call AskUserQuestion in sub-agent mode
- Never write outside brainstorm/ directory
- Facilitate, don't decide

**Sub-Agent Mode Handling**:
- Detects from prompt: "You are running as a sub-agent"
- Converts all probing questions to written output under `## FOLLOW-UP QUESTIONS FOR USER`
- Proceeds autonomously without blocking
- Creates draft user stories by default (not optional in sub-agent mode)

**Challenge & Critique Phase Details**:

| Sub-Phase | Purpose | Depth Scaling |
|-----------|---------|---------------|
| **4a: Pre-Mortem** | Identify failure scenarios | < 5 ideas: light (2 scenarios), 5-10: standard (3-5), 10+: full (5+) |
| **4b: Assumption Stress-Test** | Validate hidden assumptions | Lists every assumption, checks evidence, blast radius analysis |
| **4c: Devil's Advocate** | Find concrete objections | 3 specific failure reasons per idea, user objections, weakest link |
| **4d: Constraint Inversion** | Test against changing conditions | Budget 10x/1/10th, timeline changes, competitive response |
| **4e: Anti-Bias Domain Rotation** | Examine missed lenses | Regulatory, Accessibility, i18n, Support, Security/Privacy |
| **4f: Clustering Stress-Test** | Identify clustering bias | Over-represented clusters, blind spots, cross-cluster synergies |

**Writing Review Integration** (Step 7.5):
- Mandatory prose check before saving
- Checks: active voice, omit needless words, no AI puffery, concrete language
- Applied to: problem statements, rationale, recommendations, next steps
- Skipped: tables, code blocks, structured lists

**User Story Creation** (Step 8, optional in interactive, default in sub-agent):
- Applies INVEST principles from agile-product-owner skill
- Maps feasibility scores to story points:
  - Feasibility 5 → 1-2 pts
  - Feasibility 4 → 3-5 pts
  - Feasibility 3 → 5-8 pts
  - Feasibility 2 → 8-13 pts
  - Feasibility 1 → 13+ pts (recommend split)
- Creates: `user-stories/US-001-[name].md`, `US-002-...`, `README.md`
- Clearly marked as drafts pending team review

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Comprehensive facilitator stance with clear guidelines
- Well-structured workflow with mode support
- Robust Challenge phase with 6 sub-phases
- Sub-agent mode handled correctly
- Writing review integrated
- User story creation well-specified
- Extensive probing question bank
- Clear output format expectations

---

## Part 2: Reference Files & Supporting Materials

### 2.1 Challenge Techniques Reference
**File**: `.claude/agents/references/challenge-techniques.md` (170 lines)

**Purpose**: Expanded templates and question banks for Challenge & Critique phase.

**Content Structure**:
1. **Pre-Mortem Templates** (4 categories)
   - Market Failure scenarios
   - Technical Failure scenarios
   - Business Failure scenarios
   - Competitive Failure scenarios

2. **Devil's Advocate Question Bank** (5 categories, 20+ questions)
   - Value Challenges (5 questions)
   - Assumption Challenges (3 questions)
   - Market & Competitive Challenges (3 questions)
   - Execution Challenges (3 questions)
   - Strategic Challenges (2 questions)

3. **Persona Challenge Profiles** (5 personas)
   - Skeptical Enterprise Buyer
   - Overwhelmed New User
   - Cost-Conscious CFO
   - Competitor Analyst
   - Support Team Lead

4. **Constraint Inversion Scenarios**
   - Budget variations (10x, 1/10th, zero cost)
   - Timeline variations (half, double, tomorrow)
   - Team variations (solo, outsourced, 2x team)
   - Market variations (monopoly, crowded, new market)

5. **Advanced Elicitation Methods**
   - Red Team vs Blue Team
   - Shark Tank Pitch format
   - Thesis Defense format

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Comprehensive question banks (organized by category)
- Practical templates with examples
- Persona profiles are specific and realistic
- Constraint scenarios well-structured
- Advanced elicitation methods add depth

---

### 2.2 Brainstorm Templates Reference
**File**: `.claude/agents/references/brainstorm-templates.md` (250 lines)

**Purpose**: Output templates for SUMMARY.md, IDEAS.md, user stories, and README files.

**Templates Included**:

1. **SUMMARY.md Template**
   - Sections: Problem Statement, Ideas Generated, Comparative Analysis, Idea Clusters, Challenge & Critique Findings, Recommended Approach, Next Steps, Questions to Resolve, Parking Lot
   - Pre-filled tables for evaluation scores and cluster analysis

2. **IDEAS.md Template**
   - All ideas as generated (unfiltered)
   - Grouped by domain rotation cluster
   - Lists domains used

3. **User Story Template (US-XXX.md)**
   - Story ID, Epic, Priority, Status, Date
   - User Story (As a... I want... So that...)
   - Business Context
   - Acceptance Criteria (Given/When/Then format)
   - Estimated Effort (story points + time)
   - Dependencies / Risks
   - Notes with source and draft status

4. **User Stories README Template**
   - Story summary table
   - Total story points
   - Next steps (review, requirements, backlog)
   - Warning about preliminary estimates

5. **Story Point Estimation Reference**
   - Mapping table: Points → Complexity → Timeline → Feasibility

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Complete templates with all required sections
- Clear formatting examples
- Estimation guidance well-specified
- Draft status clearly communicated

---

### 2.3 Brainstorming Workflow Guide
**File**: `.claude/workflows/brainstorming-workflow.md` (491 lines)

**Purpose**: Complete step-by-step guide for using the brainstorming system.

**Content Structure**:
1. **When to Use** (good use cases, not suitable for)
2. **Prerequisites** (required product documents context)
3. **Step-by-Step Workflow**:
   - Step 1: Prepare your context (create product_documents/)
   - Step 2: Invoke the brainstormer agent
   - Step 3: Review brainstorming output
   - Step 4: Validate with stakeholders
   - Step 5: Choose your next path (5 options)
4. **Advanced Tips** (multiple sessions, refine existing ideas, domain experts, iterate based on feedback)
5. **Brainstorming Techniques Explained** (6 techniques: SCAMPER, HMW, Crazy 8s, Analogies, Reverse Thinking, User Mapping)
6. **Common Pitfalls & Solutions** (4 pitfalls with fixes)
7. **Success Metrics** (process, outcome, quality metrics)

**Next Steps Paths Offered**:
- Path A: Technical Validation
- Path B: User Validation
- Path C: Requirements & Backlog
- Path D: Competitive Analysis
- Path E: Risk Assessment

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Comprehensive guide suitable for new users
- Practical examples throughout
- Clear decision points for next steps
- Good coverage of pitfalls and solutions

---

## Part 3: Agent & Workflow Integration

### 3.1 Feature-Brainstormer Agent Update Document
**File**: `/docs/architecture/feature-brainstormer-update.md` (441 lines)

**Purpose**: Documents the Feb 6, 2026 enhancement adding optional user story creation to feature-brainstormer.

**Changes Documented**:
1. Added skills integration (agile-product-owner)
2. Enhanced core responsibilities (added user story creation)
3. Updated workflow pattern (steps 6-8 added)
4. Comprehensive user story creation section
5. Output structure changed from single file to user-stories/ folder
6. Story point estimation guidelines mapped to feasibility scores
7. Example interaction pattern updated

**Benefits Called Out**:
- Faster iteration (saves ~30 min)
- Immediate estimates
- Better context preservation
- Flexibility (user choice)
- Skills integration demo

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Well-structured change documentation
- Before/after comparison clear
- Benefits and integration points explained
- Testing scenarios provided

---

### 3.2 PO-Workflow-Assistant Agent
**File**: `.claude/agents/po-workflow-assistant.md` (166 lines)

**Purpose**: Meta-workflow agent for Product Owner planning rituals and strategic blind spot detection.

**Auto-Trigger Keywords**:
- "start sprint", "quarterly planning", "run workflow check"
- "pre-planning review", "what are my blind spots"
- "find gaps in product strategy", "audit my docs"

**Two-Check System**:
1. **Risk Radar Scan** (po-risk-radar): Scans product directories against 28-domain taxonomy (Tier 1-4)
2. **Writing Quality Spot-Check** (writing-clearly-and-concisely): Reviews 3 recent files for prose issues

**Integration with Brainstorming**:
- Identifies blind spots and suggests `/po-brainstorm [topic]` as remediation
- Can recommend which domains to explore in next brainstorming session

**Current Implementation Quality**: ⭐⭐⭐⭐
- Good strategic oversight mechanism
- Proper integration with po-brainstorm
- Clear output format
- Note: po-risk-radar skill referenced but implementation not in scope of this scout

---

## Part 4: Skills Ecosystem

### Skills Integrated with Brainstorming:

**Primary Skills Used**:

1. **agile-product-owner**: INVEST principles, story templates, estimation
2. **writing-clearly-and-concisely**: Prose quality review before saving docs
3. **po-risk-radar**: Strategic blind spot detection (used by po-workflow-assistant)

**Secondary Skills Available for Follow-Up**:
- analytics-insights: Validate ideas with user data
- requirements-analyst: Create detailed requirements
- backlog-manager: Add stories to official backlog
- documentation-specialist: Create feature spec from brainstorming
- prioritization-engine: Rank ideas against backlog
- esign-domain-expert: Compliance validation (domain-specific)

**Current Implementation Quality**: ⭐⭐⭐⭐⭐
- Skills properly referenced
- Clear handoff points documented
- No circular dependencies

---

## Part 5: Current Capabilities & Strengths

### ✅ What Works Well

**1. Entry Point Flow**
- `po-brainstorm` skill cleanly routes to agent
- Mode detection is robust
- Context gathering is interactive (uses AskUserQuestion before sub-agent invocation)
- Review gate ensures output quality

**2. Brainstorming Facilitation**
- SCAMPER + How Might We + Anti-bias domain rotation (prevents LLM clustering)
- Facilitator stance clear (ask probing questions, don't criticize)
- Sub-agent mode properly detected and handled
- All three modes work (full, quick, idea-only)

**3. Challenge & Critique Phase** (strongest feature)
- 6 comprehensive sub-phases with clear depth scaling
- Pre-Mortem with failure scenarios
- Assumption stress-test with blast radius analysis
- Devil's advocate with persona profiles
- Constraint inversion across budget/timeline/team/market
- Anti-bias domain rotation (regulatory, a11y, i18n, support, security)
- Clustering stress-test (identifies bias in theme selection)

**4. Writing Quality**
- Writing review step (7.5) mandatory before saving
- Checks: active voice, needless words, puffery, vague language
- Clear what to fix

**5. User Story Creation**
- INVEST-aligned format
- Story point estimates mapped from feasibility
- Optional in interactive mode, default in sub-agent
- Marked as drafts pending review

**6. Documentation**
- SUMMARY.md (comprehensive with all challenge findings)
- IDEAS.md (unfiltered raw ideas)
- User-stories/ folder (if created)
- Clear output location (brainstorm/[topic-slug]/)

**7. Sub-Agent Support**
- Accounts for lack of AskUserQuestion
- Writes probing questions in output instead of blocking
- Creates user stories by default
- Proceeds autonomously when user input unavailable

---

## Part 6: Gaps & Enhancement Opportunities

### 🔍 Identified Gaps

**1. Analytics Integration (Low Priority)**
- **Gap**: Challenge phase doesn't mention user behavior validation
- **Current State**: Agent suggests using analytics-insights as a follow-up skill
- **Opportunity**: Could add a "User Data Validation" sub-phase in Challenge that asks: "What user metrics would prove this assumption wrong?"
- **Effort**: Medium (requires analytics-insights skill integration)

**2. Stakeholder Workflow Templates (Low Priority)**
- **Gap**: No templates for stakeholder review sessions
- **Current State**: Workflow guide mentions Step 4 (stakeholder validation) but no template provided
- **Opportunity**: Create `.claude/agents/references/stakeholder-review-template.md` with:
  - Meeting agenda template
  - Feedback capture form
  - Prioritization voting template
- **Effort**: Low (documentation only)

**3. Session Memory & Iteration Tracking (Medium Priority)**
- **Gap**: No built-in way to track brainstorming session history
- **Current State**: Each session creates new brainstorm/[topic]/ folder
- **Opportunity**: Add optional session logging:
  - Track which ideas were generated across multiple sessions on same topic
  - Identify patterns (e.g., "ideas cluster A was present in both sessions")
  - Compare idea evaluations across sessions
- **Effort**: Medium (requires new reference file + agent enhancement)

**4. Competitive Analysis Automation (Low Priority)**
- **Gap**: Devil's advocate phase asks "why hasn't a competitor built this?" but no structured competitor research output
- **Current State**: Brainstorming workflow Step 5d suggests manual competitive analysis
- **Opportunity**: Create optional "Competitive Threat Assessment" section in SUMMARY.md that:
  - Lists competitor alternatives for top 3 ideas
  - Scores each competitor approach
  - Identifies differentiation gaps
- **Effort**: High (requires external research integration)

**5. Risk Quantification (Medium Priority)**
- **Gap**: Challenge phase identifies risks but doesn't quantify them
- **Current State**: Pre-mortem has Likelihood & Impact scoring, but overall risk matrix not presented
- **Opportunity**: Add "Risk Matrix" section to SUMMARY.md challenge findings:
  - Risk | Likelihood (1-5) | Impact (1-5) | Mitigation Strategy
- **Effort**: Low (template enhancement only)

### 🟡 Non-Gaps (Everything Else)

- Mode support (full, quick, challenge-only, idea-only) — ✅ Complete
- Sub-agent mode handling — ✅ Complete
- Writing review — ✅ Complete
- User story creation — ✅ Complete
- Challenge depth scaling — ✅ Complete
- Reference materials — ✅ Comprehensive
- Brainstorming techniques — ✅ 5+ techniques
- Output templates — ✅ All required sections

---

## Part 7: File Inventory

### Core Implementation Files

| File | Purpose | Lines | Status |
|------|---------|-------|--------|
| `.claude/skills/po-brainstorm/SKILL.md` | Entry point skill | 102 | ✅ Complete |
| `.claude/agents/feature-brainstormer.md` | Core brainstorming agent | 596 | ✅ Complete |
| `.claude/agents/po-workflow-assistant.md` | Strategic planning meta-agent | 166 | ✅ Complete |
| `.claude/agents/references/challenge-techniques.md` | Challenge phase templates | 170 | ✅ Complete |
| `.claude/agents/references/brainstorm-templates.md` | Output templates | 250 | ✅ Complete |
| `.claude/workflows/brainstorming-workflow.md` | User guide | 491 | ✅ Complete |
| `/docs/architecture/feature-brainstormer-update.md` | Change documentation | 441 | ✅ Complete |

**Total LOC**: ~2,216 lines of markdown + YAML

---

## Part 8: Recommended Enhancements (Priority Order)

### Priority 1: Risk Quantification (Quick Win)
**File**: `.claude/agents/references/brainstorm-templates.md`
**Change**: Add Risk Matrix template to SUMMARY.md section
**Effort**: 1-2 hours
**Impact**: Helps with risk-driven prioritization
**Example**:
```markdown
## Risk Matrix (After Challenge)

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| Market adoption slower than expected | 3/5 | 4/5 | Run user validation pilot |
```

### Priority 2: Stakeholder Review Templates (Low Effort)
**File**: Create `.claude/agents/references/stakeholder-review-template.md`
**Change**: Add meeting agenda, feedback form, voting template
**Effort**: 2-3 hours
**Impact**: Streamlines Step 4 of brainstorming workflow
**Could include**: Agenda template, feedback capture sheet, prioritization voting template

### Priority 3: Session Iteration Tracking (Medium)
**File**: Create `.claude/agents/references/session-tracking-guide.md` + enhance feature-brainstormer
**Change**: Add optional "Previous Sessions" section to SUMMARY.md that references prior brainstorm output
**Effort**: 4-6 hours
**Impact**: Helps identify convergent ideas and themes across iterations

### Priority 4: Competitive Threat Assessment (Deferred)
**File**: Create `.claude/agents/references/competitive-analysis-template.md`
**Change**: Add optional section to Challenge phase output
**Effort**: 6-8 hours
**Impact**: Strengthens differentiation analysis
**Note**: May require external research integration (scout for existing competitive analysis skills first)

---

## Part 9: How to Use This Scout Report

### For Enhancement Work:
1. Reference Part 6 (Gaps) to understand what could be improved
2. Use Part 8 (Recommended Enhancements) to prioritize next work
3. Refer to Part 7 (File Inventory) to know what to modify

### For Understanding Current State:
1. Start with Executive Summary
2. Read Part 1 (Core Implementations) for deep dive
3. Reference Part 5 (Strengths) to understand capabilities
4. Use Part 4 (Skills Ecosystem) to see integration points

### For Quick Reference:
- Challenge phase details: Part 1.2 (sub-phases 4a-4f)
- Templates available: Part 2.2
- Workflow steps: Part 2.3
- Next steps paths: Part 2.3 (Paths A-E)

---

## Part 10: Summary by Topic

### Brainstorming Modes
- **Full** (default): All 8 steps including Challenge
- **Quick** (--quick): Skip clustering + challenge (6 steps)
- **Idea** (--idea): Stop after clustering (3 steps)
- **Challenge** (--challenge): Re-challenge existing ideas (steps 5-6 only)

### Challenge Sub-Phases (6 total)
1. Pre-Mortem: Failure scenarios
2. Assumption Stress-Test: Validate assumptions
3. Devil's Advocate: Concrete objections
4. Constraint Inversion: Test robustness
5. Anti-Bias Domain Rotation: Missed lenses
6. Clustering Stress-Test: Theme bias

### Output Structure
```
brainstorm/[topic-slug]/
├── SUMMARY.md (comprehensive with challenge findings)
├── IDEAS.md (all raw ideas)
├── user-stories/ (optional)
│   ├── US-001-[name].md
│   ├── US-002-[name].md
│   └── README.md
└── references.md (optional, inspiration sources)
```

### Next Steps After Brainstorming
- Re-challenge: `/po-brainstorm [topic] --challenge`
- Research: `/po-research [topic]`
- Validate: Use analytics-insights or user research
- Requirements: Use requirements-analyst skill
- Backlog: Use backlog-manager skill
- Assess risk: Use po-risk-radar skill

---

## Conclusion

**The brainstorming system is mature, well-documented, and feature-complete.** All critical workflows are in place:
- Entry point routing (po-brainstorm skill)
- Core brainstorming (feature-brainstormer agent)
- Challenge & critique (6 sub-phases)
- Writing review (mandatory)
- User story creation (optional)
- Strategic oversight (po-workflow-assistant)

**Recommended immediate action**: Implement Priority 1 (Risk Quantification) and Priority 2 (Stakeholder Templates) for quick improvements without major refactoring.

**No critical gaps found.** The system can be enhanced incrementally without disrupting existing workflows.

---

**Scout Report Completed**: 2026-02-27
**Total Files Analyzed**: 7 core implementation files + 5 supporting docs
**Recommendations**: 4 enhancement areas identified (Priority 1-4)
