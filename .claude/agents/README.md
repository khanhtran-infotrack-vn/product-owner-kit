# Product Owner Agent System (Simplified)

A streamlined system of Claude Code agents and skills designed to augment Product Owner capabilities. This simplified architecture uses **2 core agents** for workflow orchestration and **8 skills** for domain knowledge that you call directly.

## Philosophy: Less is More

This system was simplified from 14 agents to 2 agents to reduce confusion and increase control. Instead of remembering which agent to invoke, you now:

1. Use **2 core agents** for complex workflows (brainstorming and Q&A)
2. **Call skills directly** in your prompts for everything else
3. Get **more control** over which knowledge to apply and when

## Core Agents (2)

### 1. product-knowledge
**Purpose**: Answer questions about your product by searching documentation

**Auto-triggers on**:
- "What features..." / "What's the status..." / "What did we decide..."
- "Why did we..." / "What are the requirements..." / "What's in the roadmap..."

**Usage**:
- Auto-triggers on questions (see patterns above)
- Explicit: `@product-knowledge - [your question]`

**Capabilities**:
- Searches ALL documentation (product_documents/, brainstorm/, backlog/, sprints/, requirements/, roadmap/)
- Uses Glob to find files, Grep to search content, Read to extract details
- Never guesses - only answers based on documented information
- Cites sources for every answer (specific file paths)
- Says "I don't know" when information not documented (with search explanation)
- Uses `agile-product-owner` skill for understanding agile terminology

**Example Questions**:
```
"What AI features are we building for mobile?"
→ Searches brainstorm/, backlog/, returns detailed answer with story IDs, estimates, sources

"What's the status of Computer Vision Field Detection?"
→ Searches backlog/, sprints/, returns status, timeline, dependencies, blockers

"Why did we prioritize feature X over Y?"
→ Searches brainstorming rationale, returns decision reasoning with alternatives considered
```

**Model**: Sonnet (inherits from main conversation)
**Tools**: Read, Bash, Grep, Glob
**Skills Used**: `agile-product-owner`

---

### 2. feature-brainstormer
**Purpose**: Facilitate creative brainstorming sessions with optional user story generation

**Auto-triggers on**:
- "Brainstorm..." / "Ideate..." / "Generate ideas..."
- "What innovative features..." / "Explore improvements..."

**Usage**:
- Auto-triggers on brainstorming requests (see patterns above)
- Explicit: `@feature-brainstormer - Brainstorm [topic]`

**Capabilities**:
- Facilitates creative brainstorming using SCAMPER, "How Might We", User Story Mapping
- Reads product documents for context (vision, strategy, user research)
- Generates 50-100+ ideas across multiple categories
- Evaluates ideas with scores: User Value (1-5), Business Impact (1-5), Technical Feasibility (1-5)
- Recommends top features based on evaluation
- **Optional**: Creates draft user stories with story point estimates
- Outputs to `brainstorm/[feature-name]/SUMMARY.md` and `ideas-raw.md`

**Workflow**:
1. Reads context from `product_documents/` and existing `brainstorm/` sessions
2. Generates diverse ideas using structured techniques
3. Evaluates each idea across 3 dimensions (15-point scale)
4. Creates `SUMMARY.md` with comparative analysis and top recommendations
5. **Asks**: "Would you like me to create draft user stories with estimates for top 5 ideas?"
6. **If YES**: Creates INVEST-compliant stories in `brainstorm/[feature-name]/user-stories/`

**Example Invocations**:
```
"Brainstorm AI-powered document preparation features for mobile"
→ Generates 50+ ideas, evaluates, creates SUMMARY.md, asks about user stories

"Help me ideate ways to improve mobile signature experience"
→ Uses SCAMPER technique, generates 7-10 improvements, ranks by value/feasibility

"Generate ideas for reducing customer onboarding time"
→ Applies "5 Whys" and "How Might We", creates solution categories, prioritizes
```

**Model**: Sonnet (inherits from main conversation)
**Tools**: Read, Write, Edit, Bash, Grep, Glob
**Skills Used**: `agile-product-owner` (for user story creation)

---

## Skills (9) - Call Directly

Instead of invoking agents for every task, call skills directly in your prompts. This gives you more control and clarity.

### 1. agile-product-owner
**What it provides**:
- INVEST principles for user stories
- User story templates and formats
- Story point estimation guidance
- Definition of Done standards
- Acceptance criteria patterns

**When to use**: Creating user stories, estimating work, defining acceptance criteria

**How to use**:
```
I need to create user stories for [feature].

Use the agile-product-owner skill to:
- Apply INVEST principles
- Use standard user story format (As a... I want... So that...)
- Define clear acceptance criteria
- Estimate story points

[Provide feature context]
```

---

### 2. analytics-insights
**What it provides**:
- Product metrics frameworks (HEART, AARRR, North Star)
- Feature adoption analysis methods
- A/B testing guidance
- Data interpretation patterns

**When to use**: Analyzing metrics, measuring feature success, recommending experiments

**How to use**:
```
Analyze the metrics in metrics/q1-2025.json

Use the analytics-insights skill to:
- Apply HEART framework
- Identify trends and anomalies
- Calculate adoption rates
- Recommend experiments

Focus on mobile engagement metrics.
```

---

### 3. backlog-manager
**What it provides**:
- Backlog organization patterns
- Epic breakdown techniques
- Story templates (references/story-templates.md)
- Example epic decomposition (references/epic-breakdown-example.md)

**When to use**: Creating user stories, breaking down epics, organizing backlog

**How to use**:
```
Create user stories for mobile AI features based on:
- brainstorm/ai-mobile-document-prep/SUMMARY.md

Use the backlog-manager skill to:
1. Reference templates from backlog-manager/references/story-templates.md
2. Apply epic breakdown patterns
3. Create stories in backlog/ai-mobile-prep/

For each story include:
- User story format
- Acceptance criteria
- Story points
- Dependencies
```

---

### 4. documentation-specialist
**What it provides**:
- Documentation standards and structure
- Product Requirements Document (PRD) templates
- Architecture Decision Records (ADR) format
- Release notes and changelog patterns
- API documentation guidelines

**When to use**: Writing product docs, creating PRDs, documenting decisions

**How to use**:
```
Create a PRD for the mobile signature feature.

Use the documentation-specialist skill to:
- Apply PRD template structure
- Include all required sections
- Follow documentation standards
- Create in docs/prds/mobile-signature.md

Feature context: [describe feature]
```

---

### 5. esign-domain-expert
**What it provides**:
- eIDAS 2.0 and ESIGN Act compliance knowledge
- Signature types (SES, AES, QES) guidance
- Audit trail requirements
- Identity verification standards
- Electronic signature workflows
- Reference: domain knowledge (references/domain-knowledge.md)

**When to use**: eSignature features, compliance questions, audit trail design

**How to use**:
```
Design the audit trail for our signature workflow.

Use the esign-domain-expert skill to:
- Reference compliance requirements from esign-domain-expert/references/
- Apply eIDAS 2.0 standards
- Ensure proper identity verification
- Define required audit trail fields

Jurisdiction: EU (eIDAS) and US (ESIGN Act)
```

---

### 6. prioritization-engine
**What it provides**:
- RICE framework (Reach, Impact, Confidence, Effort)
- MoSCoW method (Must/Should/Could/Won't)
- WSJF (Weighted Shortest Job First)
- Value vs Effort matrices
- Reference: framework details (references/frameworks.md)

**When to use**: Prioritizing features, deciding what to build next, ranking backlog

**How to use**:
```
Prioritize features in backlog/ai-mobile-prep/

Use the prioritization-engine skill to:
- Apply RICE framework
- Reference frameworks from prioritization-engine/references/frameworks.md
- Score each feature for Reach, Impact, Confidence, Effort
- Provide ranking with rationale

Features:
1. Computer Vision Field Detection (US-001)
2. Confidence Scores (US-002)
3. Document Understanding (US-003)
```

---

### 7. requirements-analyst
**What it provides**:
- Requirements quality framework
- Functional vs non-functional requirements
- Gap analysis methodology
- Acceptance criteria patterns
- Reference: requirement examples and patterns (references/examples.md)

**When to use**: Analyzing requirements, identifying gaps, structuring requirements

**How to use**:
```
Analyze requirements from stakeholder_feedback/mobile-signature-requests.md

Use the requirements-analyst skill to:
- Extract functional and non-functional requirements
- Apply quality checklist from requirements-analyst/references/
- Identify gaps and ambiguities
- Structure requirements by category

Output to: requirements/mobile-signature/
```

---

### 8. sprint-planner
**What it provides**:
- Sprint planning methodology
- Team capacity calculation formulas
- Sprint goal definition patterns
- Velocity tracking guidance
- Dependency identification

**When to use**: Planning sprints, calculating capacity, selecting stories

**How to use**:
```
Plan Sprint 12 using the sprint-planner skill.

Team capacity:
- 2 ML engineers × 80 hours = 160 hours
- 3 mobile engineers × 80 hours = 240 hours
- Total: 400 hours (minus 20% overhead = 320 hours)

Velocity: 30 story points

Use sprint-planner skill to:
1. Calculate effective capacity
2. Select stories from backlog/ai-mobile-prep/
3. Identify dependencies
4. Create sprints/sprint-12/sprint-plan.md

Sprint goal: Deliver Computer Vision Field Detection MVP
```

---

### 9. stakeholder-communicator
**What it provides**:
- Communication templates by audience
- Executive update formats
- Release announcement patterns
- Sprint review presentation structure
- Stakeholder alignment frameworks

**When to use**: Creating updates, announcements, presentations for stakeholders

**How to use**:
```
Create an executive update for Q1 progress.

Use the stakeholder-communicator skill to:
- Apply executive update template
- Focus on business outcomes, not technical details
- Include metrics and progress visualization
- Add next steps and asks

Audience: C-level executives
Content: Summarize sprints 9-12, highlight AI features launch
```

---

## When to Use Agents vs Skills

### Use Agents When:
- **product-knowledge**: Need to search documentation and answer questions
  - Agent orchestrates search across multiple files
  - Provides cited answers from documented information
  
- **feature-brainstormer**: Need creative ideation and optional story generation
  - Agent orchestrates brainstorming workflow
  - Optionally creates structured output (ideas + stories)

### Use Skills When:
- Creating user stories → **backlog-manager skill**
- Planning sprints → **sprint-planner skill**
- Analyzing requirements → **requirements-analyst skill**
- Prioritizing features → **prioritization-engine skill**
- Writing documentation → **documentation-specialist skill**
- Domain expertise (eSign) → **esign-domain-expert skill**
- Analyzing metrics → **analytics-insights skill**
- Stakeholder communications → **stakeholder-communicator skill**

Skills give you direct access to frameworks, templates, and best practices without agent overhead.

---

## Installation

### Prerequisites

Install both agents AND skills for full functionality:

```bash
# 1. Install skills (domain knowledge)
cd .claude/skills/
# Skills are already installed in this system

# 2. Install agents (workflow orchestration)
mkdir -p ~/.claude/agents
cp /Users/trankhanh/Desktop/MyProjects/ProductOwnerOrchestration/.claude/agents/*.md ~/.claude/agents/
```

### Option 1: User-Level (Available in all projects)

```bash
# Copy 2 agents to user-level directory
cp .claude/agents/feature-brainstormer.md ~/.claude/agents/
cp .claude/agents/product-knowledge.md ~/.claude/agents/
```

### Option 2: Project-Level (Specific to one project)

```bash
# In your project directory
mkdir -p .claude/agents
cp .claude/agents/feature-brainstormer.md .claude/agents/
cp .claude/agents/product-knowledge.md .claude/agents/
```

---

## Usage Examples

### Example 1: Brainstorm → Stories → Sprint Plan

```
Step 1: Brainstorm
@feature-brainstormer - Brainstorm AI-powered document preparation features

Step 2: Create Stories
Create user stories from brainstorm/ai-mobile-document-prep/SUMMARY.md

Use the backlog-manager skill to:
- Apply INVEST principles
- Reference templates from backlog-manager/references/story-templates.md
- Create in backlog/ai-mobile-prep/

Step 3: Plan Sprint
Plan Sprint 12 with these stories.

Use sprint-planner skill to:
- Calculate capacity (8 engineers, 2 weeks)
- Select top priority stories
- Create sprints/sprint-12/sprint-plan.md
```

---

### Example 2: Answer Questions from Docs

```
@product-knowledge - What are our Q2 priorities according to the product roadmap?

@product-knowledge - What compliance requirements do we have for eSignature features?

@product-knowledge - Which user stories in the backlog depend on the ML model deployment?
```

---

### Example 3: Requirements → Stories → Prioritization

```
Step 1: Analyze Requirements
Analyze requirements from stakeholder_feedback/mobile-requests.md

Use requirements-analyst skill to:
- Extract functional/non-functional requirements
- Reference quality checklist from requirements-analyst/references/
- Identify gaps
- Output to requirements/mobile-signature/

Step 2: Create Stories
Use backlog-manager skill to create stories from requirements/mobile-signature/

Step 3: Prioritize
Prioritize stories using prioritization-engine skill:
- Apply RICE framework
- Score: Reach, Impact, Confidence, Effort
- Provide ranked list with rationale
```

---

## Skills Architecture

### Viewing Skill Content

Skills contain domain knowledge that you reference in prompts:

```bash
# View a skill's main content
cat ~/.claude/skills/backlog-manager/SKILL.md

# View skill reference materials
cat ~/.claude/skills/backlog-manager/references/story-templates.md
cat ~/.claude/skills/backlog-manager/references/epic-breakdown-example.md
```

### Skill Structure

Each skill contains:

```
skill-name/
├── SKILL.md                  # Main skill content (frameworks, methods)
├── references/               # Supporting reference files
│   ├── examples.md
│   ├── templates.md
│   └── frameworks.md
└── scripts/                  # Optional utility scripts
```

### Available Skills

1. **agile-product-owner** - INVEST principles, story templates, estimation
2. **analytics-insights** - Metrics frameworks, analysis methods
3. **backlog-manager** - Story templates, epic decomposition (+ 2 reference files)
4. **documentation-specialist** - Documentation standards, PRD/ADR templates
5. **esign-domain-expert** - eIDAS/ESIGN compliance, signature types (+ 1 reference file)
6. **prioritization-engine** - RICE/WSJF/MoSCoW frameworks (+ 1 reference file)
7. **requirements-analyst** - Requirements quality framework (+ 1 reference file)
8. **sprint-planner** - Sprint planning methodology, capacity calculation
9. **stakeholder-communicator** - Communication templates by audience

---

## Workflows

See `.claude/workflows/` for detailed workflow guides:

- **feature-development-workflow.md** - End-to-end feature development (6 stages)
- **brainstorming-workflow.md** - Detailed brainstorming guide (5 steps)
- **sprint-planning-workflow.md** - Complete sprint planning process

---

## Benefits of Simplified System

### Before (14 agents)
- ❌ Confusion: Which agent should I use?
- ❌ Overhead: Agents for simple tasks
- ❌ Indirection: Agent decides what to do
- ❌ Complexity: Too many options

### After (2 agents + 9 skills)
- ✅ Clarity: Only 2 agents to remember
- ✅ Control: You decide which skill to apply
- ✅ Efficiency: Skills called directly in prompts
- ✅ Simplicity: Fewer moving parts

---

## Migration Guide

If you were using the previous 14-agent system:

### Removed Agents (Call skills directly instead)

| Old Agent | Use This Skill Instead |
|-----------|------------------------|
| `@analytics-insights` | **analytics-insights skill** |
| `@backlog-manager` | **backlog-manager skill** |
| `@competitive-intel` | Research manually or use web search |
| `@documentation-agent` | **documentation-specialist skill** |
| `@esign-domain-expert` | **esign-domain-expert skill** |
| `@prioritization-engine` | **prioritization-engine skill** |
| `@requirements-analyst` | **requirements-analyst skill** |
| `@risk-assessor` | Analyze risks manually with context |
| `@roadmap-planner` | Plan roadmap manually with skills |
| `@sprint-planner` | **sprint-planner skill** |
| `@stakeholder-comms` | **stakeholder-communicator skill** |
| `@user-research` | Analyze research manually |

### What Changed

**Before**:
```
@backlog-manager - Create user stories for mobile signature feature
```

**After**:
```
Create user stories for mobile signature feature.

Use the backlog-manager skill to:
- Apply INVEST principles
- Reference templates from backlog-manager/references/story-templates.md
- Create stories in backlog/mobile-signature/

[Provide feature context]
```

**Why?** You get more control over what knowledge to apply and how.

---

## Customization

### Modify Agent Behavior

Edit the agent's markdown file to customize:

1. **System Prompt**: Change the markdown body
2. **Tools**: Modify the `tools` field
3. **Model**: Change the `model` field
4. **Memory Scope**: Change `memory: user` to `memory: project` or `memory: local`
5. **Skills**: Add/remove skills in the `skills` field

Example:

```markdown
---
name: product-knowledge
description: Answer questions about product from documentation
tools: Read, Bash, Grep, Glob
model: inherit
memory: user
skills:
  - agile-product-owner
  - esign-domain-expert  # Add domain-specific skill
---

Your custom system prompt here...
```

### Add Domain-Specific Skills

For domain-specific products (e.g., eSign), create custom skills:

```bash
# Create new skill using template
cp -r /.claude/skills/template-skill /.claude/skills/my-domain-skill

# Edit SKILL.md with your domain knowledge
# Reference in agents by adding to skills: field
```

---

## Best Practices

### When to Use Agents

**Use product-knowledge agent when:**
- Need to search across multiple documentation files
- Want cited answers with source references
- Don't know where information is located

**Use feature-brainstormer agent when:**
- Need creative ideation with structure
- Want diverse ideas across categories
- Need optional user story generation

### When to Call Skills Directly

**Use skills directly when:**
- You know which framework/template to apply
- Need specific domain knowledge
- Want full control over the workflow
- Task is straightforward

### Effective Skill Usage

**Be specific about what you need:**
```
❌ "Create stories"
✅ "Use backlog-manager skill to create stories with INVEST principles and templates from references/"
```

**Reference skill resources:**
```
❌ "Prioritize features"
✅ "Use prioritization-engine skill with RICE framework from references/frameworks.md"
```

**Specify output location:**
```
❌ "Analyze requirements"
✅ "Use requirements-analyst skill to analyze requirements and output to requirements/mobile-signature/"
```

---

## Memory and Learning

Both agents have **persistent memory** enabled at the user level. They learn and improve over time by:

- Recording patterns and insights in MEMORY.md
- Building institutional knowledge across conversations
- Improving accuracy through historical data
- Adapting to your team's specific context

To view an agent's memory (stored in Claude's project memory directory):

```bash
ls ~/.claude/projects/
```

Each agent's memory is persisted in the project's memory directory and is automatically loaded into future conversations.

---

## Troubleshooting

### Agent not being invoked automatically

**Check**: Description field matches your query pattern
**Solution**: Use explicit `@agent-name` invocation or rephrase query

### Skill not found in prompt

**Check**: Skill is installed in `~/.claude/skills/`
**Solution**: Verify skill exists, check spelling in your prompt

### Want agent for specific task

**Solution**: Don't create new agent - call skill directly in prompt for more control

---

## Support and Feedback

For issues or suggestions:
- Review Claude Code documentation: https://code.claude.com/docs
- Check agent MEMORY.md files for historical context
- Modify agents to fit your team's workflow
- Create custom skills for domain-specific knowledge
- See `.claude/agents/README.md` for the full skill usage guide

---

## Version

**Version**: 3.0.0 (Simplified)
**Last Updated**: 2026-02-25
**Compatible With**: Claude Code (all versions with subagent and skills support)

**Changelog**:
- **v3.0.0**: Simplified from 14 agents to 2 agents + 9 skills (call directly)
- **v2.0.0**: Added skills integration, separated domain knowledge from workflow orchestration
- **v1.0.0**: Initial agent system

---

## License

These agents and skills are provided as templates. Customize them for your team's specific needs.
