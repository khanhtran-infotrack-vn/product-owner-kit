# Brainstorming Sessions Folder

This folder contains results from all brainstorming sessions facilitated by @feature-brainstormer.

## Purpose

Store structured brainstorming outputs to:
- Track feature ideation history
- Reference previous explorations
- Build on past ideas
- Maintain institutional knowledge

## Folder Structure

Each brainstorming session creates a subfolder:

```
brainstorm/
├── [feature-name-1]/
│   ├── SUMMARY.md              # Main brainstorming summary
│   ├── ideas-raw.md            # All ideas as generated
│   ├── user-stories-draft.md  # Draft stories for top ideas
│   ├── mockups/                # Optional: sketches/wireframes
│   └── references.md           # Links to inspiration
│
├── [feature-name-2]/
│   └── ...
│
└── index.md                    # Index of all sessions
```

## Brainstorming Session Lifecycle

### 1. Ideation (In Progress)
```
brainstorm/mobile-signature-improvements/
└── SUMMARY.md (Status: In Progress)
```

### 2. Evaluation (Completed)
```
brainstorm/mobile-signature-improvements/
├── SUMMARY.md (Status: Completed)
├── ideas-raw.md (7 ideas generated)
└── user-stories-draft.md (Top 3 concepts)
```

### 3. Implementation (Moved to Backlog)
```
brainstorm/mobile-signature-improvements/
├── SUMMARY.md (Status: Implemented)
├── implementation-notes.md
└── retrospective.md (What we learned)
```

## Session Index

Maintain an index of all brainstorming sessions:

### Active Sessions (In Progress)
- None

### Completed Sessions (Ready for Next Steps)
- None

### Implemented Features (Shipped)
- None

### Parked Ideas (Future Consideration)
- None

## How to Use This Folder

### Starting a New Brainstorming Session

```
User: "@feature-brainstormer let's brainstorm ways to improve mobile signature"

Agent creates:
brainstorm/mobile-signature-improvements/
└── SUMMARY.md (with all ideas, evaluations, recommendations)
```

### Reviewing Past Sessions

```
User: "What did we brainstorm about mobile features?"

Agent: 
1. Uses Grep to search brainstorm/ folder
2. Finds relevant sessions
3. Summarizes key ideas and outcomes
```

### Building on Previous Ideas

```
User: "We brainstormed offline mode last month. Let's expand on that."

Agent:
1. Reads brainstorm/offline-mode-exploration/
2. Reviews ideas and parking lot
3. Continues brainstorming from where we left off
```

## Brainstorming Session Template

When @feature-brainstormer creates a new session, it follows this structure:

```markdown
# [Feature Name] Brainstorming Session

**Date**: YYYY-MM-DD
**Status**: In Progress / Completed / Implemented
**Priority**: High / Medium / Low

---

## Problem Statement
[What are we solving?]

## Ideas Generated
[5-10 evaluated ideas]

## Recommended Approach
[Top choice with rationale]

## Next Steps
[Actions and responsible agents]

## Related Documents
[Links to product_documents/]

## Parking Lot
[Ideas for later]
```

## Best Practices

### During Brainstorming
1. **No Judgment**: Capture all ideas, evaluate later
2. **Build On Ideas**: "Yes, and..." approach
3. **Think Big**: Don't self-censor during generation
4. **Document Everything**: Even "bad" ideas (they might inspire good ones)

### After Brainstorming
1. **Evaluate Systematically**: Use consistent criteria
2. **Choose One**: Pick top idea to move forward
3. **Document Rationale**: Explain why chosen over alternatives
4. **Define Next Steps**: Clear actions and owners

### Revisiting Sessions
1. **Review Quarterly**: Check parking lot for ideas whose time has come
2. **Update Status**: Mark sessions as implemented or archived
3. **Learn from Outcomes**: Document what worked/didn't work
4. **Reference in New Sessions**: Build on past thinking

## Integration with Other Workflows

### After Brainstorming → Requirements Analysis
```
brainstorm/feature-x/ → @requirements-analyst → backlog/requirements/
```

### After Brainstorming → User Stories
```
brainstorm/feature-x/ → @backlog-manager → backlog/epics/EPIC-XXX.md
```

### After Brainstorming → Risk Assessment
```
brainstorm/feature-x/ → @risk-assessor → risks identified
```

### After Brainstorming → Prioritization
```
brainstorm/feature-x/ → @prioritization-engine → ranked in backlog
```

## Examples

### Example 1: New Feature Brainstorming
```
brainstorm/ai-powered-field-suggestions/
├── SUMMARY.md
│   ├── Problem: Users spend too much time finding signature fields
│   ├── Ideas: 8 AI/ML approaches generated
│   ├── Top Choice: ML-based field detection with manual override
│   └── Next Steps: Validate with @user-research, prototype
├── ideas-raw.md (all 8 ideas)
└── references.md (competitor examples, research papers)
```

### Example 2: Feature Improvement
```
brainstorm/onboarding-improvements/
├── SUMMARY.md
│   ├── Problem: 40% drop-off during onboarding
│   ├── Ideas: 5 UX improvement approaches
│   ├── Top Choice: Progressive disclosure with quick wins
│   └── Next Steps: A/B test with @analytics-insights
└── user-stories-draft.md (3 stories for MVP)
```

### Example 3: Problem Solving
```
brainstorm/performance-optimization/
├── SUMMARY.md
│   ├── Problem: Mobile app slow on older devices
│   ├── Ideas: 6 optimization strategies
│   ├── Top Choice: Lazy loading + image optimization
│   └── Next Steps: Technical spike, impact assessment
└── technical-notes.md (performance benchmarks)
```

## Tips for Effective Brainstorming

### Preparation
- Review `product_documents/` for context
- Check existing `brainstorm/` sessions for related ideas
- Understand user pain points and needs
- Know current technical constraints

### Facilitation
- Start broad, narrow down later
- Use structured techniques (SCAMPER, "How Might We")
- Challenge assumptions
- Explore extreme scenarios
- Consider competitive landscape

### Documentation
- Capture ideas as generated (don't edit during brainstorming)
- Evaluate systematically after generation
- Document evaluation criteria clearly
- Explain why top choice was selected
- Define concrete next steps

### Follow-Through
- Move top ideas to backlog (@backlog-manager)
- Validate with users (@user-research)
- Assess risks (@risk-assessor)
- Update product docs (@documentation-agent)
- Communicate decisions (@stakeholder-communicator)

---

## Getting Started

1. **Try Your First Session**:
   ```
   "Use @feature-brainstormer to brainstorm ways to improve [feature]"
   ```

2. **Review the Output**:
   - Check `brainstorm/[feature-name]/SUMMARY.md`
   - Review ideas and evaluations
   - Consider next steps

3. **Take Action**:
   - Validate top ideas with other agents
   - Move forward with implementation
   - Document learnings

4. **Build the Habit**:
   - Regular brainstorming sessions (weekly/bi-weekly)
   - Review parking lot ideas quarterly
   - Learn from implemented features

---

**Need Help?**
- Use @feature-brainstormer to start a session
- Use Grep to search past brainstorming sessions
- Reference this README for best practices
