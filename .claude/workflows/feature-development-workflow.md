# Feature Development Workflow

## Overview
This workflow demonstrates the complete feature development process using the Product Owner Orchestration System, from initial brainstorming through sprint planning and backlog management.

**Time to Complete**: 2-3 days (including validation and refinement)
**Involved**: 1 agent (@feature-brainstormer) + 4 skills (requirements-analyst, backlog-manager, sprint-planner, documentation-specialist)
**Output Artifacts**: Brainstorming summary, user stories, sprint plan, documentation

---

## Workflow Stages

### Stage 1: Discovery & Brainstorming
**Goal**: Generate and evaluate feature ideas based on user research and product context

**Prerequisites**:
- Product documentation in `product_documents/` folder
- User research or problem statement
- Strategic context (goals, competitors, constraints)

**Steps**:

1. **Prepare Product Context** (Manual)
   ```
   Add to product_documents/:
   - product-vision.md (product overview, target users, goals)
   - user-research-q1-2025.md (research findings, pain points)
   - competitive-landscape.md (optional)
   ```

2. **Invoke Feature Brainstormer Agent**
   ```
   @feature-brainstormer - Brainstorm features for [topic/problem]
   
   Example:
   @feature-brainstormer - Brainstorm "AI-powered document preparation for mobile"
   based on user research showing 35% of signatures on mobile but high frustration
   ```

3. **Review Brainstorming Output**
   ```
   Output location: brainstorm/[feature-name]/
   Files created:
   - SUMMARY.md (top ideas, evaluations, roadmap)
   - IDEAS.md (all raw ideas)
   - NEXT_STEPS.md (recommendations)
   ```

4. **Validate with Stakeholders** (Manual)
   - Review top 5-10 ideas with team
   - Gather feedback on priorities
   - Adjust based on business constraints

**Duration**: 1-2 hours (agent work) + 2-4 hours (validation)

**Output**: 
- ✅ 15-20 evaluated feature ideas
- ✅ Prioritized roadmap (3 phases)
- ✅ Next steps with agent collaboration plan

---

### Stage 2: Competitive Analysis (Optional)
**Goal**: Understand competitor capabilities and positioning strategy

**When to Use**:
- New feature category for your product
- Competitive differentiation is critical
- Uncertain about market standards

**Steps**:

1. **Research Competitor Capabilities** (manual research or web search)
   ```
   Context: brainstorm/[feature-name]/SUMMARY.md

   Focus areas:
   - What features do DocuSign, Adobe Sign, HelloSign offer?
   - How are they positioning AI capabilities?
   - What are gaps we can exploit?
   ```

2. **Document Competitive Analysis**
   ```
   Output location: product_documents/competitive-[feature-name]/
   Files:
   - competitor-matrix.md (feature comparison)
   - positioning-strategy.md (differentiation recommendations)
   ```

**Duration**: 2-3 hours

**Output**:
- ✅ Competitive feature matrix
- ✅ Positioning recommendations
- ✅ Differentiation strategy

---

### Stage 3: Requirements Analysis
**Goal**: Transform feature ideas into detailed requirements with acceptance criteria

**Steps**:

1. **Use Requirements Analyst Skill**
   ```
   Use the requirements-analyst skill to create detailed requirements for features in
   brainstorm/ai-mobile-document-prep/SUMMARY.md

   Focus on top 5 features:
   1. Computer Vision Field Detection
   2. Confidence Scores + Visual Indicators
   3. Document Understanding + Contact Intelligence
   4. One-Tap Scan & Prep
   5. AI Pre-Flight Check
   ```

2. **Review Requirements**
   ```
   Output location: requirements/[feature-name]/
   Files:
   - functional-requirements.md (detailed requirements by feature)
   - non-functional-requirements.md (performance, security, scalability)
   - acceptance-criteria.md (testable conditions)
   - edge-cases.md (scenarios to handle)
   ```

3. **Validate with Engineering** (Manual)
   - Review technical feasibility
   - Identify unknowns requiring spikes
   - Confirm acceptance criteria are testable

**Duration**: 3-4 hours (agent work) + 2 hours (validation)

**Output**:
- ✅ Functional requirements document
- ✅ Non-functional requirements
- ✅ Detailed acceptance criteria
- ✅ Edge case documentation

---

### Stage 4: Backlog Management
**Goal**: Create INVEST-compliant user stories ready for sprint planning

**Steps**:

1. **Use Backlog Manager Skill**
   ```
   Use the backlog-manager skill to create user stories for features in
   brainstorm/ai-mobile-document-prep/SUMMARY.md

   Use requirements from: requirements/ai-mobile-document-prep/
   Create stories for Phase 1 features (3-month timeline)
   ```

2. **Review User Stories**
   ```
   Output location: backlog/[feature-name]/
   Files:
   - US-001-[feature-name].md
   - US-002-[feature-name].md
   - ...
   - README.md (backlog summary)
   
   Each story includes:
   - User story format (As a... I want... So that...)
   - Acceptance criteria
   - Definition of Done
   - Dependencies
   - Estimated effort (story points)
   - Success metrics
   ```

3. **Validate INVEST Principles** (Automatic)
   - Independent: Can be developed separately
   - Negotiable: Flexibility in implementation
   - Valuable: Clear business value
   - Estimable: Team can estimate effort
   - Small: Fits in 1-2 sprints
   - Testable: Clear acceptance criteria

4. **Refine with Team** (Manual)
   - Review story points with engineering
   - Adjust priorities based on dependencies
   - Break down large stories (>13 points)

**Duration**: 2-3 hours (agent work) + 2 hours (refinement)

**Output**:
- ✅ 5-15 INVEST-compliant user stories
- ✅ Story point estimates
- ✅ Dependency mapping
- ✅ Backlog README with sprint recommendations

---

### Stage 5: Sprint Planning
**Goal**: Create actionable sprint plan with capacity planning and goals

**Steps**:

1. **Use Sprint Planner Skill**
   ```
   Use the sprint-planner skill to create a 2-week sprint plan using stories from
   backlog/ai-mobile-document-prep/

   Team capacity:
   - 2 ML engineers (80 hours each)
   - 3 mobile engineers (80 hours each)
   - 2 backend engineers (80 hours each)
   - 1 QA engineer (80 hours)

   Sprint goal: Deliver Computer Vision Field Detection MVP
   ```

2. **Review Sprint Plan**
   ```
   Output location: sprints/sprint-[number]/
   Files:
   - sprint-plan.md (goals, capacity, commitments)
   - daily-standup-template.md
   - sprint-board.md (backlog, in-progress, done)
   ```

3. **Conduct Sprint Planning Meeting** (Manual)
   - Review sprint goal with team
   - Confirm story commitments
   - Identify blockers and dependencies
   - Assign stories to team members

**Duration**: 1 hour (agent work) + 2 hours (sprint planning meeting)

**Output**:
- ✅ Sprint goal
- ✅ Committed user stories
- ✅ Capacity plan
- ✅ Risk identification

---

### Stage 6: Documentation
**Goal**: Create technical and user-facing documentation

**Steps**:

1. **Use Documentation Specialist Skill**
   ```
   Use the documentation-specialist skill to create documentation for features in sprint-1/

   Document types needed:
   - Technical design (architecture, APIs, data models)
   - User guide (how to use AI document preparation)
   - API documentation (field detection endpoints)
   - Developer guide (integration instructions)
   ```

2. **Review Documentation**
   ```
   Output location: docs/features/[feature-name]/
   Files:
   - technical-design.md
   - user-guide.md
   - api-documentation.md
   - developer-guide.md
   ```

3. **Validate with Stakeholders** (Manual)
   - Engineering reviews technical design
   - Product reviews user guide
   - DevRel reviews API docs

**Duration**: 2-3 hours (agent work) + 1 hour (review)

**Output**:
- ✅ Technical design document
- ✅ User documentation
- ✅ API documentation
- ✅ Developer guides

---

## Complete Example: AI Mobile Document Prep

### Timeline
**Total Duration**: 2-3 days (agents working in sequence or parallel)

### Day 1: Discovery
1. ✅ **Brainstorming** (2 hours)
   - Agent: @feature-brainstormer
   - Output: 65+ ideas, top 15 prioritized, 3-phase roadmap

2. ✅ **Competitive Analysis** (2 hours, parallel with requirements)
   - Manual research / web search
   - Output: Competitor matrix, positioning strategy

3. ✅ **Requirements Analysis** (3 hours, parallel with competitive)
   - Skill: requirements-analyst
   - Output: Functional/non-functional requirements, acceptance criteria

### Day 2: Planning
4. ✅ **Backlog Creation** (2 hours)
   - Skill: backlog-manager
   - Output: 3 user stories, INVEST-validated, story points

5. ✅ **Sprint Planning** (1 hour + 2 hours team meeting)
   - Skill: sprint-planner
   - Output: Sprint plan, capacity allocation, goals

### Day 3: Documentation & Refinement
6. ✅ **Documentation** (2 hours)
   - Skill: documentation-specialist
   - Output: Technical design, user guides, API docs

7. ✅ **Refinement** (4 hours, manual)
   - Team reviews, adjustments, final validation

---

## Workflow Variations

### Fast Track (Same Day)
**When**: Small feature, low complexity, clear requirements
**Agents**: 2-3 agents in sequence
**Duration**: 4-6 hours

```
1. Brainstorming (1 hour) → 2. Backlog (1 hour) → 3. Sprint Planning (1 hour)
Skip: Competitive analysis, detailed requirements
```

### Deep Analysis (1-2 Weeks)
**When**: Strategic feature, high investment, uncertain requirements
**Agents**: 6-8 agents with multiple validation loops
**Duration**: 1-2 weeks

```
1. User Research → 2. Brainstorming → 3. Competitive Analysis →
4. Risk Assessment → 5. Requirements Analysis → 6. Backlog Creation →
7. Sprint Planning → 8. Documentation → 9. Stakeholder Review
```

### Iterative Approach (Ongoing)
**When**: Feature evolves based on user feedback, phased rollout
**Agents**: Continuous agent involvement with feedback loops

```
Sprint 1: Build MVP → Analytics → User Research → Brainstorming (improvements) →
Sprint 2: Build v2 → Analytics → ...
```

---

## Best Practices

### 1. Prepare Context Upfront
✅ **Do**: Add comprehensive product docs to `product_documents/` before starting
❌ **Don't**: Invoke agents without context (they'll make assumptions)

### 2. Use Agents in Sequence
✅ **Do**: Wait for one agent to complete before invoking dependent agents
❌ **Don't**: Run all agents in parallel without considering dependencies

**Dependency Flow**:
```
brainstorming (@feature-brainstormer) → requirements (skill) → backlog (skill) → sprint planning (skill)
                ↓
           competitive analysis (manual/web research, parallel with requirements)
```

### 3. Validate Agent Outputs
✅ **Do**: Review agent outputs with team before proceeding
❌ **Don't**: Assume agent outputs are final without human validation

### 4. Iterate Based on Feedback
✅ **Do**: Refine stories, adjust priorities, add missing requirements
❌ **Don't**: Treat first pass as final deliverable

### 5. Document Decisions
✅ **Do**: Use ADRs (Architecture Decision Records) for key decisions
❌ **Don't**: Make decisions without documentation

---

## Troubleshooting

### Problem: Brainstorming output is too generic
**Solution**: 
- Add more specific product context to `product_documents/`
- Include user quotes, metrics, pain points
- Provide competitor examples to differentiate against

### Problem: User stories lack technical detail
**Solution**:
- Run requirements-analyst agent first to create detailed requirements
- Reference requirements when invoking backlog-manager
- Add technical notes to stories during refinement

### Problem: Sprint plan is unrealistic
**Solution**:
- Validate story points with engineering team
- Adjust capacity based on team availability
- Break down large stories (>13 points) into smaller chunks

### Problem: Dependencies block progress
**Solution**:
- Map dependencies explicitly in user stories
- Prioritize foundational stories first
- Use sprint-planner to identify critical path

---

## Metrics to Track

### Process Efficiency
- **Time to create user stories**: Target < 4 hours (from brainstorming to backlog)
- **Agent output quality**: Human review required (target: minimal edits)
- **Story refinement rounds**: Target 1-2 rounds before sprint commitment

### Outcome Quality
- **Story completeness**: All INVEST criteria met (100% target)
- **Acceptance criteria clarity**: QA can write tests without clarification (target: >90%)
- **Sprint commitment accuracy**: Stories completed vs committed (target: >80%)

### Team Satisfaction
- **Product confidence**: Team understands "why" behind stories (survey)
- **Planning efficiency**: Time spent in sprint planning (target: <2 hours)
- **Documentation usefulness**: Developers reference docs (usage tracking)

---

## Next Steps

After completing this workflow:

1. **Execute Sprint**: Developers build features based on user stories
2. **Track Progress**: Use sprint-planner for daily tracking
3. **Gather Feedback**: Use analytics-insights agent to measure outcomes
4. **Iterate**: Based on results, refine features or plan next sprint

---

## Related Workflows

- [Brainstorming Workflow](./brainstorming-workflow.md) - Deep dive on ideation process
- [Sprint Planning Workflow](./sprint-planning-workflow.md) - Detailed sprint planning steps

---

## Questions?

If you encounter issues or have suggestions for improving this workflow, document them in `docs/workflows/workflow-feedback.md` and share with the team.
