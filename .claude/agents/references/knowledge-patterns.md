# Product Knowledge Patterns

Reference file for `product-knowledge` agent. Load with Read when you need question-type templates or example patterns.

---

## Question Type Templates

Use these patterns to structure searches and answers by question type.

### Type 1: Feature Questions
**Examples**: "What AI features are we building?", "Do we have mobile signature support?"

**Search**:
1. Glob `"**/*[keyword]*"`, `"brainstorm/**/*"`, `"backlog/**/*"`
2. Grep feature terms in brainstorm/ and backlog/
3. Read SUMMARY.md files + user stories

**Answer format**:
```
Based on [document]:
- Feature: [Name] ([Story ID])
- Status: In brainstorming / Backlog / In development / Shipped
- Priority: HIGH/MEDIUM/LOW
- Story Points: [X]
- Details: [Description, acceptance criteria, dependencies]

Source: [file paths]
```

---

### Type 2: Roadmap Questions
**Examples**: "What are we building in Q2?", "When will feature X be delivered?"

**Search**:
1. Glob `"roadmap/**/*"`, `"**/*roadmap*"`, `"sprints/**/*"`
2. Read roadmap docs + sprint plans + backlog priorities

**Answer format**:
```
Based on [roadmap document]:
Q2 Roadmap:
- Phase 1 (Weeks 1-4): [Features]
- Phase 2 (Weeks 5-8): [Features]

Timeline for [feature]:
- Start: [Date] | End: [Date] | Dependencies: [List]

Source: [file paths]
```

---

### Type 3: User Research Questions
**Examples**: "What do users say about mobile?", "Who are our target users?"

**Search**:
1. Read `product_documents/user-research*.md` and `product_documents/product-vision.md`
2. Grep for user quotes in brainstorm/

**Answer format**:
```
Based on [user research document]:
User Pain Points:
1. [Pain point] — [X]% of users
   Quote: "[direct quote]"
   Source: [document]

Target Users:
- [Persona 1]: [Description]

Source: [file paths]
```

---

### Type 4: Decision Questions
**Examples**: "Why did we choose X over Y?", "Why is this a priority?"

**Search**:
1. Read brainstorm/ SUMMARY.md files (rationale section)
2. Check docs/decisions/ for ADRs
3. Check "Business Context" in user stories

**Answer format**:
```
Based on [document]:
Decision: [What was decided]
Rationale: [Reason 1], [Reason 2]
Alternatives Considered:
- [Option A]: Rejected because [reason]
Impact: User Value [score], Business Impact [score]

Source: [file paths]
```

---

### Type 5: Technical Questions
**Examples**: "What are dependencies for feature X?", "What's the estimated effort?"

**Search**:
1. Read user stories in backlog/ (Dependencies section)
2. Read brainstorm/ SUMMARY.md (Technical Feasibility score)
3. Check requirements/ for technical specs

**Answer format**:
```
Based on [document]:
Estimated Effort: [X] story points (~[Y] weeks)
Breakdown: [discipline breakdown if available]
Dependencies: [List]
Technical Risks: [Risk] → [Mitigation]

Source: [file paths]
```

---

### Type 6: Status Questions
**Examples**: "What's the status of feature X?", "What stories are in the current sprint?"

**Search**:
1. Check sprints/ for current sprint board
2. Check backlog/ for story status
3. Check brainstorm/ if still in ideation

**Answer format**:
```
Based on [sprint plan / backlog]:
Feature: [Name]
Status: In brainstorming / Backlog / Current sprint / Completed

If in sprint: Sprint [N], Progress [X]%, Blockers: [list]
If in backlog: Priority [level], Points [X], Next action: [when]

Source: [file paths]
```

---

## Common Glob/Grep Patterns

```
# Features
Glob: "**/*[feature-name]*", "brainstorm/**/*", "backlog/**/*"
Grep: "# .*[keyword]"  (headings)

# Roadmap
Glob: "roadmap/**/*", "sprints/**/*", "**/*plan*"

# User research
Glob: "product_documents/*research*", "product_documents/*user*", "**/*persona*"

# Decisions
Glob: "docs/decisions/**/*"
Grep: "Decision|Rationale|Recommended Approach"

# User stories
Grep: "US-[0-9]+" (IDs)
Grep: "As a.*I want" (story format)

# Timelines
Grep: "Story Points.*[0-9]+", "Timeline|Sprint|Phase|Q[1-4]"

# User quotes
Grep: '>".*', "User.*said|reported|mentioned"
```

---

## Answer Quality — Good vs Bad

**Good answer** (always aim for this):
```
Based on brainstorm/ai-mobile-prep/SUMMARY.md and backlog/ai-mobile-prep/README.md:

We are building 3 AI features for mobile:
1. Computer Vision Field Detection (US-001) — HIGH priority, 13 points (~6-8 weeks)
   Description: ML model auto-detects signature/date/initial fields ≥85% accuracy
   Rationale: 92% of users want auto-detection (top pain point)

Sources: brainstorm/ai-mobile-prep/SUMMARY.md, backlog/ai-mobile-prep/US-001.md
```
✅ Specific, cites sources, includes story IDs, estimates, and rationale.

**Bad answer** (never do this):
```
We're building AI features for mobile like field detection. It should be ready soon.
```
❌ Vague, no sources, no IDs, no estimates, guesses timeline.

**"I don't know" answer** (when information is not found):
```
I don't know — I couldn't find information about [topic] in the documentation.

I searched: product_documents/, brainstorm/, backlog/, sprints/, roadmap/

What I did find: [related info if any]

You may need to ask the product team directly, or document this first.
```

---

## Complex Question Handling

**Multi-part questions**: Break into sub-questions, answer each with source citations, then synthesize.

**Conflicting information**: Report both sources with dates, defer to the more recent document, flag the conflict for user verification.

**Proactive context**: When answering effort questions, include related stories, dependencies, and broader phase context — not just the direct answer.

---

## Example Interactions (Abbreviated)

**Feature question**: User asks "What AI features are we building for mobile?"
→ Glob `"**/*ai*"`, `"**/*mobile*"` → Grep `"AI.*mobile"` → Read SUMMARY.md and backlog/
→ Return 3 features with story IDs, priorities, points, and source file paths

**Timeline question**: User asks "When will Computer Vision Field Detection be ready?"
→ Glob `"**/*computer*vision*"` → Read US-001.md → Check sprints/ for scheduling
→ Return estimate (13 points, 6-8 weeks), current status (Backlog, not scheduled), broader phase context

**"I don't know"**: User asks about Windows Phone support
→ Search all directories, find iOS/Android references but no Windows Phone
→ Return honest answer with search explanation and what WAS found
