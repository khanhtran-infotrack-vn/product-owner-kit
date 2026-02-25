# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

A **prompt-engineering / markdown repository** — there is no source code to build, compile, or test. The "code" is Claude Code agent and skill definitions (markdown files with YAML frontmatter) plus product management artifacts. There are no build, lint, or test commands.

The one executable utility is:
```bash
python3 .claude/skills/agile-product-owner/scripts/user_story_generator.py          # generate stories
python3 .claude/skills/agile-product-owner/scripts/user_story_generator.py sprint 30 # plan sprint
python3 .claude/skills/agile-product-owner/scripts/user_story_generator.py --save    # save to docs/user-stories/
```

## Architecture

```
3 Agents (workflow orchestration)   13 Skills (domain knowledge, called directly)
├── product-knowledge               ├── agile-product-owner   (INVEST, user stories)
│   tools: Read, Glob, Grep         ├── analytics-insights    (HEART, AARRR, A/B)
├── feature-brainstormer            ├── backlog-manager       (story templates, epics)
│   tools: Read,Write,Edit,         ├── documentation-specialist (PRD, ADR, release notes)
│          Bash,Grep,Glob           ├── esign-domain-expert   (eIDAS, ESIGN, audit trails)
└── po-workflow-assistant           ├── po-brainstorm         (brainstorm entry point)
    tools: Read,Glob,Grep,Write     ├── po-research           (research entry point)
                                    ├── po-risk-radar         (blind spot detector)
Agent references/                   ├── prioritization-engine (RICE, MoSCoW, WSJF)
├── challenge-techniques.md         ├── requirements-analyst  (extraction, gap analysis)
├── user-interaction-patterns.md    ├── sprint-planner        (capacity, story selection)
├── brainstorm-templates.md         ├── stakeholder-communicator (updates, presentations)
└── knowledge-patterns.md          └── writing-clearly-and-concisely (docs, commits, UI text)
```

**Agents** use Claude Code's subagent system (invoked with `@agent-name`). They have tool access declared in their `tools:` frontmatter field and orchestrate multi-step workflows.

**Skill integration note**: When agents say they "use" a skill (e.g., `agile-product-owner`), this means the skill's knowledge is baked into the agent's system prompt as static context — not dynamically loaded at runtime. Skills are context files, not callable modules.

**Skills** are loaded as context by Claude Code when referenced in prompts. They provide frameworks and templates but have no tool access themselves.

## File Formats

### Agent format (`.claude/agents/*.md`)
```markdown
---
name: agent-name
description: One-line description used for auto-trigger matching — this is critical
model: sonnet
---

System prompt in markdown...
```

The `description` field is parsed by Claude Code to decide when to auto-invoke the agent. Keep it precise with trigger keywords.

The `tools:` field (optional) restricts which tools the agent can access. If omitted, the agent inherits all available tools. The architecture diagram above documents which tools each agent uses; this is informational, not enforced via frontmatter.

### Skill format (`.claude/skills/<name>/SKILL.md`)
```markdown
---
name: skill-name
description: When to invoke this skill (used by skill registry)
---

# Skill Name

Domain knowledge, frameworks, templates...
```

Skills with reference files keep supporting material in `references/` subdirectories. Skills with scripts keep utility code in `scripts/`.

## Content Directories (Product Management Artifacts)

These directories hold **live product content** written by agents or users:

| Directory | Purpose |
|-----------|---------|
| `product_documents/` | Product vision, user research, strategy — read by `@feature-brainstormer` for context |
| `brainstorm/[feature]/` | Brainstorming outputs: `SUMMARY.md`, `IDEAS.md`, optional `user-stories/` |
| `backlog/[feature]/` | User stories (`US-001.md`, etc.) and `README.md` index |
| `sprints/sprint-N/` | Sprint plans, boards, standup templates |
| `requirements/[feature]/` | Structured requirements documents |
| `roadmap/` | Quarterly roadmap plans |
| `docs/decisions/` | Architecture Decision Records (ADRs) |
| `docs/assumptions/` | Assumption ledger — tracked across brainstorming sessions |
| `docs/` | Workflow guides, quickstart, architecture docs |

See `docs/QUICKSTART.md` for the complete PO workflow guide.

## Key Skill Reference Files

Some skills have reference files with specific content — always use the correct filenames:

| Skill | Reference file(s) |
|-------|------------------|
| `backlog-manager` | `references/story-templates.md`, `references/epic-breakdown-example.md` |
| `esign-domain-expert` | `references/domain-knowledge.md` |
| `prioritization-engine` | `references/frameworks.md` |
| `requirements-analyst` | `references/examples.md` |

## Document Skills

`.claude/skills/document-skills/` contains four additional skills for document manipulation (docx, pdf, pptx, xlsx). These are separate from the 13 product management skills and have their own scripts and OOXML reference schemas.

## Adding New Skills

1. Create directory: `.claude/skills/my-skill/`
2. Create `SKILL.md` with YAML frontmatter (`name`, `description`) and markdown knowledge body
3. Optionally add `references/` for supporting materials or `scripts/` for utilities
4. Reference the skill by name in prompts; no registration step required

## Adding New Agents

1. Create `.claude/agents/my-agent.md` with frontmatter (`name`, `description`, `tools`, `model`) and system prompt
2. The `description` field controls auto-trigger matching — make it specific
3. Agent reference files (supporting docs the agent reads) go in `.claude/agents/references/`

> Note: Never create agents at `~/.claude/agents/` during project work — all files stay in `.claude/`.

