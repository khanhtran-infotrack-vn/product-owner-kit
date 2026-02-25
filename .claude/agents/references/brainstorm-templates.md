# Brainstorm Output Templates

Reference file for `feature-brainstormer` agent. Load with Read when creating output files.

---

## SUMMARY.md Template

Save to `brainstorm/[feature_name]/SUMMARY.md`:

```markdown
# [Feature Name] Brainstorming Session

**Date**: YYYY-MM-DD
**Participants**: Product Owner, AI Agent
**Status**: In Progress / Completed

---

## Problem Statement / Opportunity

[Clear description of what we're brainstorming about]

**Context**:
- Current situation
- User pain points
- Market opportunity
- Strategic importance

---

## Ideas Generated

### Idea 1: [Title]
**Description**: [What is it?]
**User Benefit**: [Why would users care?]
**Business Impact**: [Revenue, retention, acquisition?]

**Evaluation Scores**:
- User Value: X/5
- Business Impact: X/5
- Technical Feasibility: X/5
- **Overall Score**: XX/15

**Pros**: [Advantage 1], [Advantage 2]
**Cons**: [Challenge 1], [Challenge 2]
**Dependencies**: [List]
**Risks**: [List]

[Repeat for each idea]

---

## Comparative Analysis

| Idea | User Value | Business | Feasibility | Total | Rank |
|------|-----------|----------|-------------|-------|------|
| Idea 1 | 5 | 4 | 3 | 12 | 1 |

---

## Idea Clusters

| Cluster | Theme | Ideas Included | Novelty | Feasibility | Impact | Selected |
|---------|-------|---------------|---------|-------------|--------|----------|
| A | [Theme] | #1, #3, #7 | X/5 | X/5 | X/5 | Yes/No |

---

## Challenge & Critique Findings

### Pre-Mortem Results
| Top Idea | Most Likely Failure Mode | Likelihood | Impact |
|----------|------------------------|-----------|--------|
| [Idea 1] | [Failure scenario] | X/5 | X/5 |

### Assumption Stress-Test
| Assumption | Evidence Level | If Wrong... | Blast Radius |
|------------|---------------|-------------|--------------|
| [Assumption] | Strong/Weak/None | [Consequence] | High/Medium/Low |

### Devil's Advocate — Strongest Objections
- **[Idea 1]**: [Strongest counter-argument]

### Ranking Changes After Challenge
| Idea | Pre-Challenge Rank | Post-Challenge Rank | Change Reason |
|------|-------------------|---------------------|---------------|
| [Idea 1] | #1 | #1 | Confirmed: [reason] |

**Challenge Summary**: [1-2 sentences]

---

## Recommended Approach

**Top Choice**: [Idea name]
**Rationale**: [Why this is the best option]

**Implementation Strategy**:
1. Phase 1: [MVP scope]
2. Phase 2: [Enhancements]
3. Phase 3: [Advanced features]

**Alternative Approach**: [Backup option]

---

## Next Steps

1. [ ] Validate assumptions with user research (analytics-insights skill)
2. [ ] Analyze competitive landscape
3. [ ] Create detailed requirements (requirements-analyst skill)
4. [ ] Break down into user stories (backlog-manager skill)
5. [ ] Assess technical risks (review with engineering team)
6. [ ] Prioritize against backlog (prioritization-engine skill)

---

## Questions to Resolve

1. [Open question 1]

---

## Parking Lot (Ideas for Later)

- [Idea we can't do now but want to remember]
```

---

## IDEAS.md Template

Save to `brainstorm/[feature_name]/IDEAS.md`:

```markdown
# [Feature Name] — All Ideas Generated

**Date**: YYYY-MM-DD
**Session**: Unfiltered idea generation

[All ideas as generated, grouped by domain rotation cluster]

## Domain Rotation Used
Technology → UX → Business Model → Edge Cases → Operations → Security → Compliance
```

---

## User Story Template (US-001.md)

Save to `brainstorm/[feature_name]/user-stories/US-001-[name].md`:

```markdown
# US-001: [Feature Name]

**Story ID**: US-001
**Epic**: [Epic name]
**Priority**: HIGH/MEDIUM/LOW
**Status**: Draft
**Created**: YYYY-MM-DD

---

## User Story

**As a** [user persona]
**I want** [capability]
**So that** [benefit/value]

---

## Business Context

**Problem**: [From brainstorming problem statement]
**Opportunity**: [Business Impact score rationale]
**User Impact**: [User Value score rationale]

---

## Draft Acceptance Criteria

1. **Given** [precondition] **When** [action] **Then** [expected outcome]
2. [Repeat for 3-5 key scenarios]

---

## Estimated Effort (Draft)

**Story Points**: [1/2/3/5/8/13] (Feasibility 5→1-2pts, 4→3-5pts, 3→5-8pts, 2→8-13pts, 1→13+pts)
**Estimated Time**: [Based on story points]

---

## Dependencies / Risks

[From brainstorming evaluation]

---

## Notes

- Source: Brainstorming session YYYY-MM-DD
- Brainstorm Rank: #[X] (Score: [Y]/15)
- Status: Draft — requires refinement with engineering team
```

---

## User Stories README Template

Save to `brainstorm/[feature_name]/user-stories/README.md`:

```markdown
# Draft User Stories — [Feature Name]

**Generated**: YYYY-MM-DD
**Source**: Brainstorming session — see ../SUMMARY.md
**Status**: Draft (requires team review)

## Stories

| Story ID | Title | Priority | Points | Status |
|----------|-------|----------|--------|--------|
| US-001 | [Title] | HIGH | 8 | Draft |

**Total Story Points**: [X]

## Next Steps

1. Review with team — validate structure, refine criteria, confirm estimates
2. Use requirements-analyst skill for complex stories
3. Use backlog-manager skill to add refined stories to backlog
4. Use sprint-planner skill when stories are ready

⚠️ Estimates are preliminary. Final estimates require team consensus.
```

---

## Story Point Estimation (from agile-product-owner skill)

| Points | Complexity | Timeline | Feasibility Score |
|--------|-----------|----------|------------------|
| 1-2 | Trivial/Simple | Hours–1 day | 5 (simple) |
| 3-5 | Small/Medium | 2-5 days | 4 (straightforward) |
| 5-8 | Medium | 3-5 days | 3 (moderate) |
| 8-13 | Large/Very Large | 1-3 weeks | 2 (complex) |
| 13+ | Enormous — split | 3+ weeks | 1 (very complex) |
