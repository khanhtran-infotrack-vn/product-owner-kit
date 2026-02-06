# How to Use Skills Directly

## Overview

Skills provide domain knowledge (frameworks, templates, best practices) that you reference directly in your prompts. This gives you more control than invoking agents for every task.

**Key principle**: You tell Claude which skill to use and how to apply it, rather than delegating to an agent that decides for you.

---

## When to Use Skills vs Agents

### Use Agents (2 available)
- **@product-knowledge**: Search documentation and answer questions with citations
- **@feature-brainstormer**: Facilitate creative brainstorming with optional story generation

### Use Skills Directly (8 available)
- **Creating artifacts**: Use skills to apply frameworks and templates
- **Specific knowledge**: Reference particular methods or best practices
- **Full control**: You decide exactly what to apply and how

---

## Skill Reference Guide

### 1. agile-product-owner

**What it provides**:
- INVEST principles (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- User story templates and formats
- Story point estimation guidance (Fibonacci scale)
- Definition of Done standards
- Acceptance criteria patterns

**When to use**:
- Creating user stories
- Estimating work
- Defining acceptance criteria
- Applying agile best practices

**Example usage**:

```
I need to create user stories for the mobile signature feature.

Use the agile-product-owner skill to:
1. Apply INVEST principles to ensure quality stories
2. Use standard user story format: "As a [persona], I want [goal], so that [benefit]"
3. Define clear acceptance criteria using Given/When/Then format
4. Estimate story points using Fibonacci scale (1, 2, 3, 5, 8, 13)

Feature context:
- Users need to sign documents on mobile devices
- Support iOS and Android
- Must work offline
- Sync signatures when online

Create stories in: backlog/mobile-signature/
```

**Output**: User stories following INVEST principles with estimates

---

### 2. analytics-insights

**What it provides**:
- Product metrics frameworks:
  - HEART (Happiness, Engagement, Adoption, Retention, Task Success)
  - AARRR (Acquisition, Activation, Retention, Revenue, Referral)
  - North Star Metric identification
- Feature adoption analysis methods
- A/B testing guidance and statistical significance
- Data interpretation patterns
- Metric selection for different product stages

**When to use**:
- Analyzing product metrics
- Measuring feature success
- Recommending experiments
- Interpreting user behavior data

**Example usage**:

```
Analyze the product metrics from metrics/q1-2025.json

Use the analytics-insights skill to:
1. Apply the HEART framework to categorize metrics
2. Calculate feature adoption rate for mobile signature feature
3. Identify trends (growth, decline, plateaus)
4. Compare against industry benchmarks
5. Recommend A/B tests for improvement

Focus areas:
- Mobile engagement metrics
- Signature completion rates
- User retention after first signature

Output analysis to: reports/q1-2025-analysis.md
```

**Output**: Structured metrics analysis with insights and recommendations

---

### 3. backlog-manager

**What it provides**:
- Backlog organization patterns (by theme, epic, sprint)
- Epic breakdown techniques (vertical slicing)
- Story templates (references/story-templates.md)
- Example epic decomposition (references/epic-breakdown-example.md)
- Story refinement checklists
- Dependency mapping

**When to use**:
- Creating user stories
- Breaking down epics into stories
- Organizing backlog by themes
- Refining existing stories

**Example usage**:

```
Create user stories for AI-powered document preparation based on:
- brainstorm/ai-mobile-document-prep/SUMMARY.md (top 3 ideas)

Use the backlog-manager skill to:
1. Reference story templates from backlog-manager/references/story-templates.md
2. Apply vertical slicing to break down features into deliverable stories
3. Use epic breakdown patterns from references/epic-breakdown-example.md
4. Apply INVEST principles from agile-product-owner skill

For each story include:
- User story format (As a... I want... So that...)
- Acceptance criteria (Given/When/Then)
- Story points (Fibonacci scale)
- Dependencies on other stories or systems
- Technical notes

Top 3 features to convert:
1. Computer Vision Field Detection (High impact, 8 points feasibility)
2. Confidence Scores + Visual Indicators (High impact, 9 points feasibility)
3. Document Understanding + Contact Intelligence (Medium impact, 6 points feasibility)

Create stories in: backlog/ai-mobile-prep/
```

**Output**: Well-structured user stories with acceptance criteria and estimates

---

### 4. documentation-specialist

**What it provides**:
- Documentation standards and structure
- Product Requirements Document (PRD) templates
- Architecture Decision Records (ADR) format
- Release notes and changelog patterns
- API documentation guidelines (REST, GraphQL)
- User guide structures
- Documentation maintenance workflows

**When to use**:
- Writing product documentation
- Creating PRDs or technical specs
- Documenting architectural decisions
- Writing release notes

**Example usage**:

```
Create a Product Requirements Document (PRD) for the mobile signature feature.

Use the documentation-specialist skill to:
1. Apply PRD template structure
2. Include all required sections:
   - Executive Summary
   - Problem Statement
   - Goals and Success Metrics
   - User Stories and Requirements
   - Technical Considerations
   - Dependencies and Risks
   - Timeline and Milestones
3. Follow documentation standards for clarity and completeness
4. Use visual aids (diagrams, mockups) where appropriate

Create in: docs/prds/mobile-signature.md

Feature context:
- Mobile users need native signature capability
- iOS and Android platforms
- Offline-first with sync
- Compliance: eIDAS, ESIGN Act
- Timeline: 3 sprints
```

**Output**: Complete PRD following template structure

---

### 5. esign-domain-expert

**What it provides**:
- eIDAS 2.0 (EU) and ESIGN Act (US) compliance knowledge
- Signature types and when to use each:
  - SES (Simple Electronic Signature)
  - AES (Advanced Electronic Signature)
  - QES (Qualified Electronic Signature)
- Audit trail requirements for compliance
- Identity verification standards (KYC)
- Electronic signature workflows and UX patterns
- Compliance reference: references/compliance-requirements.md

**When to use**:
- Designing eSignature features
- Ensuring compliance with regulations
- Defining audit trail requirements
- Implementing identity verification

**Example usage**:

```
Design the audit trail system for our signature workflow to ensure compliance.

Use the esign-domain-expert skill to:
1. Reference compliance requirements from esign-domain-expert/references/compliance-requirements.md
2. Apply eIDAS 2.0 standards (EU jurisdiction)
3. Apply ESIGN Act requirements (US jurisdiction)
4. Define required audit trail fields for each signature type (SES, AES, QES)
5. Ensure proper identity verification (KYC) steps
6. Include tamper-evident mechanisms

Signature types to support:
- SES: Simple Electronic Signature (basic use cases)
- AES: Advanced Electronic Signature (business documents)
- QES: Qualified Electronic Signature (high-value contracts)

Jurisdictions: EU (eIDAS) and US (ESIGN Act)

Output design to: docs/architecture/audit-trail-design.md
```

**Output**: Compliant audit trail specification

---

### 6. prioritization-engine

**What it provides**:
- RICE framework (Reach × Impact × Confidence / Effort)
- MoSCoW method (Must have, Should have, Could have, Won't have)
- WSJF (Weighted Shortest Job First) for SAFe
- Value vs Effort 2×2 matrices
- Cost of Delay calculations
- Dependency-aware prioritization
- Reference: Framework details (references/frameworks.md)

**When to use**:
- Prioritizing features in backlog
- Deciding what to build next
- Ranking competing priorities
- Resource allocation decisions

**Example usage**:

```
Prioritize the user stories in backlog/ai-mobile-prep/

Use the prioritization-engine skill to:
1. Apply the RICE framework (Reach × Impact × Confidence / Effort)
2. Reference framework details from prioritization-engine/references/frameworks.md
3. Score each feature on:
   - Reach: How many users will this impact? (1-10 scale)
   - Impact: How much will it improve their experience? (0.25=minimal, 0.5=low, 1=medium, 2=high, 3=massive)
   - Confidence: How confident are we in our estimates? (percentage)
   - Effort: How many person-months will it take? (0.5-10+ scale)
4. Calculate RICE score = (Reach × Impact × Confidence) / Effort
5. Rank features by RICE score (highest to lowest)
6. Provide rationale for each score

Features to prioritize:
1. Computer Vision Field Detection (US-001)
2. Confidence Scores + Visual Indicators (US-002)
3. Document Understanding + Contact Intelligence (US-003)

Context:
- 50,000 active mobile users
- Q2 goal: Increase mobile document completion rate by 30%
- Available capacity: 2 ML engineers, 3 mobile engineers
- 2-week sprints

Output ranking to: backlog/ai-mobile-prep/PRIORITY_RANKING.md
```

**Output**: Ranked feature list with RICE scores and rationale

---

### 7. requirements-analyst

**What it provides**:
- Requirements quality framework (clear, complete, consistent, testable)
- Functional vs non-functional requirements distinction
- Gap analysis methodology
- Acceptance criteria patterns (Given/When/Then, checklist format)
- Requirements traceability
- Reference: Quality checklist (references/quality-checklist.md)

**When to use**:
- Analyzing stakeholder requirements
- Identifying gaps and ambiguities
- Structuring requirements
- Validating requirement quality

**Example usage**:

```
Analyze the requirements from stakeholder_feedback/mobile-signature-requests.md

Use the requirements-analyst skill to:
1. Extract functional requirements (what the system must do)
2. Extract non-functional requirements (performance, security, usability)
3. Apply quality checklist from requirements-analyst/references/quality-checklist.md
4. Identify gaps, ambiguities, and inconsistencies
5. Structure requirements by category:
   - Core functionality
   - User experience
   - Security and compliance
   - Performance
   - Integration
6. Define clear acceptance criteria for each requirement

Quality checks:
- Are requirements clear and unambiguous?
- Are they testable?
- Are they complete (no missing information)?
- Are they consistent (no contradictions)?

Output structured requirements to: requirements/mobile-signature/
Create files:
- functional-requirements.md
- non-functional-requirements.md
- gaps-analysis.md
```

**Output**: Structured, high-quality requirements documents with gap analysis

---

### 8. sprint-planner

**What it provides**:
- Sprint planning methodology (Scrum framework)
- Team capacity calculation formulas
- Sprint goal definition patterns
- Velocity tracking and forecasting
- Dependency identification
- Sprint anti-patterns to avoid
- Story selection criteria

**When to use**:
- Planning sprint content
- Calculating team capacity
- Selecting stories from backlog
- Defining sprint goals

**Example usage**:

```
Plan Sprint 12 using the sprint-planner skill.

Team composition and capacity:
- 2 ML engineers × 80 hours/sprint = 160 hours
- 3 mobile engineers × 80 hours/sprint = 240 hours
- Total: 400 hours
- Overhead (meetings, support, etc.): 20%
- Effective capacity: 320 hours

Historical velocity: 30 story points per sprint

Use sprint-planner skill to:
1. Calculate effective capacity accounting for overhead
2. Select stories from backlog/ai-mobile-prep/ that fit capacity
3. Identify dependencies between selected stories
4. Ensure story mix (features + bugs + tech debt)
5. Define clear sprint goal (one sentence)
6. Validate against velocity (don't overcommit)
7. Check for sprint anti-patterns (too many stories, unclear goal, missing skills)

Sprint goal: Deliver Computer Vision Field Detection MVP (US-001)

Available stories (ranked by priority):
1. US-001: Computer Vision Field Detection (8 points, ML focus)
2. US-002: Confidence Scores UI (5 points, mobile focus)
3. US-003: Document Understanding (13 points, ML focus)
4. BUG-045: Signature rendering issue (2 points)
5. TECH-012: API performance optimization (3 points)

Create sprint plan in: sprints/sprint-12/sprint-plan.md
```

**Output**: Complete sprint plan with selected stories, capacity analysis, and sprint goal

---

### 9. stakeholder-communicator

**What it provides**:
- Communication templates by audience:
  - Executive updates (C-level)
  - Engineering updates (technical teams)
  - Sales enablement (customer-facing teams)
  - Customer announcements (end users)
- Release announcement patterns
- Sprint review presentation structure
- Stakeholder alignment frameworks
- Message framing techniques (SCQA, BLUF)

**When to use**:
- Creating executive updates
- Writing release announcements
- Preparing sprint review presentations
- Communicating with stakeholders

**Example usage**:

```
Create an executive update for Q1 2025 progress.

Use the stakeholder-communicator skill to:
1. Apply executive update template (concise, business-focused)
2. Use BLUF format (Bottom Line Up Front)
3. Focus on business outcomes, not technical details
4. Include:
   - Executive Summary (2-3 sentences)
   - Key Achievements (3-5 bullets with metrics)
   - Metrics Dashboard (visual representation)
   - Strategic Impact (alignment with company goals)
   - Next Steps (Q2 priorities)
   - Asks (what you need from leadership)
5. Keep to 1 page maximum

Audience: C-level executives (CEO, CTO, CPO)

Content to summarize:
- Sprints 9-12 completed (Jan-Mar 2025)
- AI features launched (Computer Vision Field Detection)
- Mobile adoption increased 40% (target was 30%)
- Customer feedback score: 4.6/5.0 (up from 4.2)
- 3 major enterprise deals closed using new AI features

Strategic context:
- Company goal: Become market leader in AI-powered document workflows
- Q2 focus: Expand AI capabilities to document understanding

Output to: communications/executive-updates/q1-2025.md
```

**Output**: Executive-friendly update with business focus and clear asks

---

## Combining Multiple Skills

Often you'll want to combine multiple skills in a single workflow:

### Example: Requirements → Stories → Prioritization → Sprint

```
Step 1: Analyze Requirements
Analyze stakeholder_feedback/enterprise-customer-requests.md

Use requirements-analyst skill to:
- Extract functional and non-functional requirements
- Apply quality checklist from references/
- Identify gaps and ambiguities
- Output to: requirements/enterprise-features/

Step 2: Create User Stories
Use backlog-manager skill to create stories from requirements/enterprise-features/

- Reference story templates from references/story-templates.md
- Apply INVEST principles (use agile-product-owner skill)
- Create in: backlog/enterprise-features/

Step 3: Prioritize Stories
Use prioritization-engine skill with RICE framework:
- Score Reach, Impact, Confidence, Effort
- Reference frameworks from references/frameworks.md
- Rank stories by RICE score
- Output ranking to: backlog/enterprise-features/PRIORITY_RANKING.md

Step 4: Plan Sprint
Use sprint-planner skill to plan Sprint 13:
- Team: 8 engineers, 320 hours effective capacity
- Velocity: 35 points
- Select top-ranked stories that fit capacity
- Define sprint goal
- Create: sprints/sprint-13/sprint-plan.md
```

---

## Common Patterns

### Pattern 1: Brainstorm → Stories → Plan

```
# Use agent for creative work
@feature-brainstormer - Brainstorm improvements to mobile onboarding flow

# Use skill for structured artifact creation
Create user stories from brainstorm/mobile-onboarding/SUMMARY.md

Use backlog-manager skill with story templates from references/

# Use skill for planning
Plan Sprint 14 with these stories using sprint-planner skill
Team capacity: 320 hours, Velocity: 30 points
```

---

### Pattern 2: Question → Research → Document

```
# Use agent for information retrieval
@product-knowledge - What are our current compliance requirements for eSignature features?

# Use skill for domain expertise
Design audit trail using esign-domain-expert skill
Reference: compliance-requirements.md

# Use skill for documentation
Document design using documentation-specialist skill
Create ADR (Architecture Decision Record) in: docs/adrs/adr-012-audit-trail.md
```

---

### Pattern 3: Analyze → Prioritize → Communicate

```
# Use skill for analysis
Analyze Q1 metrics from metrics/q1-2025.json

Use analytics-insights skill with HEART framework

# Use skill for prioritization
Prioritize Q2 feature ideas based on Q1 insights

Use prioritization-engine skill with RICE framework

# Use skill for communication
Create executive update summarizing Q1 results and Q2 priorities

Use stakeholder-communicator skill
Audience: C-level executives
Format: 1-page BLUF format
```

---

## Best Practices

### 1. Be Specific About Which Skill to Use

**Bad**:
```
Create user stories for the mobile feature
```

**Good**:
```
Create user stories for the mobile signature feature.

Use the backlog-manager skill to:
- Reference story templates from references/story-templates.md
- Apply INVEST principles
- Create in backlog/mobile-signature/
```

---

### 2. Reference Skill Resources

**Bad**:
```
Prioritize the backlog
```

**Good**:
```
Prioritize backlog/ai-mobile-prep/ using the prioritization-engine skill.

Apply RICE framework (reference: prioritization-engine/references/frameworks.md)
Score each feature for Reach, Impact, Confidence, Effort
```

---

### 3. Specify Output Location

**Bad**:
```
Analyze the requirements
```

**Good**:
```
Analyze requirements from stakeholder_feedback/enterprise-requests.md

Use requirements-analyst skill
Output to:
- requirements/enterprise-features/functional-requirements.md
- requirements/enterprise-features/non-functional-requirements.md
- requirements/enterprise-features/gaps-analysis.md
```

---

### 4. Provide Context

**Bad**:
```
Plan the next sprint
```

**Good**:
```
Plan Sprint 12 using sprint-planner skill

Context:
- Team: 5 engineers (2 ML, 3 mobile)
- Capacity: 320 hours effective
- Velocity: 30 points
- Sprint goal: Deliver Computer Vision Field Detection MVP
- Available stories: backlog/ai-mobile-prep/
```

---

### 5. Combine Skills When Needed

**Bad**:
```
Create stories and prioritize them
```

**Good**:
```
Step 1: Create stories using backlog-manager skill
- Reference templates from references/story-templates.md
- Apply INVEST principles from agile-product-owner skill
- Create in backlog/feature-x/

Step 2: Prioritize using prioritization-engine skill
- Apply RICE framework
- Score stories
- Output ranking to backlog/feature-x/PRIORITY_RANKING.md
```

---

## Troubleshooting

### "I don't know which skill to use"

**Solution**: Match your task to skill purpose:
- Creating artifacts (stories, docs, plans) → Use specific skill
- Answering questions from docs → Use @product-knowledge agent
- Creative ideation → Use @feature-brainstormer agent

### "The output doesn't match my needs"

**Solution**: Be more specific in your prompt:
- Specify which templates or frameworks to use
- Reference specific files within skill's references/
- Provide examples of desired output format
- Give context about your team, product, or constraints

### "I want to combine multiple skills"

**Solution**: Use multi-step prompts:
```
Step 1: Use [skill-1] to [task-1]
Step 2: Use [skill-2] to [task-2] based on output from Step 1
Step 3: Use [skill-3] to [task-3] combining results
```

---

## Viewing Skill Content

### List All Skills

```bash
ls -la ~/.claude/skills/
```

### View Skill Main Content

```bash
cat ~/.claude/skills/backlog-manager/SKILL.md
```

### View Skill References

```bash
ls ~/.claude/skills/backlog-manager/references/
cat ~/.claude/skills/backlog-manager/references/story-templates.md
cat ~/.claude/skills/backlog-manager/references/epic-breakdown-example.md
```

### Skills with Reference Files

- **backlog-manager**: 2 reference files (story-templates.md, epic-breakdown-example.md)
- **esign-domain-expert**: 1 reference file (compliance-requirements.md)
- **prioritization-engine**: 1 reference file (frameworks.md)
- **requirements-analyst**: 1 reference file (quality-checklist.md)

---

## Summary

### Use Agents (2) For:
- **@product-knowledge**: Searching docs and answering questions
- **@feature-brainstormer**: Creative brainstorming with optional story generation

### Use Skills (8) For:
- **agile-product-owner**: User story creation and estimation
- **analytics-insights**: Metrics analysis and experiments
- **backlog-manager**: Story creation and backlog organization
- **documentation-specialist**: Writing docs, PRDs, ADRs
- **esign-domain-expert**: eSignature compliance and design
- **prioritization-engine**: Feature ranking with frameworks
- **requirements-analyst**: Requirements extraction and analysis
- **sprint-planner**: Sprint planning and capacity calculation
- **stakeholder-communicator**: Updates and announcements

### Key Benefits:
- **Control**: You decide which knowledge to apply
- **Clarity**: Direct access to frameworks and templates
- **Efficiency**: No agent overhead for simple tasks
- **Flexibility**: Combine skills in custom workflows

---

## Additional Resources

- `/claude/agents/README.md` - Agent system overview
- `/docs/workflows/` - Detailed workflow guides
- `~/.claude/skills/` - Installed skills with reference materials
- `/docs/MIGRATION_GUIDE.md` - Migrating from old agent system
