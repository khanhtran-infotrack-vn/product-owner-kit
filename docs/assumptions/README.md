# Assumption Ledger

Running list of assumptions made across brainstorming sessions and requirements work.
Review periodically to validate, invalidate, or retire assumptions.

## Why Track Assumptions?

Unvalidated assumptions are the #1 source of wasted development effort.
This ledger makes them visible so they can be tested, challenged, or confirmed.

## Structure

Each assumption entry:
```markdown
## ASM-NNN: [Short Description]

**Date**: YYYY-MM-DD
**Source**: brainstorm/[feature]/SUMMARY.md | stakeholder meeting | etc.
**Feature area**: [which feature or domain this affects]
**Status**: Unvalidated | Validated | Invalidated | Retired

### The Assumption
[What are we assuming to be true?]

### Evidence
[What supports this assumption? Strong / Weak / None]

### If Wrong...
[What would break or need to change?]

### Blast Radius
High | Medium | Low

### Validation Plan
[How do we test this assumption? User interview, analytics, prototype, etc.]
```

## No assumptions logged yet

Use the `requirements-analyst` skill to extract assumptions from feature discussions.
Or log them manually after each `feature-brainstormer` session (check Assumption Stress-Test section of SUMMARY.md).
