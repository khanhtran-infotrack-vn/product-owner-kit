# Product Owner OpenCode Subagents

Streamlined system of 2 core OpenCode subagents for Product Owner workflows. These agents auto-trigger based on user questions or can be invoked explicitly with `@agent-name`.

## Philosophy: Auto-Trigger + Direct Control

- **Auto-trigger**: Agents activate automatically when you ask relevant questions
- **Explicit invoke**: Use `@agent-name` when you want specific agent behavior
- **Skill integration**: Agents leverage Product Owner skills for domain knowledge

---

## Agents (2)

### 1. feature-brainstormer
**Purpose**: Facilitate creative brainstorming sessions with optional user story generation

**Auto-triggers on**:
- "Brainstorm [topic]"
- "Ideate [feature]"
- "Generate ideas for [problem]"
- "What innovative features..."
- "Explore improvements to [area]"

**Capabilities**:
- Structured brainstorming (SCAMPER, "How Might We", User Story Mapping)
- Idea evaluation (User Value, Business Impact, Technical Feasibility)
- Generates 50-100+ diverse ideas
- Creates `brainstorm/[feature-name]/SUMMARY.md` with ranked recommendations
- **Optional**: Creates draft user stories with estimates

**Example**:
```
Brainstorm AI-powered document preparation features for mobile
```

**Output**: Structured brainstorming session in `brainstorm/ai-mobile-prep/` with:
- SUMMARY.md (evaluated ideas, recommendations)
- ideas-raw.md (all ideas generated)
- user-stories/ (optional - if requested)

---

### 2. product-knowledge
**Purpose**: Answer questions about product by searching documentation

**Auto-triggers on**:
- "What features..."
- "What's the status of..."
- "What did [source] say..."
- "Why did we decide..."
- "What are our [roadmap/priorities]..."

**Capabilities**:
- Searches ALL documentation (product docs, brainstorms, backlog, sprints, roadmap)
- Never guesses - only answers from documented information
- Cites sources (file paths and line numbers)
- Says "I don't know" when information not documented
- Provides comprehensive context

**Example**:
```
What AI features are we building for mobile?
```

**Answer format**:
```
Based on brainstorm/ai-mobile-prep/SUMMARY.md and backlog/ai-mobile-prep/:

1. Computer Vision Field Detection (US-001)
   - Status: Backlog - HIGH priority
   - Story Points: 13 points (~6-8 weeks)
   - Description: [details]

Sources:
- backlog/ai-mobile-prep/US-001.md
- brainstorm/ai-mobile-prep/SUMMARY.md
```

---

## When to Use Agents vs Skills

### Use Agents When:
- **feature-brainstormer**: Need creative ideation workflow (generates many ideas, evaluates, documents)
- **product-knowledge**: Need to search documentation and answer questions

### Call Skills Directly When:
You want direct application of frameworks without agent workflow:
- Creating user stories → `agile-product-owner` skill
- Planning sprints → `sprint-planner` skill
- Prioritizing features → `prioritization-engine` skill
- Analyzing requirements → `requirements-analyst` skill
- Writing docs → `documentation-specialist` skill
- eSign domain questions → `esign-domain-expert` skill
- Analyzing metrics → `analytics-insights` skill
- Stakeholder comms → `stakeholder-communicator` skill

---

## Usage Examples

### Example 1: Brainstorm → Knowledge Check → Stories
```
Step 1: Brainstorm (auto-triggers)
"Brainstorm AI-powered document preparation features"
→ Creates brainstorm/ai-mobile-prep/SUMMARY.md

Step 2: Check documentation (auto-triggers)
"What features are currently in the mobile backlog?"
→ Searches and cites documented mobile features

Step 3: Create stories (call skill directly)
"Use the backlog-manager skill to create user stories from
brainstorm/ai-mobile-prep/SUMMARY.md with INVEST principles"
→ Creates stories in backlog/ai-mobile-prep/
```

---

### Example 2: Question → Answer with Sources
```
"What's the status of Computer Vision Field Detection?"

→ product-knowledge agent auto-triggers, searches:
  - backlog/**/*
  - sprints/**/*
  - brainstorm/**/*

→ Returns:
  Based on backlog/ai-mobile-prep/US-001.md:
  - Status: Backlog (not in sprint)
  - Story Points: 13 points
  - Estimated: 6-8 weeks
  - Priority: HIGH

  Sources: backlog/ai-mobile-prep/US-001.md
```

---

## Agent Features

### Auto-Trigger Detection
Agents automatically activate when you ask questions matching their description patterns. No need to explicitly invoke with `@agent-name` unless you want to force a specific agent.

### Skill Integration
Both agents leverage Product Owner skills:
- `feature-brainstormer` uses `agile-product-owner` skill for user story creation
- `product-knowledge` uses `agile-product-owner` skill to interpret agile documentation

### Structured Outputs
Agents create organized documentation:
- `brainstorm/[feature-name]/` - Brainstorming sessions
- Clear citations with file paths
- Comprehensive context and related information

---

## Installation

Agents are already installed in this project at:
```
.opencode/agents/
├── feature-brainstormer.md
├── product-knowledge.md
└── README.md
```

OpenCode automatically loads agents from `.opencode/agents/` directory.

---

## Migration from Previous System

This is v3.0.0 (simplified from 14 agents to 2 agents + 8 skills).

**What changed**:
- Removed 12 task-specific agents → Call skills directly instead
- Kept 2 core workflow agents (brainstorming, knowledge search)
- Skills provide domain knowledge without agent overhead

**Before**:
```
@backlog-manager - Create user stories for mobile signature
```

**After**:
```
Create user stories for mobile signature feature.

Use the backlog-manager skill to:
- Apply INVEST principles
- Reference templates from backlog-manager/references/
- Create in backlog/mobile-signature/
```

**Why**: More control, less confusion, clearer workflow.

---

## Available Skills (Call Directly)

1. **agile-product-owner** - INVEST principles, user story templates, estimation
2. **analytics-insights** - Metrics frameworks, analysis methods
3. **backlog-manager** - Story templates, epic decomposition
4. **documentation-specialist** - PRD templates, ADRs, release notes
5. **esign-domain-expert** - eIDAS/ESIGN compliance, signature types
6. **prioritization-engine** - RICE/WSJF/MoSCoW frameworks
7. **requirements-analyst** - Requirements quality framework
8. **sprint-planner** - Sprint planning methodology, capacity calculation
9. **stakeholder-communicator** - Communication templates by audience

See `/Users/trankhanh/Desktop/MyProjects/ProductOwnerOrchestration/.claude/skills/` for skill details.

---

## Version

**Version**: 3.0.0 (OpenCode Subagent Format)
**Format**: OpenCode subagent with auto-trigger descriptions
**Last Updated**: 2024-02-09
**Compatible With**: Claude Code with OpenCode subagent support

---

## Support

For issues or customization:
- Check agent files in `.opencode/agents/`
- Review skill definitions in `.claude/skills/`
- Modify agent descriptions to adjust auto-trigger patterns
- See Claude Code documentation: https://code.claude.com/docs
