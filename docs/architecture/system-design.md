# System Architecture

## Overview

The Product Owner Orchestration System follows a **simplified layered architecture** that separates concerns between domain knowledge (Skills), workflow orchestration (Agents), and infrastructure (Claude Code).

**Key Design Principle**: 3 agents for complex workflows + 13 skills for direct invocation = clarity and control.

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                         User Layer                          │
│              (Product Owners, PMs, Scrum Masters)           │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    Claude Code Interface                     │
│               (Natural Language Interaction)                 │
└────────────────────────┬────────────────────────────────────┘
                         │
         ┌───────────────┴───────────────┐
         ▼                               ▼
┌─────────────────┐             ┌─────────────────┐
│  Agent Layer    │             │  Skills Layer   │
│  (3 Agents)     │◄───────────►│  (13 Skills)    │
│                 │             │                 │
│ • Q&A           │             │ • Domain        │
│ • Brainstorm    │             │   Knowledge     │
└────────┬────────┘             │ • Frameworks    │
         │                      │ • Templates     │
         │                      └────────┬────────┘
         │                               │
         ▼                               ▼
┌─────────────────────────────────────────────────────────────┐
│                       Tools Layer                            │
│          (Read, Write, Edit, Bash, Grep, Glob)              │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                     File System Layer                        │
│        (Project files, Backlog, Documentation, Data)         │
└─────────────────────────────────────────────────────────────┘
```

## Architectural Layers

### 1. User Layer

**Purpose**: Human interaction with the system

**Components**:
- Product Owners
- Product Managers
- Scrum Masters
- Engineering Leads

**Interactions**:
- Natural language requests
- Agent invocation: `@product-knowledge`, `@feature-brainstormer`, `@po-workflow-assistant`
- Direct skill calls: "Use [skill-name] skill to..."
- File-based inputs (requirements docs, backlog files)

---

### 2. Claude Code Interface Layer

**Purpose**: Translation between user intent and execution

**Responsibilities**:
- Parse natural language requests
- Route requests to agents or skills
- Manage conversation context
- Handle multi-step workflows

**Key Capabilities**:
- Agent invocation with @mentions
- Direct skill application based on user instructions
- Context preservation across steps
- Result aggregation

---

### 3. Agent Layer (Workflow Orchestration)

**Purpose**: Orchestrate tools for complex workflows

**Current Agents (3)**:

#### product-knowledge
```yaml
name: product-knowledge
description: Answer questions about product from documentation
tools: Read, Glob, Grep
model: inherit
```

**Responsibilities**:
- Search all product documentation
- Never guess — only answer from documented information
- Always cite sources (file:line)
- Say "I don't know" when info not found

**Workflow**:
1. Parse user question
2. Use Glob to find relevant files
3. Use Grep to search content
4. Use Read to extract details
5. Synthesize answer with citations

---

#### feature-brainstormer
```yaml
name: feature-brainstormer
description: Facilitate creative brainstorming with optional story creation
tools: Read, Write, Edit, Bash, Grep, Glob
model: opus
```

**Responsibilities**:
- Facilitate structured brainstorming sessions
- Generate 50-100+ diverse ideas across standard and deep challenge phases
- Evaluate feasibility and impact
- Optional: Create user stories with estimates
- Save output to `brainstorm/[feature-name]/`

**Flags**:
- `--personas`: Activates Persona Council (Step 1.5) before SCAMPER — 7 stakeholder personas each generate 3-5 ideas from their POV
- `--deep`: After the standard 6 challenge sub-phases (4a-4f), runs 5 enhanced sub-phases (4g-4k) on the top 3 ideas
- Flags combine freely: `--deep --personas` runs both; `--challenge --deep` re-challenges with deep sub-phases

**Standard challenge sub-phases (4a-4f)**:
- 4a Pre-Mortem, 4b Assumption Stress-Test, 4c Devil's Advocate, 4d Constraint Inversion, 4e Anti-Bias Challenge, 4f Clustering Stress-Test

**Deep challenge sub-phases (4g-4k, activated by --deep)**:
- 4g Steelman Protocol, 4h Socratic Depth, 4i Assumption Ladder, 4j Regulatory Pre-Mortem, 4k Anti-Pattern Check

**Agent reference files used**:
- `brainstorm-templates.md` — output templates including Persona Council Findings table and Deep Challenge Results tables
- `challenge-techniques.md` — question banks for 4a-4f + Section 6 Deep Challenge Techniques (4g-4k)
- `persona-profiles.md` — 7 stakeholder persona profiles for Persona Council

**Workflow**:
1. Read product context from `product_documents/`
2. (If `--personas`) Run Persona Council (Step 1.5): each persona generates 3-5 ideas
3. Generate ideas via SCAMPER across multiple categories
4. Run standard challenge sub-phases 4a-4f
5. (If `--deep`) Run deep challenge sub-phases 4g-4k on top 3 ideas
6. Evaluate each idea (feasibility, impact)
7. Create summary with top recommendations
8. Optional: Generate user stories with estimates

---

#### po-workflow-assistant
```yaml
name: po-workflow-assistant
description: Assist with PO workflow planning and strategic decisions
tools: Read, Glob, Grep, Write
model: inherit
```

**Responsibilities**:
- Guide product owners through workflow decisions
- Help with strategic planning and prioritization
- Read and synthesize product documentation
- Write workflow summaries and planning artifacts

**Workflow**:
1. Read relevant product and workflow documentation
2. Synthesize context from multiple sources
3. Provide structured guidance and recommendations
4. Write output artifacts as needed

---

**Agent Architecture**:
```
Agent = Configuration + System Prompt + Tool Access + Skill References

Components:
├── Frontmatter (YAML)
│   ├── name: Unique identifier
│   ├── description: Purpose and usage
│   ├── tools: Available tools
│   ├── model: LLM model selection
│   ├── memory: Memory scope (user/project/local)
│   └── skills: Domain knowledge references
│
└── System Prompt (Markdown)
    ├── Skills Integration: What skills provide
    ├── Core Responsibilities: What agent does
    ├── Workflow Patterns: How agent operates
    └── Memory Management: What to remember
```

**Storage Locations** (Priority Order):
1. CLI arguments (highest priority)
2. Project-level: `.claude/agents/`
3. User-level: `~/.claude/agents/`
4. Plugin-level (lowest priority)

---

### 4. Skills Layer (Domain Knowledge)

**Purpose**: Provide reusable domain expertise called directly by users

**Current Skills (13)**:

1. **agile-product-owner** - User stories, INVEST principles, estimation (+ scripts/)
2. **analytics-insights** - Metrics frameworks (HEART, AARRR), A/B testing
3. **backlog-manager** - Story templates, epic breakdown (+ 2 reference files)
4. **documentation-specialist** - PRD/ADR templates, documentation standards
5. **esign-domain-expert** - eIDAS/ESIGN compliance, audit trails (+ 1 reference file)
6. **po-brainstorm** - Brainstorm entry point; supports `--deep` and `--personas` flags
7. **po-research** - Research entry point
8. **po-risk-radar** - Blind spot detector
9. **prioritization-engine** - RICE/MoSCoW/WSJF frameworks (+ 1 reference file)
10. **requirements-analyst** - Requirements extraction, gap analysis (+ 1 reference file)
11. **sprint-planner** - Sprint planning methodology, capacity calculation
12. **stakeholder-communicator** - Communication templates, audience guidelines
13. **writing-clearly-and-concisely** - Docs, commits, UI text (+ elements-of-style/)

**Architecture**:
```
Skill = Main Content + Reference Files + Optional Scripts

Structure:
skill-name/
├── SKILL.md                    # Core domain knowledge
├── references/                 # Supporting materials
│   ├── frameworks.md           # Detailed methodologies
│   ├── templates.md            # Reusable templates
│   └── examples.md             # Complete examples
└── scripts/                    # Optional utility scripts
    └── helper.py
```

**Design Principles**:
1. **Progressive Disclosure**: Main SKILL.md is concise, references provide depth
2. **Single Responsibility**: Each skill covers one domain area
3. **Reusability**: Multiple agents can use same skill, users call directly
4. **Versioning**: Skills can evolve independently

**Storage Locations**:
- Development: `/claude/skills/` (source files)
- Active: `/.claude/skills/` (packaged skills)
- User-level: `~/.claude/skills/` (installed skills)

**Skills with Reference Files**:
- `backlog-manager/references/` — 2 files (story-templates.md, epic-breakdown-example.md)
- `esign-domain-expert/references/` — 1 file (domain-knowledge.md)
- `prioritization-engine/references/` — 1 file (frameworks.md)
- `requirements-analyst/references/` — 1 file (examples.md)

**Agent Reference Files** (in `.claude/agents/references/`):
- `brainstorm-templates.md` — output templates: SUMMARY.md, IDEAS.md, user stories, Persona Council Findings table, Deep Challenge Results tables
- `challenge-techniques.md` — question banks for sub-phases 4a-4f + Section 6 Deep Challenge Techniques (4g-4k)
- `knowledge-patterns.md` — knowledge retrieval patterns
- `persona-profiles.md` — 7 stakeholder persona profiles for Persona Council (Enterprise Buyer, New User, CFO, Competitor Analyst, Support Lead, Power User, Regulator)
- `user-interaction-patterns.md` — interaction and clarification patterns

**Skills with Scripts**:
- `agile-product-owner/scripts/` - user_story_generator.py

---

### 5. Tools Layer

**Purpose**: Provide file system and command-line operations

**Available Tools**:

| Tool | Purpose | Operations |
|------|---------|------------|
| **Read** | Read file contents | View files, extract data |
| **Write** | Create new files | Generate docs, create files |
| **Edit** | Modify existing files | Update content, refactor |
| **Bash** | Execute commands | Run scripts, process data |
| **Grep** | Search file contents | Find patterns, extract info |
| **Glob** | Find files by pattern | Locate files, list directories |

**Tool Usage by Agent**:
- **product-knowledge**: Read, Glob, Grep (search-focused)
- **feature-brainstormer**: Read, Write, Edit, Bash, Grep, Glob (full workflow)
- **po-workflow-assistant**: Read, Glob, Grep, Write (read-heavy, limited write)

**Tool Usage by Skills**:
- Skills don't use tools directly
- Users apply skills, then use tools as needed

---

### 6. File System Layer

**Purpose**: Persistent storage for product management artifacts

**Directory Structure**:
```
ProductOwnerOrchestration/
├── .claude/
│   ├── agents/                    # Agent definitions (3 agents)
│   │   ├── feature-brainstormer.md
│   │   ├── product-knowledge.md
│   │   ├── po-workflow-assistant.md
│   │   └── references/            # Agent reference files (5 files)
│   │       ├── brainstorm-templates.md
│   │       ├── challenge-techniques.md
│   │       ├── knowledge-patterns.md
│   │       ├── persona-profiles.md
│   │       └── user-interaction-patterns.md
│   │
│   ├── skills/                    # Skills source (13 skills)
│   │   ├── agile-product-owner/
│   │   │   ├── SKILL.md
│   │   │   └── scripts/user_story_generator.py
│   │   ├── analytics-insights/SKILL.md
│   │   ├── backlog-manager/
│   │   │   ├── SKILL.md
│   │   │   └── references/
│   │   │       ├── story-templates.md
│   │   │       └── epic-breakdown-example.md
│   │   ├── documentation-specialist/SKILL.md
│   │   ├── esign-domain-expert/
│   │   │   ├── SKILL.md
│   │   │   └── references/domain-knowledge.md
│   │   ├── po-brainstorm/SKILL.md
│   │   ├── po-research/SKILL.md
│   │   ├── po-risk-radar/SKILL.md
│   │   ├── prioritization-engine/
│   │   │   ├── SKILL.md
│   │   │   └── references/frameworks.md
│   │   ├── requirements-analyst/
│   │   │   ├── SKILL.md
│   │   │   └── references/examples.md
│   │   ├── sprint-planner/SKILL.md
│   │   ├── stakeholder-communicator/SKILL.md
│   │   ├── writing-clearly-and-concisely/
│   │   │   ├── SKILL.md
│   │   │   └── elements-of-style/
│   │   └── document-skills/         # Document processing skills (separate)
│   │       ├── docx/
│   │       ├── pdf/
│   │       ├── pptx/
│   │       └── xlsx/
│   │
│   └── workflows/                 # Workflow guides (3 files)
│       ├── brainstorming-workflow.md
│       ├── feature-development-workflow.md
│       └── sprint-planning-workflow.md
│
├── docs/                          # Documentation
│   ├── HOW_TO_USE_SKILLS.md      # Skills usage guide
│   ├── workflows/                 # Workflow guides (3 files)
│   ├── architecture/              # Architecture docs (4 files)
│   └── product/                   # Product docs (2 files)
│
├── product_documents/             # Product vision, user research
├── brainstorm/                    # Brainstorming outputs
├── backlog/                       # User stories
├── sprints/                       # Sprint plans
├── requirements/                  # Requirements docs
└── README.md                      # Project README
```

---

## Data Flow

### Example 1: Q&A Workflow

```
1. User Request
   "@product-knowledge - What are our Q2 priorities?"
   │
   ▼
2. Claude Code Interface
   - Parses @mention
   - Routes to: product-knowledge agent
   │
   ▼
3. Agent: product-knowledge
   - Uses Glob tool → Find roadmap files
   - Uses Grep tool → Search for "Q2" and "priorities"
   - Uses Read tool → Extract relevant sections
   - References agile-product-owner skill for context
   │
   ▼
4. Skill: agile-product-owner
   - Provides product management context
   - Provides prioritization frameworks
   │
   ▼
5. Agent: product-knowledge (continued)
   - Synthesizes answer from findings
   - Cites sources (file:line)
   - Returns answer to user
   │
   ▼
6. Response to User
   - Answer with citations
   - "Based on docs/product/roadmap-q2.md:23..."
```

### Example 2: Direct Skill Invocation Workflow

```
1. User Request
   "Use backlog-manager skill to create user stories for mobile signature feature"
   │
   ▼
2. Claude Code Interface
   - Recognizes direct skill call
   - Loads backlog-manager skill
   - Applies skill knowledge to task
   │
   ▼
3. Skill: backlog-manager
   - Provides INVEST principles
   - Provides user story template from references/story-templates.md
   - Provides epic breakdown patterns
   │
   ▼
4. Execution (Claude with Skill Context)
   - Applies skill's templates to feature context
   - Generates user stories
   - Uses Write tool → Create story files
   │
   ▼
5. File System
   - Creates: backlog/mobile-signature/US-001.md
   - Creates: backlog/mobile-signature/US-002.md
   - Creates: backlog/mobile-signature/README.md
   │
   ▼
6. Response to User
   - Summary of created stories
   - Locations of files (backlog/mobile-signature/)
   - Story points and acceptance criteria
```

### Example 3: Brainstorming Workflow

```
1. User Request
   "@feature-brainstormer - Brainstorm AI features for mobile document prep"
   │
   ▼
2. Claude Code Interface
   - Routes to: feature-brainstormer agent
   │
   ▼
3. Agent: feature-brainstormer
   - Uses Read tool → Extract context from product_documents/
   - References agile-product-owner skill
   - Generates 65+ ideas across categories
   - Evaluates feasibility (1-10 scale)
   - Uses Write tool → Create brainstorm/ai-mobile-prep/IDEAS.md
   - Uses Write tool → Create brainstorm/ai-mobile-prep/SUMMARY.md
   - Uses Write tool → Create brainstorm/ai-mobile-prep/NEXT_STEPS.md
   │
   ▼
4. Agent: feature-brainstormer (optional)
   - Asks: "Create draft user stories?"
   - If YES: Uses agile-product-owner skill
   - Generates stories with estimates
   - Uses Write tool → Create brainstorm/ai-mobile-prep/user-stories/
   │
   ▼
5. Response to User
   - Summary of ideas generated (65+)
   - Top 10 recommendations
   - Optional: User stories created
   - Next steps for implementation
```

---

## Memory Architecture

### Memory Scopes

| Scope | Location | Persistence | Use Case |
|-------|----------|-------------|----------|
| **User** | `~/.claude/agent-memory/<agent>/` | All projects | Cross-project learning |
| **Project** | `.claude/agent-memory/<agent>/` | Single project | Project-specific patterns |
| **Local** | Session only | Current session | Temporary context |

### Memory Content Structure

Both agents use **user-level memory** to learn across projects:

```markdown
# MEMORY.md (per agent)

## Patterns Learned
- [Date] Pattern: Product questions often require searching multiple doc types
- [Date] Pattern: Brainstorming sessions benefit from diverse categories

## Common Tasks
- Q&A about roadmaps, priorities, compliance
- Brainstorming for mobile features and AI capabilities
- User story creation from brainstorming output

## Institutional Knowledge
- Documentation structure: product_documents/, docs/product/, docs/architecture/
- Common domains: eSignature, mobile apps, AI features
- Team preferences: INVEST-compliant stories, Fibonacci scale

## Historical Decisions
- [Date] Decision: Never guess when answering questions - cite sources or say "I don't know"
- [Date] Decision: Optional user story creation gives users flexibility
```

---

## Usage Patterns

### When to Use Agents

**Use @product-knowledge when**:
- Need to search documentation
- Want cited answers from docs
- Don't know where information is located
- Need comprehensive document search

**Use @feature-brainstormer when**:
- Need creative ideation
- Want structured brainstorming with evaluation
- Need optional user story generation
- Want 50-100+ diverse ideas
- Use `--personas` to activate the Persona Council (7 stakeholder POVs)
- Use `--deep` to run enhanced challenge sub-phases (4g-4k) on the top 3 ideas

**Use @po-workflow-assistant when**:
- Need guidance on PO workflow decisions
- Want structured support for strategic planning
- Need to synthesize information across multiple product documents

### When to Call Skills Directly

**Call skills directly when**:
- Creating artifacts (stories, plans, docs)
- Applying specific frameworks (RICE, INVEST, MoSCoW)
- Need full control over the process
- Want to see methodology explicitly
- Task is straightforward

**Example Direct Skill Calls**:
```
Use backlog-manager skill to create user stories...
Use sprint-planner skill to plan Sprint 12...
Use prioritization-engine skill with RICE framework...
Use requirements-analyst skill to analyze requirements...
Use documentation-specialist skill to create PRD...
```

---

## Multi-Step Workflow Pattern

Users compose workflows by combining agents and skills:

```
Example: Complete Feature Development

Step 1: Brainstorm
@feature-brainstormer - Brainstorm [feature topic]

Step 2: Create Stories (Direct Skill Call)
Use backlog-manager skill to create stories from brainstorm/[feature]/SUMMARY.md
- Reference templates from backlog-manager/references/
- Apply INVEST principles
- Create in backlog/[feature]/

Step 3: Prioritize (Direct Skill Call)
Use prioritization-engine skill with RICE framework
- Score stories from backlog/[feature]/
- Rank by RICE score
- Output to backlog/[feature]/PRIORITY_RANKING.md

Step 4: Plan Sprint (Direct Skill Call)
Use sprint-planner skill
- Team: [capacity details]
- Select top-ranked stories
- Create sprints/sprint-X/sprint-plan.md

Step 5: Q&A
@product-knowledge - What compliance requirements apply to this feature?
```

---

## Security & Privacy

### Data Handling
- All processing happens locally
- No data sent to external services (except Claude API for LLM)
- Sensitive data stays in project files
- Memory files respect project boundaries

### Agent Permissions
- Agents have explicit tool restrictions
- product-knowledge: Read, Glob, Grep — search-only, no writes
- feature-brainstormer: Read, Write, Edit, Bash, Grep, Glob — full workflow orchestration
- po-workflow-assistant: Read, Glob, Grep, Write — read-heavy with limited write
- Bash commands sandboxed to project directory

---

## Performance Considerations

### Latency
- Agent invocation: ~2-5 seconds
- Direct skill application: Immediate (no agent overhead)
- Multi-step workflows: Sequential execution
- Document search (product-knowledge): Depends on document count

### Optimization Strategies
- Cache frequently used skill content
- Minimize agent prompt size (use skills for bulk knowledge)
- Use Read tool efficiently (targeted reads, not full scans)
- Direct skill calls faster than agent delegation for simple tasks

---

## Extensibility

### Adding Custom Skills

1. Create skill directory in `claude/skills/`:
```bash
mkdir claude/skills/my-custom-skill
```

2. Create SKILL.md with domain knowledge:
```markdown
---
name: my-custom-skill
description: Custom domain expertise
---

# My Custom Skill

[Domain knowledge, frameworks, templates]
```

3. Add reference files (optional):
```bash
mkdir claude/skills/my-custom-skill/references
# Add templates, examples, frameworks
```

4. Reference in agent or call directly:
```
Use my-custom-skill to [task]
```

### Modifying Agents

Edit agent markdown files in `claude/agents/`:
- Change system prompt
- Adjust tool access
- Update skill references
- Modify memory scope

---

## Deployment Modes

### Local Development
```
Agents:  /claude/agents/ (project-level)
Skills:  /claude/skills/ (source files)
Memory:  /.claude/agent-memory/ (project-scoped)
```

### User Installation
```
Agents:  ~/.claude/agents/ (user-level)
Skills:  ~/.claude/skills/ (user-level)
Memory:  ~/.claude/agent-memory/ (cross-project)
```

### Team Deployment
```
Agents:  Shared via Git (/claude/agents/)
Skills:  Shared via Git (/claude/skills/)
Memory:  Per-developer (local)
```

---

## Version Compatibility

| Component | Version | Compatibility |
|-----------|---------|---------------|
| Claude Code | Any with subagent support | Required |
| System Architecture | v4.2 | Current |
| Agents | 3 agents | Stable |
| Skills | 13 skills | Backward compatible |
| Agent References | 5 files | Stable |

---

## Architecture Benefits

### Simplification (v3.0+)
- ✅ **Clearer**: 3 focused agents vs 14 agents
- ✅ **More Control**: Direct skill calls vs agent delegation
- ✅ **More Transparent**: Users see methodology explicitly
- ✅ **Easier to Learn**: Simple mental model (3 agents + 13 skills)

### Separation of Concerns
- ✅ **Agents**: Complex workflows requiring tool orchestration
- ✅ **Skills**: Domain knowledge called directly by users
- ✅ **Clear Boundary**: Agents orchestrate, skills inform

### Scalability
- ✅ Add new skills without adding agents
- ✅ Skills reusable across projects
- ✅ Memory accumulation bounded by scope
- ✅ No central coordination bottleneck

---

## System Evolution

### Version History
- **v4.2.0** (2026-02-28): Added --deep flag (challenge sub-phases 4g-4k), --personas flag (Persona Council with 7 stakeholder personas), persona-profiles.md agent reference; updated po-brainstorm skill with flag support
- **v4.0.0** (2026-02-XX): Added po-workflow-assistant agent; expanded to 13 skills (added po-brainstorm, po-research, po-risk-radar, writing-clearly-and-concisely)
- **v3.0.0** (2026-02-07): Simplified to 2 agents + 9 skills (call directly)
- **v2.0.0** (2026-02-06): Added skills integration (14 agents + 8 skills)
- **v1.0.0** (2026-01-XX): Initial agent system

### Design Decisions
- **Simplification**: Reduced agent count for clarity (user feedback: "too many agents")
- **Direct Skill Calls**: Users wanted more control over which knowledge to apply
- **Agent Retention**: Kept only agents providing unique workflow value (Q&A, brainstorming)
- **Skill Expansion**: Maintained all skills as direct-access domain knowledge

### Future Considerations
- Additional skills for new domains (as needed)
- External tool integrations (Jira, Linear)
- Workflow automation hooks
- Performance monitoring

---

## Monitoring & Observability

### Agent Memory Inspection
```bash
# View what product-knowledge has learned
cat ~/.claude/agent-memory/product-knowledge/MEMORY.md

# View what feature-brainstormer has learned
cat ~/.claude/agent-memory/feature-brainstormer/MEMORY.md

# View what po-workflow-assistant has learned
cat ~/.claude/agent-memory/po-workflow-assistant/MEMORY.md
```

### Workflow Tracing
- Agent activities visible in conversation
- File system changes trackable (backlog/, brainstorm/, docs/)
- Memory updates logged in MEMORY.md
- Direct skill calls explicit in user prompts

---

## Conclusion

The Product Owner Orchestration System v4.2 provides a **simplified, controllable, and transparent** architecture:

- **3 Agents**: Handle complex workflows (Q&A, brainstorming, PO workflow assistance)
- **13 Skills**: Provide domain knowledge users call directly
- **Clear Separation**: Agents orchestrate tools, skills provide knowledge
- **User Control**: Direct skill calls give full transparency and control

This architecture prioritizes clarity over magic, control over convenience, and simplicity over complexity.
