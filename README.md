# Product Owner Orchestration System

An AI-powered toolkit for Product Owners — brainstorm ideas, research decisions, find blind spots, and manage your backlog, all through Claude Code.

---

## Start Here

Two guides cover everything you need:

| Guide | What it covers |
|-------|---------------|
| **[docs/QUICKSTART.md](docs/QUICKSTART.md)** | Your first brainstorm, your first research query, the 5-step PO workflow |
| **[docs/HOW_TO_USE_SKILLS.md](docs/HOW_TO_USE_SKILLS.md)** | Every skill explained: when to use it, how to invoke it, what it produces |

---

## What You Can Do

| I want to... | Use this |
|-------------|---------|
| Brainstorm feature ideas | `/po-brainstorm [topic]` |
| Find what we already decided | `/po-research [question]` |
| Discover what I'm NOT thinking about | `/po-risk-radar` |
| Create user stories | `backlog-manager` skill |
| Rank features by value | `prioritization-engine` skill |
| Plan a sprint | `sprint-planner` skill |
| Analyze user feedback | `analytics-insights` skill |
| Write a stakeholder update | `stakeholder-communicator` skill |
| Document a decision | `documentation-specialist` skill |
| Validate compliance | `esign-domain-expert` skill |

---

## Quick Start: Your First 3 Steps

### 1. Set your product context

Fill in your product vision so every agent has context before answering:

```
Edit: product_documents/product-vision.md
```

### 2. Run your first brainstorm

```
/po-brainstorm [what you want to explore]
```

**Examples:**
- `/po-brainstorm improve onboarding for new users`
- `/po-brainstorm reduce customer churn`
- `/po-brainstorm what could we do with AI in our product`

Results are saved to `brainstorm/[topic]/SUMMARY.md` and `IDEAS.md`.

**Brainstorm modes** — add a flag to change how the session runs:

| Flag | What it does | When to use |
|------|-------------|-------------|
| *(none)* | Full session: ideation → clustering → evaluation → challenge | Default — always a good start |
| `--quick` | Skip clustering and challenge; run ideation → evaluation → documentation | Time-constrained sessions |
| `--idea` | Ideation and clustering only — stop before challenge | When you just want raw ideas |
| `--challenge` | Re-challenge ideas from a previous session | When you want a second pass |
| `--deep` | Full session + 5 enhanced challenge sub-phases on your top 3 ideas | High-stakes decisions |
| `--personas` | Adds 7 stakeholder personas who each generate ideas before SCAMPER | Solo PO needing diverse perspectives |
| `--radar` | Risk radar scan before ideation — identifies uncovered strategic domains to guide brainstorm focus | Strategic or exploratory topics |
| `--deep --personas` | Everything: persona ideation + full challenge + deep challenge | Most thorough option |

### 3. Research what's already documented

```
/po-research [your question]
```

**Examples:**
- `/po-research what features are planned for Q2?`
- `/po-research what did we decide about the mobile workflow?`
- `/po-research what are the requirements for onboarding?`

Only answers from documented facts — never guesses, always cites the source file.

---

## The 3 Agents (Running in the Background)

You invoke these through skills (`/po-brainstorm`, `/po-research`, `/po-risk-radar`) — you rarely need to call them directly.

| Agent | What it does |
|-------|-------------|
| `@feature-brainstormer` | Runs brainstorming sessions: 50-100+ ideas, challenge phase, optional user stories |
| `@product-knowledge` | Searches all your docs and answers questions with cited sources |
| `@po-workflow-assistant` | Strategic planning support: roadmap framing, risk mapping, assumption validation |

---

## The 13 Skills

Call these directly for specific tasks. Full usage guide: [docs/HOW_TO_USE_SKILLS.md](docs/HOW_TO_USE_SKILLS.md).

### Entry Points (Start here for most tasks)

| Skill | What it does |
|-------|-------------|
| `po-brainstorm` | Start a brainstorming session (routes to feature-brainstormer agent) |
| `po-research` | Search your product docs (routes to product-knowledge agent) |
| `po-risk-radar` | Scan all docs and surface what strategic domains are NOT covered |

### Domain Skills (Call directly for specific artifacts)

| Skill | What it produces |
|-------|----------------|
| `agile-product-owner` | INVEST-compliant user stories, sprint ceremonies |
| `analytics-insights` | HEART/AARRR metrics, A/B test analysis |
| `backlog-manager` | User stories, epics, backlog refinement |
| `documentation-specialist` | PRDs, ADRs, release notes, onboarding docs |
| `esign-domain-expert` | eIDAS/ESIGN Act compliance guidance |
| `prioritization-engine` | RICE/MoSCoW/WSJF scoring and ranking |
| `requirements-analyst` | Requirements extraction, gap analysis |
| `sprint-planner` | Sprint capacity, story selection, sprint goals |
| `stakeholder-communicator` | Executive updates, sprint reviews, announcements |
| `writing-clearly-and-concisely` | Writing review for docs, commits, UI copy |

---

## Example Workflows

### Feature from idea to backlog

```
1. /po-brainstorm [feature topic]
   → brainstorm/[topic]/SUMMARY.md

2. Use backlog-manager skill to create stories from the brainstorm
   → backlog/[feature]/US-NNN.md

3. Use prioritization-engine skill with RICE framework to rank stories
   → backlog/[feature]/PRIORITY_RANKING.md

4. Use sprint-planner skill to fit stories into the next sprint
   → sprints/sprint-N/PLAN.md
```

### Quarterly risk audit

```
1. /po-risk-radar
   → Lists all uncovered strategic domains with severity ratings
   → Generates ready-to-use /po-brainstorm commands for each blind spot

2. Run the suggested /po-brainstorm commands for your top gaps

3. /po-research what unvalidated assumptions do we have?
   → Review docs/assumptions/
```

### Stakeholder update

```
1. /po-research what shipped in the last sprint?
2. Use stakeholder-communicator skill to draft an executive update
3. Use writing-clearly-and-concisely skill to review before sending
```

---

## Where Output Lives

```
product_documents/   → Your product vision and user research (you write this)
brainstorm/          → Brainstorming outputs (SUMMARY.md, IDEAS.md, user-stories/)
backlog/             → User stories and epics
sprints/             → Sprint plans
requirements/        → Formal requirement specs
roadmap/             → Quarterly roadmap plans
docs/decisions/      → Architecture Decision Records (ADRs)
docs/assumptions/    → Assumption ledger
```

---

## Documentation

- **[docs/QUICKSTART.md](docs/QUICKSTART.md)** — Step-by-step PO workflow guide
- **[docs/HOW_TO_USE_SKILLS.md](docs/HOW_TO_USE_SKILLS.md)** — Full skills reference
- **[CLAUDE.md](CLAUDE.md)** — Repository structure (for contributors)

---

## Version History

- **v4.2.0** (2026-02-28): Added `--deep` flag (Steelman, Socratic Depth, Assumption Ladder, Regulatory Pre-Mortem, Anti-Pattern Check) and `--personas` flag (7-persona Persona Council); added po-workflow-assistant agent, po-risk-radar and writing-clearly-and-concisely skills
- **v4.1.0** (2026-02-25): Added po-brainstorm + po-research entry-point skills, enhanced feature-brainstormer with challenge phases and anti-bias domain rotation
- **v4.0.0** (2026-02-25): Claude Code exclusive (removed OpenCode support)
- **v3.0.0** (2024-02-07): Simplified to 2 agents + 9 skills
- **v1.0.0** (2024-01-XX): Initial agent system
