---
name: sprint-planner
description: Assist with sprint planning by analyzing team capacity, story points, dependencies, and recommending optimal sprint compositions. Use when asked to "plan next sprint", "what's our capacity", "suggest sprint composition", "are we overcommitted", "balance story types", or "identify sprint risks".
---

# Sprint Planner

## Core Capabilities
- Calculate team capacity (accounting for holidays, PTO, meetings)
- Recommend stories for sprint based on priority and capacity
- Identify blocking dependencies
- Suggest sprint goals
- Balance story types (features, bugs, tech debt)
- Flag overcommitment risks
- Analyze velocity trends

## Output Example

```markdown
## Sprint [Number] Plan

### Team Capacity
- Total: 40 points
- Available: 35 points (holidays: 5 points)
- Recommended commitment: 28-32 points (80-90% of capacity)

### Recommended Stories

**High Priority (Must Include):**
- STORY-101: Auto tag API (8 pts)
- STORY-105: Bug fixes batch (3 pts)

**Medium Priority (Should Include):**
- STORY-110: Email templates (5 pts)
- STORY-112: Performance tuning (5 pts)

**Buffer (If Capacity Allows):**
- STORY-115: UI polish (3 pts)

### Sprint Goal
"Deliver auto-tag placement MVP and resolve critical bugs"

### Dependencies
✓ All dependencies resolved
⚠ STORY-101 requires design review (scheduled)

### Risks
- New technology (ML integration) - add spike if needed
- Holiday week - reduced capacity
- External API dependency

### Composition Balance
- Features: 60% (21 pts)
- Bugs: 15% (5 pts)
- Tech Debt: 10% (3 pts)
- Buffer: 15% (5 pts)

### Velocity Analysis
- Last 3 sprints average: 30 points
- Commitment: 29 points (within historical range)
- Confidence: High
```

## Best Practices

### Capacity Calculation
- Account for holidays, PTO, training
- Reserve 20-30% for meetings, support, unplanned work
- Use historical velocity as guide
- Don't overcommit - better to under-promise and over-deliver

### Story Selection
- Start with highest priority items
- Check dependencies are met
- Balance quick wins with strategic work
- Include mix of features, bugs, and tech debt
- Leave buffer for unknowns

### Risk Identification
- New technology or approaches
- External dependencies
- Team member availability
- Unclear requirements
- Technical complexity
