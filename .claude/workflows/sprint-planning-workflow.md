# Sprint Planning Workflow

## Overview
This workflow guides you through creating effective sprint plans using the **sprint-planner agent**, from backlog refinement through sprint commitment and daily execution.

**Time to Complete**: 2-3 hours (preparation + meeting)
**Skill**: sprint-planner
**Output**: Sprint plan, capacity allocation, goals, and tracking board

---

## When to Use This Workflow

### Standard Sprint Planning (Every 1-2 Weeks)
Use this workflow at the start of each sprint to:
- Select user stories from backlog
- Estimate team capacity
- Define sprint goal
- Commit to deliverables
- Plan daily standups

### Ad-Hoc Planning (As Needed)
Use this workflow when:
- Starting new project or initiative
- Team composition changes (new members, vacations)
- Priorities shift mid-sprint (re-planning needed)
- Scaling to multiple teams (coordination required)

---

## Prerequisites

### Required Inputs

1. **Refined Backlog**
   ```
   Location: backlog/[feature-name]/
   Content:
   - User stories with acceptance criteria
   - Story point estimates
   - Dependencies mapped
   - Priority assigned (HIGH/MEDIUM/LOW)
   ```

2. **Team Capacity**
   ```
   Know for each team member:
   - Role (frontend, backend, ML, QA, design)
   - Availability (hours per sprint, accounting for PTO, meetings)
   - Skills (what stories can they work on?)
   ```

3. **Sprint Parameters**
   ```
   - Sprint duration (1-2 weeks typical)
   - Sprint start date
   - Sprint end date
   - Team velocity (average story points completed per sprint)
   ```

### Optional Context (Helpful)

4. **Previous Sprint Metrics**
   - Stories completed vs committed
   - Velocity trend (increasing/decreasing)
   - Blockers encountered
   - Lessons learned

5. **Dependencies & Risks**
   - External dependencies (other teams, vendors)
   - Technical unknowns requiring spikes
   - Infrastructure or tooling limitations

---

## Step-by-Step Workflow

### Step 1: Pre-Planning Preparation (30-60 minutes)

**1.1 Backlog Refinement (if not already done)**

Ensure user stories are "sprint-ready" (INVEST-compliant):
- [ ] **Independent**: Can be developed without blocking on other stories
- [ ] **Negotiable**: Flexibility in implementation approach
- [ ] **Valuable**: Clear business value articulated
- [ ] **Estimable**: Team can confidently estimate effort
- [ ] **Small**: Fits within 1 sprint (< 13 story points)
- [ ] **Testable**: Acceptance criteria are clear and measurable

**If stories need refinement:**
```
Use the backlog-manager skill to review and refine stories in backlog/[feature-name]/
Ensure INVEST compliance for sprint planning
```

**1.2 Calculate Team Capacity**

**Formula**: `Available hours = Team size × Sprint hours - Meetings - PTO`

**Example** (2-week sprint):
```
Team composition:
- 2 ML engineers × 80 hours = 160 hours
- 3 mobile engineers × 80 hours = 240 hours
- 2 backend engineers × 80 hours = 160 hours
- 1 QA engineer × 80 hours = 80 hours
Total theoretical: 640 hours

Subtract:
- Meetings (standups, planning, retro): 10 hours/person = 80 hours
- PTO (1 engineer on vacation): 80 hours
- Buffer (sick days, interruptions): 10% = 48 hours

Available capacity: 640 - 80 - 80 - 48 = 432 hours
```

**1.3 Review Sprint Goal Options**

Sprint goal should be:
- **Focused**: One clear objective (not "complete 10 stories")
- **Valuable**: Delivers user or business value
- **Achievable**: Realistic given capacity
- **Inspiring**: Motivates the team

**Examples**:
- ✅ "Deliver Computer Vision Field Detection MVP for beta users"
- ✅ "Complete mobile app redesign and launch to 10% of users"
- ✅ "Reduce document preparation time by 40% with AI assistance"
- ❌ "Complete US-001, US-002, US-003" (not inspiring)
- ❌ "Work on AI features" (too vague)

---

### Step 2: Use Sprint Planner Skill (15-30 minutes)

**2.1 Craft Sprint Planning Prompt**

Use this template:
```
Use the sprint-planner skill to create a sprint plan for Sprint [number]

Backlog location: backlog/[feature-name]/

Team capacity:
- [Role 1]: [Number] engineers × [Hours] = [Total hours]
- [Role 2]: [Number] engineers × [Hours] = [Total hours]
- Total available: [Total hours]

Sprint parameters:
- Duration: [1-2 weeks]
- Start date: [Date]
- End date: [Date]
- Velocity (previous 3 sprints): [Story points per sprint]

Sprint goal: [One sentence describing primary objective]

Priority stories (in order):
1. [Story ID] - [Story title] ([Story points])
2. [Story ID] - [Story title] ([Story points])
3. [Story ID] - [Story title] ([Story points])
...

Constraints:
- [Any known blockers, dependencies, or limitations]
```

**Example**:
```
Use the sprint-planner skill to create a sprint plan for Sprint 12

Backlog location: backlog/ai-mobile-prep/

Team capacity:
- ML engineers: 2 × 80 hours = 160 hours
- Mobile engineers: 3 × 80 hours = 240 hours
- Backend engineers: 2 × 80 hours = 160 hours
- QA engineer: 1 × 80 hours = 80 hours
Total available: 640 hours (minus 208 hours overhead) = 432 hours

Sprint parameters:
- Duration: 2 weeks
- Start date: February 10, 2026
- End date: February 21, 2026
- Velocity (previous 3 sprints): 28, 32, 30 points (avg: 30 points)

Sprint goal: Deliver Computer Vision Field Detection MVP for beta testing

Priority stories (in order):
1. US-001 - Computer Vision Field Detection (13 points)
2. US-002 - Confidence Scores + Visual Indicators (5 points)
3. US-003 - Document Understanding + Contact Intelligence (8 points)

Constraints:
- ML infrastructure requires AWS SageMaker setup (2-day lead time)
- Mobile team has 1 engineer on PTO week 2
```

**2.2 What the Agent Produces (Automatic)**

The sprint-planner agent will create:

1. **Sprint Plan** (`sprints/sprint-[number]/sprint-plan.md`)
   - Sprint goal and success criteria
   - Committed user stories with assignments
   - Capacity allocation by role
   - Risk identification and mitigation
   - Daily standup schedule

2. **Sprint Board** (`sprints/sprint-[number]/sprint-board.md`)
   - Backlog (stories not yet started)
   - In Progress (stories being worked on)
   - In Review (stories awaiting QA/approval)
   - Done (completed stories meeting DoD)

3. **Daily Standup Template** (`sprints/sprint-[number]/daily-standup-template.md`)
   - Template for recording daily progress
   - Blocker tracking
   - Burndown chart (manual or automated)

**Duration**: 15-30 minutes (agent processes in background)

---

### Step 3: Review Sprint Plan Draft (15-20 minutes)

**3.1 Output Location**
```
sprints/sprint-[number]/
├── sprint-plan.md           # Goals, capacity, commitments
├── sprint-board.md          # Kanban board (Backlog/In Progress/Review/Done)
└── daily-standup-template.md
```

**3.2 Validation Checklist**

Review sprint-plan.md and verify:

**Goal & Scope**:
- [ ] Sprint goal is clear, focused, and valuable
- [ ] Committed stories align with sprint goal
- [ ] Success criteria are measurable

**Capacity & Commitment**:
- [ ] Total story points ≤ team velocity (don't overcommit!)
- [ ] Capacity allocation by role is balanced (no single bottleneck)
- [ ] Buffer exists for unknowns (aim for 80% capacity utilization)

**Dependencies & Risks**:
- [ ] All dependencies are identified and mitigated
- [ ] High-risk stories have contingency plans
- [ ] External blockers are escalated upfront

**Team Assignment**:
- [ ] Each story has an owner or pair assigned
- [ ] Skills match story requirements (ML story → ML engineer)
- [ ] No team member overloaded (check individual capacity)

**3.3 Common Adjustments**

**If overcommitted** (story points > velocity):
- Remove lowest-priority stories
- Split large stories (>13 points) into smaller chunks
- Defer "nice-to-have" stories to next sprint

**If undercommitted** (story points < 80% of velocity):
- Add more stories from backlog (prioritized order)
- Include technical debt or refactoring work
- Plan spikes for future features

**If dependencies are blocking**:
- Escalate external dependencies to unblock
- Reorder stories to work on independent items first
- Plan parallel workstreams to reduce waiting

---

### Step 4: Sprint Planning Meeting (1-2 hours)

**4.1 Meeting Structure**

**Attendees**: Product Manager, Engineering Team, Scrum Master (if applicable), QA, Design

**Agenda**:

**Part 1: Sprint Review & Context** (15 minutes)
- Review previous sprint metrics (what went well, what didn't)
- Recap product roadmap and strategic priorities
- Introduce sprint goal for current sprint

**Part 2: Story Walkthrough** (30-45 minutes)
- Review each committed story in priority order
- Clarify acceptance criteria and definition of done
- Discuss implementation approach (high-level)
- Confirm story point estimates (team agreement)
- Identify dependencies and risks

**Part 3: Capacity Planning** (15-20 minutes)
- Review team capacity and availability
- Assign stories to team members (volunteer model preferred)
- Validate commitment (can we achieve sprint goal with these stories?)

**Part 4: Sprint Commitment** (10 minutes)
- Team confirms commitment to sprint goal and stories
- Document any concerns or caveats
- Set up daily standup schedule (time, location/tool)

**4.2 Facilitation Tips**

✅ **Do**:
- Encourage team to ask questions and raise concerns
- Focus on "what" and "why" (not "how" in detail)
- Keep discussion high-level (deep dives in separate meetings)
- Time-box discussions (move detailed debates offline)
- Capture decisions and action items

❌ **Don't**:
- Dictate story assignments (let team self-organize)
- Skip story details (causes confusion during sprint)
- Ignore risks or dependencies (surfaces as blockers later)
- Overload sprint (better to undercommit and overdeliver)

---

### Step 5: Sprint Execution & Tracking (Daily)

**5.1 Daily Standup**

**Format** (15 minutes max):
- Each team member shares:
  1. **Yesterday**: What I completed
  2. **Today**: What I'm working on
  3. **Blockers**: Anything preventing progress

**Update sprint-board.md** after standup:
```markdown
## Sprint Board (Updated: Feb 11, 2026)

### In Progress
- [US-001] Computer Vision Field Detection (Alice, Bob - ML model training 60% complete)
- [US-002] Confidence Scores (Carol - UI mockups done, coding started)

### In Review
- [US-000] Set up ML infrastructure (Dave - awaiting QA approval)

### Done
- [US-004] Update dependencies

### Blockers
- AWS SageMaker quotas insufficient (escalated to DevOps - ETA: Feb 12)
```

**5.2 Burndown Tracking**

Track progress daily:
```
Day 1: 26 story points remaining
Day 2: 24 story points remaining
Day 3: 22 story points remaining
...
Day 10: 0 story points remaining (sprint complete!)
```

**If burndown is trending poorly**:
- Identify blockers and resolve ASAP
- Re-scope sprint (remove low-priority stories)
- Ask for help (pair programming, additional resources)

**5.3 Mid-Sprint Check-In** (Optional, Day 5-7)

If sprint is at risk, conduct mid-sprint review:
- Are we on track to meet sprint goal?
- Do we need to adjust scope?
- Are there blockers we can't resolve internally?

**Decision options**:
- **Stay the course**: Sprint is on track, continue
- **Re-scope**: Remove stories to ensure goal is met
- **Escalate**: Bring in additional resources or leadership support

---

### Step 6: Sprint Completion & Handoff

**6.1 Definition of Done (DoD) Checklist**

Before marking story as "Done", verify:
- [ ] Code complete and merged to main branch
- [ ] Unit tests written and passing (>80% coverage)
- [ ] Integration tests passing
- [ ] QA manual testing complete (acceptance criteria validated)
- [ ] Documentation updated (technical docs, user guides)
- [ ] Product Owner accepts story (demo conducted)
- [ ] No known bugs or issues (or triaged to backlog)

**6.2 Demo & Review**

At end of sprint:
- Demo completed stories to stakeholders
- Gather feedback for future iterations
- Celebrate wins! 🎉

**6.3 Handoff to Next Sprint**

Update backlog for next sprint:
- Move incomplete stories back to backlog (re-prioritize)
- Create new stories based on learnings
- Document technical debt or follow-up work

---

## Sprint Planning Anti-Patterns

### Anti-Pattern 1: No Clear Sprint Goal
**Problem**: Team commits to random stories without unifying objective

**Impact**: Lack of focus, low team motivation, hard to make trade-off decisions

**Solution**: Define ONE clear sprint goal before selecting stories

---

### Anti-Pattern 2: Overcommitment
**Problem**: Committing to 40 story points when velocity is 28 points

**Impact**: Team stress, rushed work, incomplete stories, sprint failure

**Solution**: Use historical velocity as guide, aim for 80-90% capacity utilization

---

### Anti-Pattern 3: Ignoring Dependencies
**Problem**: Committing to US-002 which depends on US-001, but US-001 isn't prioritized

**Impact**: Blocked work, wasted time, missed sprint goal

**Solution**: Map dependencies upfront, ensure foundational stories are prioritized first

---

### Anti-Pattern 4: No Buffer for Unknowns
**Problem**: Planning 100% of capacity with zero slack

**Impact**: Any hiccup (sick day, bug, miscommunication) causes sprint failure

**Solution**: Reserve 10-20% buffer for unplanned work, bugs, unknowns

---

### Anti-Pattern 5: Product Owner Dictates Estimates
**Problem**: PM says "This should be 3 points" but team believes it's 8 points

**Impact**: Inaccurate estimates, team resentment, commitment not genuine

**Solution**: Team owns estimates (they're doing the work!), PM influences priority

---

## Advanced Sprint Planning

### Multi-Team Sprint Planning
**When**: Multiple teams working on same product/feature

**Approach**:
1. Each team plans separately (parallel sprint planning)
2. Identify cross-team dependencies
3. Conduct coordination meeting (representatives from each team)
4. Adjust plans to resolve conflicts

**Tools**:
- Dependency matrix (Team A needs X from Team B by Day 5)
- Cross-team standup (weekly or bi-weekly)
- Shared sprint board (visibility into other teams' progress)

---

### Spike Stories for Unknowns
**When**: High uncertainty requires investigation before committing

**Example**:
```
Story: [SPIKE] Evaluate ML model accuracy for field detection
- Time-boxed: 2 days
- Output: Technical report with accuracy metrics, recommendations
- Success criteria: Enough information to estimate US-001 confidently
```

**Include spikes in sprint plan**:
- Treat as regular stories (assign points, track progress)
- Conduct spike early in sprint (informs other work)
- Document findings for team visibility

---

### Rolling Wave Planning
**When**: Long-term project (3+ months) with evolving requirements

**Approach**:
- Plan next sprint in detail (commit to stories)
- Plan following 2-3 sprints at high level (epics, themes)
- Revisit and refine each sprint (adjust based on learnings)

**Benefits**:
- Flexibility to adapt to changing priorities
- Reduces wasted planning effort on distant work
- Maintains long-term vision while allowing tactical adjustments

---

## Metrics to Track

### Sprint Health Metrics
- **Velocity**: Story points completed per sprint (track trend over 3+ sprints)
- **Commitment accuracy**: % of committed stories completed (target: >80%)
- **Sprint goal achievement**: Did we meet the sprint goal? (Yes/No)
- **Blocker frequency**: # of blockers per sprint (lower is better)

### Team Metrics
- **Capacity utilization**: Actual hours worked / Available hours (target: 80-90%)
- **Story cycle time**: Days from "In Progress" to "Done" (lower is better)
- **Defect rate**: Bugs found per story (target: <0.5)

### Process Metrics
- **Planning time**: Hours spent in sprint planning (target: <5% of sprint time)
- **Standup duration**: Minutes per daily standup (target: <15 min)
- **Mid-sprint changes**: # of stories added/removed mid-sprint (target: 0)

---

## Related Workflows

- [Feature Development Workflow](./feature-development-workflow.md) - Complete feature delivery
- [Brainstorming Workflow](./brainstorming-workflow.md) - Generate ideas before planning

---

## Questions & Feedback

For sprint planning questions or workflow improvements, document in:
`docs/workflows/workflow-feedback.md`
