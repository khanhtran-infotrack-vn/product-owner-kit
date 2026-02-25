# Architecture Decision Records (ADRs)

Documents significant product and architectural decisions with context and rationale.

## Structure

```
docs/decisions/
├── ADR-001-[short-title].md
├── ADR-002-[short-title].md
└── ...
```

## No ADRs yet

To create a decision record:
- Use the `documentation-specialist` skill: "create decision record for [decision topic]"
- Or: after any `feature-brainstormer` session, create an ADR for the recommended approach

## ADR Template

```markdown
# ADR-NNN: [Short Title]

**Date**: YYYY-MM-DD
**Status**: Proposed | Accepted | Deprecated | Superseded by ADR-XXX

## Context
[What situation or problem required a decision?]

## Decision
[What was decided?]

## Rationale
[Why this option over alternatives?]

## Alternatives Considered
- Option A: rejected because [reason]
- Option B: rejected because [reason]

## Consequences
- Positive: [benefits]
- Negative: [trade-offs]

## Source
[brainstorm/[feature]/SUMMARY.md or stakeholder meeting]
```
