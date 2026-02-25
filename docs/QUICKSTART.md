# PO Orchestration System — Quick Start Guide

This system helps you as a Product Owner to brainstorm, discover blind spots, structure requirements, manage your backlog, and document decisions — all through Claude Code.

---

## System Map

```
Entry Points (Skills you invoke directly)
├── /po-brainstorm [topic]    → feature-brainstormer agent → brainstorm/ output
└── /po-research [question]   → product-knowledge agent   → answer from docs

Supporting Skills (invoke directly for specific tasks)
├── backlog-manager          → create/refine user stories
├── requirements-analyst     → extract requirements from stakeholder input
├── prioritization-engine    → rank features (RICE, MoSCoW, WSJF)
├── sprint-planner           → plan sprint capacity and story selection
├── analytics-insights       → analyze user feedback and metrics
├── stakeholder-communicator → draft executive updates, release notes
├── documentation-specialist → ADRs, product docs, FAQs
├── esign-domain-expert      → compliance validation (eIDAS, ESIGN Act, etc.)
└── agile-product-owner      → INVEST stories, sprint ceremonies
```

---

## Step 1: Set Up Product Context

Fill in your product vision so agents have context:

```
Edit: product_documents/product-vision.md
```

The product-knowledge agent reads this first for every research question.
The feature-brainstormer reads it to anchor ideation in your actual product.

---

## Step 2: Your First Brainstorm

```
/po-brainstorm [topic you want to explore]
```

**Examples:**
- `/po-brainstorm improve onboarding for new users`
- `/po-brainstorm what could we do with AI in our product`
- `/po-brainstorm reduce customer churn`

**What happens:**
1. You'll be asked 1-3 quick context questions
2. The feature-brainstormer agent runs a full session:
   - Reads `product_documents/` for context
   - Generates 20+ ideas using SCAMPER + anti-bias rotation
   - Clusters ideas into themes
   - Evaluates top ideas (User Value / Business Impact / Feasibility)
   - Runs Challenge phase (Pre-Mortem, Devil's Advocate, Assumption Stress-Test)
   - Reconciles rankings after challenge
   - Saves results to `brainstorm/[topic]/SUMMARY.md` and `IDEAS.md`
   - Optionally creates draft user stories

**Mode flags:**
- `--quick` — skip ideation+clustering, go straight to evaluation (faster)
- `--challenge` — re-challenge ideas from a previous session
- `--idea` — ideation only, stop before challenge

---

## Step 3: Research Documented Decisions

```
/po-research [your question]
```

**Examples:**
- `/po-research what features are planned for Q2?`
- `/po-research what did we decide about the mobile workflow?`
- `/po-research what are the requirements for onboarding?`

**What happens:**
- product-knowledge agent searches all docs with cited source paths
- Returns only documented facts — says "I don't know" if not found
- Never guesses or infers

---

## Step 4: Create Backlog Stories

After brainstorming, promote your best ideas:

```
Use backlog-manager skill: "create user story for [idea from brainstorm]"
```

Save stories to `backlog/[feature-name]/US-NNN-[name].md`

---

## Step 5: Plan Your Sprint

```
Use sprint-planner skill: "plan sprint with 30 story points capacity"
```

Needs stories in `backlog/` marked `Ready for Sprint`.

---

## Discovering What You Don't Know

The most powerful use of this system is **surfacing unknown unknowns**:

### 1. Risk Radar (the dedicated tool)
```
/po-risk-radar
```
Scans all your documented artifacts and maps coverage against 22 strategic
concern domains (UX, compliance, security, i18n, tech debt, etc.).
Reports which domains have NO coverage with severity ratings and ready-to-use
`/po-brainstorm` commands for each blind spot.

**Run quarterly** (before roadmap planning) or before starting a new feature area.

### 2. Challenge Phase (built-in to every brainstorm)
Every `/po-brainstorm` session includes a Challenge & Critique phase that:
- Runs Pre-Mortem (what if this fails?)
- Stress-tests assumptions
- Plays Devil's Advocate
- Applies compliance/accessibility/international lenses

### 3. "What's NOT in the Backlog?"
```
/po-research what areas of [product domain] are NOT in our backlog or roadmap?
```

### 4. Assumption Audit
Review `docs/assumptions/` periodically:
```
/po-research what unvalidated assumptions do we have?
```

### 5. Domain Compliance Check
```
Use esign-domain-expert skill: "validate [feature idea] for compliance gaps"
```

---

## Documentation Flow

```
Brainstorm session
  └── brainstorm/[topic]/SUMMARY.md
      └── IDEAS.md
      └── user-stories/ (draft stories)
          └── Promote → backlog/[feature]/US-NNN.md
              └── Plan → sprints/sprint-N/PLAN.md
                  └── Document decision → docs/decisions/ADR-NNN.md
                      └── Log assumptions → docs/assumptions/ASM-NNN.md
```

---

## Key Directories

| Directory | Purpose | Created by |
|-----------|---------|-----------|
| `product_documents/` | Product vision, user research, strategy | You |
| `brainstorm/[feature]/` | Brainstorming outputs | feature-brainstormer agent |
| `backlog/[feature]/` | User stories, epics | backlog-manager skill |
| `sprints/sprint-N/` | Sprint plans and boards | sprint-planner skill |
| `requirements/[feature]/` | Formal requirement specs | requirements-analyst skill |
| `roadmap/` | Quarterly roadmap plans | prioritization-engine skill |
| `docs/decisions/` | Architecture Decision Records | documentation-specialist skill |
| `docs/assumptions/` | Assumption ledger | You + requirements-analyst |

---

## Quick Reference

| I want to... | Use this |
|-------------|---------|
| Brainstorm new feature ideas | `/po-brainstorm [topic]` |
| Find existing decisions/status | `/po-research [question]` |
| Discover what I'm NOT thinking about | `/po-risk-radar` |
| Create user stories | `backlog-manager` skill |
| Rank features by value | `prioritization-engine` skill |
| Plan a sprint | `sprint-planner` skill |
| Analyze user feedback | `analytics-insights` skill |
| Write stakeholder update | `stakeholder-communicator` skill |
| Document a decision | `documentation-specialist` skill |
| Validate compliance | `esign-domain-expert` skill |
| Extract requirements from notes | `requirements-analyst` skill |
