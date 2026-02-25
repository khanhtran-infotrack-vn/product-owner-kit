# Product Owner Orchestration System

An AI-powered system for product management workflows built for Claude Code.

## Overview

This system provides **2 core agents** for complex workflows and **11 specialized skills** for domain knowledge, helping Product Owners manage the entire product development lifecycle more efficiently.

### Philosophy: Simple, Powerful, Controllable

- **2 Core Agents**: Handle complex workflows (Q&A and brainstorming)
- **11 Skills**: Call directly for full control over frameworks and methodologies
- **Clear Separation**: Agents orchestrate tools, skills provide knowledge

## Quick Start

### Installation

```bash
# 1. Clone repository
git clone <repo-url>
cd ProductOwnerOrchestration

# 2. Agents are already installed at project level in .claude/agents/
# No action needed — agents are ready to use within this project

# 3. Verify agents are present
ls .claude/agents/
# Should show: feature-brainstormer.md, product-knowledge.md
```

### Basic Usage

**Ask questions about your product**:
```
@product-knowledge - What are our Q2 priorities?
```

**Generate ideas**:
```
@feature-brainstormer - Brainstorm improvements for mobile onboarding
```

**Create user stories** (call skill directly):
```
Use the backlog-manager skill to create user stories for mobile signature feature.
- Reference templates from backlog-manager/references/story-templates.md
- Apply INVEST principles
- Create in backlog/mobile-signature/
```

## Core Components

### 2 Agents

#### 1. product-knowledge
**Purpose**: Answer questions by searching documentation

- Searches all product documentation
- Never guesses - only answers from documented information
- Always cites sources (file:line)
- Says "I don't know" when info not found

**Usage**: `@product-knowledge - [your question]`

#### 2. feature-brainstormer
**Purpose**: Facilitate creative brainstorming sessions

- Generates 50-100+ diverse ideas with anti-bias domain rotation
- Clusters ideas into themes, evaluates with User Value/Business/Feasibility scores
- Runs Challenge & Critique phase (pre-mortem, assumption stress-test, devil's advocate, constraint inversion)
- Reconciles rankings after challenge
- Optional: Creates INVEST-compliant user stories after brainstorming
- Saves output to `brainstorm/[feature-name]/`

**Mode flags**: `--quick` (skip clustering/challenge), `--challenge` (re-challenge existing ideas)

**Usage**: `@feature-brainstormer - Brainstorm [topic]`

---

### 11 Skills (Call Directly)

| Skill | Purpose | When to Use |
|-------|---------|-------------|
| **agile-product-owner** | INVEST principles, user story templates | Creating stories, estimation |
| **analytics-insights** | HEART/AARRR metrics, A/B testing | Analyzing metrics, experiments |
| **backlog-manager** | Story templates, epic breakdown | Creating stories, organizing backlog |
| **documentation-specialist** | PRD/ADR templates, standards | Writing docs, PRDs, ADRs |
| **esign-domain-expert** | eIDAS/ESIGN compliance, audit trails | eSignature features, compliance |
| **po-brainstorm** | Brainstorm entry point — routes to feature-brainstormer | Starting a brainstorming session |
| **po-research** | Research entry point — routes to product-knowledge | Querying product documentation |
| **prioritization-engine** | RICE/MoSCoW/WSJF frameworks | Prioritizing features, ranking |
| **requirements-analyst** | Requirements extraction, gap analysis | Analyzing requirements, finding gaps |
| **sprint-planner** | Sprint planning, capacity calculation | Planning sprints, selecting stories |
| **stakeholder-communicator** | Updates, announcements, presentations | Communicating with stakeholders |

## Features

### What This System Can Do

- **Answer Questions**: Search all documentation with citations
- **Generate Ideas**: 50-100+ creative ideas per brainstorming session
- **Create User Stories**: INVEST-compliant stories with acceptance criteria
- **Plan Sprints**: Calculate capacity, select stories, define goals
- **Prioritize Features**: RICE/MoSCoW/WSJF scoring with rationale
- **Analyze Requirements**: Extract functional/non-functional requirements
- **Write Documentation**: PRDs, ADRs, release notes with templates
- **eSignature Compliance**: eIDAS 2.0 and ESIGN Act guidance
- **Stakeholder Updates**: Executive summaries, sprint reviews

### Time Savings

- **Brainstorming**: 30 minutes saved per session (45% faster)
- **Q&A**: 10-15 minutes saved per question (80-90% faster)
- **End-to-End Feature**: 1.5 hours vs 4-6 hours manual (60-75% faster)

## System Architecture

```
Product Owner Orchestration System
│
├── Agents (Workflow Orchestration)
│   ├── product-knowledge       → Q&A from documentation
│   └── feature-brainstormer    → Creative ideation + story creation
│
├── Skills (Domain Knowledge)
│   ├── agile-product-owner     → User stories, INVEST, estimation
│   ├── analytics-insights      → Metrics frameworks (HEART, AARRR)
│   ├── backlog-manager         → Story templates, epic breakdown
│   ├── documentation-specialist → PRD/ADR templates
│   ├── esign-domain-expert     → eIDAS/ESIGN compliance
│   ├── po-brainstorm           → Brainstorm entry point (routes to feature-brainstormer)
│   ├── po-research             → Research entry point (routes to product-knowledge)
│   ├── prioritization-engine   → RICE/MoSCoW/WSJF
│   ├── requirements-analyst    → Requirements extraction
│   ├── sprint-planner          → Sprint planning, capacity
│   └── stakeholder-communicator → Updates, announcements
│
└── Documentation
    ├── Workflows                → Feature dev, brainstorming, sprint planning
    ├── Architecture             → System design, agent specs
    └── Usage Guides             → How to use skills directly
```

## Usage Examples

### Example 1: Feature Development Workflow

```
Step 1: Brainstorm Ideas
@feature-brainstormer - Brainstorm AI-powered document preparation features

Step 2: Create User Stories
Use backlog-manager skill to create stories from brainstorm/ai-document-prep/SUMMARY.md
- Apply INVEST principles
- Reference templates from backlog-manager/references/
- Create in backlog/ai-document-prep/

Step 3: Prioritize Stories
Use prioritization-engine skill with RICE framework
- Score each story: Reach × Impact × Confidence / Effort
- Rank by RICE score
- Output to backlog/ai-document-prep/PRIORITY_RANKING.md

Step 4: Plan Sprint
Use sprint-planner skill
- Team: 8 engineers, 320 hours capacity
- Velocity: 30 points
- Select top-ranked stories
- Create sprints/sprint-12/sprint-plan.md
```

### Example 2: Requirements Analysis

```
Step 1: Analyze Requirements
Use requirements-analyst skill to analyze stakeholder_feedback/requests.md
- Extract functional and non-functional requirements
- Apply quality checklist from requirements-analyst/references/
- Identify gaps and ambiguities
- Output to requirements/feature-x/

Step 2: Answer Questions
@product-knowledge - What compliance requirements exist for this feature?

Step 3: Create Stories
Use backlog-manager skill to create stories from requirements/feature-x/
```

### Example 3: Sprint Planning

```
Use sprint-planner skill to plan Sprint 12

Context:
- Team: 5 engineers × 80 hours = 400 hours
- Overhead: 20% (80 hours)
- Effective capacity: 320 hours
- Velocity: 30 story points

Tasks:
1. Calculate effective capacity
2. Select stories from backlog/ that fit
3. Identify dependencies
4. Define sprint goal
5. Create sprints/sprint-12/sprint-plan.md

Sprint goal: Deliver Computer Vision Field Detection MVP
```

## Documentation

### Essential Guides

1. **[docs/HOW_TO_USE_SKILLS.md](docs/HOW_TO_USE_SKILLS.md)** - Comprehensive skills usage guide
2. **[CLAUDE.md](CLAUDE.md)** - Repository structure and contribution guide

### Architecture Docs

- **[docs/architecture/system-design.md](docs/architecture/system-design.md)** - System architecture
- **[docs/architecture/product-knowledge-agent.md](docs/architecture/product-knowledge-agent.md)** - Q&A agent design
- **[docs/architecture/feature-brainstormer-update.md](docs/architecture/feature-brainstormer-update.md)** - Brainstormer enhancements

## Project Structure

```
ProductOwnerOrchestration/
├── README.md                          # This file
│
├── .claude/                           # Claude Code format
│   ├── agents/
│   │   ├── feature-brainstormer.md   # Brainstorming agent
│   │   ├── product-knowledge.md      # Q&A agent
│   │   └── references/               # Agent supporting docs
│   │       ├── challenge-techniques.md
│   │       └── user-interaction-patterns.md
│   │
│   └── skills/
│       ├── agile-product-owner/      # User stories, INVEST principles
│       ├── analytics-insights/       # Metrics frameworks
│       ├── backlog-manager/          # Story templates + references
│       ├── documentation-specialist/ # PRD/ADR templates
│       ├── esign-domain-expert/      # eSignature compliance + references
│       ├── po-brainstorm/            # Brainstorm entry point skill
│       ├── po-research/              # Research entry point skill
│       ├── prioritization-engine/    # RICE/MoSCoW frameworks + references
│       ├── requirements-analyst/     # Requirements quality + references
│       ├── sprint-planner/           # Sprint planning methodology
│       └── stakeholder-communicator/ # Communication templates
│
├── docs/
│   ├── HOW_TO_USE_SKILLS.md         # Skills usage guide
│   │
│   ├── architecture/
│   │   ├── system-design.md
│   │   ├── product-knowledge-agent.md
│   │   ├── feature-brainstormer-update.md
│   │   └── skills-recommendation-standalone-agents.md
│   │
│   └── product/
│       ├── overview.md
│       └── features.md
│
├── product_documents/               # Product vision, user research
├── brainstorm/                      # Brainstorming outputs
├── backlog/                         # User stories
└── sprints/                         # Sprint plans
```

## Testing & Validation

### End-to-End Test Results

**Test Scenario**: AI Mobile Document Preparation Feature

1. Created product context documents
2. Brainstormed 65+ ideas with feasibility scores
3. Created 3 INVEST-compliant user stories
4. All artifacts production-ready

**Timeline**: 1.5 hours (vs 4-6 hours manual)

### Validated Capabilities

- Agent-skill integration working
- Document search with 100% citation accuracy
- Never guesses - only answers from docs
- INVEST-compliant user stories
- Feasibility scoring and prioritization
- Optional story creation after brainstorming

## Benefits

### Why Use This System?

**Efficiency**:
- 45% faster brainstorming sessions
- 80-90% faster documentation search
- 60-75% faster end-to-end feature planning

**Quality**:
- INVEST-compliant user stories
- Framework-based prioritization (RICE/MoSCoW/WSJF)
- Compliance-aware (eIDAS 2.0, ESIGN Act)
- Professional documentation standards

**Control**:
- You decide which skills to apply
- You provide context and constraints
- You see the methodology explicitly
- No "magic" - transparent processes

**Simplicity**:
- Only 2 agents to remember
- Skills called directly when needed
- Clear mental model
- Easy to onboard team members

## Requirements

- **Claude Code**: Latest version with subagent and skills support
- **Model**: Works with claude-sonnet-4-5 or compatible models
- **Environment**: macOS/Linux/Windows with bash support
- **Skills**: Requires skills installed in `~/.claude/skills/`

## Configuration

### User-Level Installation (Recommended)

Agents available in all projects:

```bash
mkdir -p ~/.claude/agents
cp .claude/agents/*.md ~/.claude/agents/
```

### Project-Level Installation

Agents already in `.claude/agents/` — ready to use within this project.

**Skills**: Already installed in `~/.claude/skills/` and available system-wide.

## Best Practices

### When to Use Agents

**Use @product-knowledge when**:
- Need to search documentation
- Want cited answers from docs
- Don't know where information is located

**Use @feature-brainstormer when**:
- Need creative ideation
- Want structured brainstorming
- Need optional story generation

### When to Call Skills Directly

**Call skills directly when**:
- Creating artifacts (stories, plans, docs)
- Applying specific frameworks (RICE, INVEST)
- Need full control over process
- Want to see methodology explicitly

### Multi-Step Workflows

Combine skills for complex workflows:

```
Step 1: Use requirements-analyst skill to extract requirements
Step 2: Use backlog-manager skill to create stories
Step 3: Use prioritization-engine skill to rank stories
Step 4: Use sprint-planner skill to plan sprint
Step 5: Use stakeholder-communicator skill to create update
```

## Common Use Cases

### Product Planning
- Q&A about roadmap and priorities
- Brainstorm feature ideas
- Analyze requirements
- Create user stories
- Prioritize backlog

### Sprint Management
- Calculate team capacity
- Select stories for sprint
- Define sprint goals
- Create sprint plans
- Track dependencies

### Stakeholder Communication
- Executive updates (BLUF format)
- Sprint review presentations
- Release announcements
- Feature documentation

### Compliance
- eSignature compliance (eIDAS 2.0, ESIGN Act)
- Audit trail requirements
- Identity verification standards
- Signature type selection (SES/AES/QES)

## Troubleshooting

### Agent not responding

```bash
# Check project-level agents
ls .claude/agents/
# Should see: feature-brainstormer.md, product-knowledge.md
```

### Skill not found

```bash
# Check project-level skills
ls .claude/skills/
# Should show 11+ skill directories
```

### Output quality issues

**Solution**: Be more specific in prompts
- Specify which templates/frameworks to use
- Provide context about team, product, constraints
- Reference specific skill files (e.g., `backlog-manager/references/`)

## Version History

- **v4.1.0** (2026-02-25): Added po-brainstorm + po-research entry-point skills, enhanced feature-brainstormer with challenge phases, anti-bias domain rotation, and sub-agent mode
- **v4.0.0** (2026-02-25): Removed OpenCode support, Claude Code exclusive
- **v3.1.0** (2024-02-09): Added dual-format support (OpenCode + Claude Code)
- **v3.0.0** (2024-02-07): Simplified to 2 agents + 9 skills
- **v2.0.0** (2024-02-06): Added skills integration, separated knowledge from workflow
- **v1.0.0** (2024-01-XX): Initial agent system

## Contributing

This is a personal project template. Feel free to:
- Customize agents for your team's needs
- Create domain-specific skills
- Adjust templates and frameworks
- Add new workflows

## Support

For issues or questions:
- Review documentation in `docs/`
- Read skills usage guide: `docs/HOW_TO_USE_SKILLS.md`
- Check `CLAUDE.md` for repository structure and conventions

## License

Provided as a template for product management workflows. Customize for your team's specific needs.

---

## Quick Reference

### 2 Agents
- `@product-knowledge` - Q&A from documentation
- `@feature-brainstormer` - Creative brainstorming

### 11 Skills (Call Directly)
- `agile-product-owner` - User stories, INVEST
- `analytics-insights` - Metrics analysis
- `backlog-manager` - Story creation
- `documentation-specialist` - PRDs, ADRs
- `esign-domain-expert` - eSignature compliance
- `po-brainstorm` - Brainstorm entry point
- `po-research` - Research entry point
- `prioritization-engine` - RICE/MoSCoW/WSJF
- `requirements-analyst` - Requirements extraction
- `sprint-planner` - Sprint planning
- `stakeholder-communicator` - Updates, announcements

### Key Documentation
- `CLAUDE.md` - Repository structure and guide
- `docs/HOW_TO_USE_SKILLS.md` - Skills guide
