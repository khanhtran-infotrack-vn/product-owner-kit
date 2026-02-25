# Requirements

Formal requirement specifications, extracted from stakeholder conversations and user feedback.

## Structure

```
requirements/
├── [feature-name]/
│   ├── REQ-001-[name].md   — individual requirement spec
│   └── README.md           — requirement index for this feature
```

## No requirements yet

To create requirements:
- Use the `requirements-analyst` skill: "analyze these requirements: [paste stakeholder input]"
- Or: "extract requirements from this meeting notes: [paste notes]"
- Link requirements back to user stories in `backlog/`

## Conventions

- Requirement IDs: `REQ-NNN` (padded 3-digit, scoped per feature)
- Each requirement: description, rationale, acceptance criteria, priority (MoSCoW)
- Status: `Draft` → `Review` → `Approved`
