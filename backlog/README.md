# Backlog

This folder contains user stories and epics organized by feature area.

## Structure

```
backlog/
├── [feature-name]/
│   ├── README.md       — epic summary, story index, priority
│   ├── US-001-[name].md
│   ├── US-002-[name].md
│   └── ...
```

## No entries yet

To create your first backlog entries:
- Use `/po-brainstorm [topic]` to ideate and generate draft stories
- Use the `backlog-manager` skill to create INVEST-compliant stories from requirements
- Promote ideas from `brainstorm/[feature]/user-stories/` after team review

## Conventions

- Story files: `US-NNN-short-name.md` (padded 3-digit ID)
- Each story must have: user story, acceptance criteria, story points, dependencies, risks
- Status values: `Draft` → `Ready for Sprint` → `In Progress` → `Done`
