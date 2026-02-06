# System Architecture

## Overview

The Product Owner Orchestration System follows a **layered architecture** that separates concerns between domain knowledge (Skills), workflow orchestration (Agents), and infrastructure (Claude Code).

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
│  Agent Layer    │◄───────────►│  Skills Layer   │
│  (Orchestration)│             │  (Knowledge)    │
└────────┬────────┘             └────────┬────────┘
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
- Explicit agent invocation (@agent-name)
- File-based inputs (requirements docs, backlog files)

---

### 2. Claude Code Interface Layer

**Purpose**: Translation between user intent and agent orchestration

**Responsibilities**:
- Parse natural language requests
- Route requests to appropriate agents
- Manage conversation context
- Handle multi-agent workflows

**Key Capabilities**:
- Automatic agent delegation based on trigger phrases
- Explicit agent invocation with @mentions
- Context preservation across agent calls
- Result aggregation from multiple agents

---

### 3. Agent Layer (Workflow Orchestration)

**Purpose**: Coordinate tools to accomplish product management tasks

**Architecture**:
```
Agent = Configuration + System Prompt + Tool Access + Skill References

Components:
├── Frontmatter (YAML)
│   ├── name: Unique identifier
│   ├── description: Trigger phrases
│   ├── tools: Available tools
│   ├── model: LLM model selection
│   ├── memory: Memory scope (user/project/local)
│   └── skills: Domain knowledge references
│
└── System Prompt (Markdown)
    ├── Skills Integration: What skills provide
    ├── Core Responsibilities: What agent does
    ├── Workflow Patterns: How agent operates
    ├── Collaboration Signals: How agents coordinate
    └── Memory Management: What to remember
```

**Agent Categories**:

**Skill-Integrated Agents** (8):
- analytics-insights
- backlog-manager
- documentation-agent
- esign-domain-expert
- prioritization-engine
- requirements-analyst
- sprint-planner
- stakeholder-communicator

**Standalone Agents** (4):
- competitive-intel
- risk-assessor
- roadmap-planner
- user-research

**Storage Locations** (Priority Order):
1. CLI arguments (highest priority)
2. Project-level: `.claude/agents/`
3. User-level: `~/.claude/agents/`
4. Plugin-level (lowest priority)

---

### 4. Skills Layer (Domain Knowledge)

**Purpose**: Provide reusable domain expertise across agents

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
3. **Reusability**: Multiple agents can use same skill
4. **Versioning**: Skills can evolve independently from agents

**Storage Locations**:
- Development: `/skills/` (source files)
- Active: `/.claude/skills/` (packaged skills)
- User-level: `~/.claude/skills/` (installed skills)

**Packaging**:
```bash
cd skills/
./package_skill.py skill-name
# Creates: skill-name.skill (distributable package)
# Installs to: ~/.claude/skills/skill-name/
```

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

**Tool Restrictions by Agent**:
- **Read-only agents**: competitive-intel, risk-assessor (analysis only)
- **Read-write agents**: backlog-manager, documentation-agent (create/update)
- **Full access**: Most agents (complete workflow orchestration)

---

### 6. File System Layer

**Purpose**: Persistent storage for product management artifacts

**Directory Structure**:
```
project/
├── .claude/
│   ├── agents/                # Agent definitions
│   │   └── *.md
│   └── skills/                # Active skills
│       └── skill-name/
│           ├── SKILL.md
│           └── references/
│
├── skills/                    # Skill source (development)
│   └── skill-name/
│       ├── SKILL.md
│       └── references/
│
├── docs/                      # Product documentation
│   ├── product/
│   ├── architecture/
│   ├── workflows/
│   ├── templates/
│   └── decisions/
│
├── backlog/                   # User stories, epics
│   ├── epics/
│   └── stories/
│
├── sprint/                    # Sprint plans
│   └── sprint-XX/
│
└── data/                      # Analytics, metrics
    ├── metrics/
    └── feedback/
```

---

## Data Flow

### Example: User Story Creation Workflow

```
1. User Request
   "Create user stories for mobile signature feature"
   │
   ▼
2. Claude Code Interface
   - Parses request
   - Identifies task: user story creation
   - Routes to: @backlog-manager
   │
   ▼
3. Agent: backlog-manager
   - Receives task
   - References skill: backlog-manager
   - Uses Read tool → Extract requirements
   │
   ▼
4. Skill: backlog-manager
   - Provides INVEST principles
   - Provides user story template
   - Provides acceptance criteria patterns
   │
   ▼
5. Agent: backlog-manager (continued)
   - Applies skill's templates
   - Generates user stories
   - Uses Write tool → Create story files
   - Signals @requirements-analyst for validation
   │
   ▼
6. File System
   - Creates: backlog/stories/US-001.md
   - Updates: backlog/INDEX.md
   │
   ▼
7. Response to User
   - Summary of created stories
   - Locations of files
   - Next steps recommendation
```

### Multi-Agent Collaboration Flow

```
User: "Create Q2 roadmap"

1. @roadmap-planner (orchestrator)
   ├─► Calls @analytics-insights → Current metrics
   ├─► Calls @user-research → User needs
   ├─► Calls @competitive-intel → Market analysis
   ├─► Calls @prioritization-engine → Prioritized backlog
   └─► Synthesizes → Creates roadmap

2. @roadmap-planner
   └─► Calls @stakeholder-communicator → Executive presentation

3. Result
   ├─► Roadmap document (docs/product/roadmap-Q2-2024.md)
   └─► Executive presentation (docs/presentations/Q2-roadmap.md)
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

```markdown
# MEMORY.md (per agent)

## Patterns Learned
- [Date] Pattern: Story estimation accuracy improves with reference stories
- [Date] Pattern: Sprint capacity = velocity × 0.85 (15% buffer optimal)

## Common Tasks
- User story creation for mobile features
- Sprint planning for 2-week sprints with 6-person team

## Institutional Knowledge
- Team velocity: ~42 points/sprint (last 6 sprints)
- Common domains: eSignature, mobile apps
- Stakeholder preferences: Executive updates prefer metrics-first

## Historical Decisions
- [Date] Decision: Use RICE for feature prioritization (most effective)
- [Date] Decision: Story points: Fibonacci scale (1, 2, 3, 5, 8, 13)
```

---

## Integration Points

### External Tool Integration (Future)

```
┌─────────────────┐
│ Jira / Linear   │◄─── API Integration
└─────────────────┘
         │
         ▼
┌─────────────────────────────────┐
│  Agent: backlog-sync            │
│  - Pull stories from Jira        │
│  - Apply local analysis          │
│  - Push enriched data back       │
└─────────────────────────────────┘
```

### Webhook Integration (Future)

```
External Event → Webhook → Agent Trigger
  (GitHub PR)      (API)    (@risk-assessor)
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
- Read-only agents cannot modify files
- Bash commands sandboxed to project directory
- Memory scoped appropriately

---

## Scalability

### Horizontal Scaling
- Add more agents for new domains
- Agents operate independently
- No central coordination bottleneck

### Vertical Scaling
- Skills can grow with reference files
- Agents remain lightweight
- Memory accumulation bounded by scope

---

## Performance Considerations

### Latency
- Agent invocation: ~2-5 seconds
- Multi-agent workflows: Additive (sequential)
- Parallel agent calls: Supported (independent tasks)

### Optimization Strategies
- Cache frequently used skill content
- Minimize agent prompt size (use skills for bulk knowledge)
- Use Read tool efficiently (targeted reads, not full scans)

---

## Extensibility

### Adding New Agents
1. Create agent markdown file
2. Define frontmatter (name, tools, model, memory, skills)
3. Write system prompt
4. Install to `~/.claude/agents/`

### Adding New Skills
1. Use template: `skills/template-skill/`
2. Fill SKILL.md with domain knowledge
3. Add reference files as needed
4. Package: `./package_skill.py skill-name`

### Custom Workflows
1. Define workflow in agent prompt
2. Use collaboration signals
3. Chain agents explicitly or implicitly

---

## Monitoring & Observability

### Agent Memory Inspection
```bash
# View what agent has learned
cat ~/.claude/agent-memory/backlog-manager/MEMORY.md
```

### Workflow Tracing
- Agent collaboration signals visible in conversation
- File system changes trackable
- Memory updates logged

---

## Deployment Modes

### Local Development
```
Skills:  /skills/ (source)
Agents:  /.claude/agents/ (project-level)
Memory:  /.claude/agent-memory/ (project-scoped)
```

### User Installation
```
Skills:  ~/.claude/skills/ (user-level)
Agents:  ~/.claude/agents/ (user-level)
Memory:  ~/.claude/agent-memory/ (cross-project)
```

### Team Deployment
```
Skills:  Shared via Git (/.claude/skills/)
Agents:  Shared via Git (/.claude/agents/)
Memory:  Per-developer (local)
```

---

## Version Compatibility

| Component | Version | Compatibility |
|-----------|---------|---------------|
| Claude Code | Any with subagent support | Required |
| Skills | v1.0+ | Backward compatible |
| Agents | v2.0+ | Current architecture |
| Memory Format | Markdown | Stable |

---

## Future Architecture Enhancements

### Planned (Q1-Q2 2024)
- Workflow automation hooks
- Event-driven agent triggers
- External tool integrations (Jira, Linear)
- Real-time collaboration features

### Under Consideration
- Agent-to-agent direct communication (no user mediation)
- Distributed agent execution
- Cloud-based memory sync
- Custom skill creation UI
