# Orchestration Review — Brainstorm Summary

**Date**: 2026-02-26
**Participants**: Product Owner + Claude Code
**Topic**: Review `.claude/` folder — understand workflow, orchestration consistency, PO discovery of unknown unknowns
**Scope**: Full audit of 2 agents + 12 skills + reference files + content directories

---

## Problem Statement

As a solo Product Owner, I need confidence that:
1. The agents and skills work together **consistently** — no broken links, missing pieces, or silent failures
2. The system can help me **discover what I don't know** — not just answer questions I think to ask
3. All discovery outputs are **documented correctly** — from ideation through backlog to sprint

---

## Scouted State (What We Found)

### Agents (2)
| Agent | Model | Has `tools`? | Trigger Keywords |
|-------|-------|-------------|-----------------|
| `feature-brainstormer` | sonnet | ❌ Missing | brainstorm, ideate, generate ideas, innovative features, explore improvements, challenge ideas, stress-test, critique |
| `product-knowledge` | sonnet | ❌ Missing | what features, what's the status, what did we decide, why did we, what are the requirements, what's in the roadmap |

### Skills (12)
| Skill | Role in PO Workflow |
|-------|-------------------|
| `po-brainstorm` | Entry point → routes to feature-brainstormer |
| `po-research` | Entry point → routes to product-knowledge |
| `agile-product-owner` | Embedded context in both agents (INVEST, story templates) |
| `backlog-manager` | Story creation, epic breakdown, INVEST validation |
| `requirements-analyst` | Extract & analyze requirements from stakeholder input |
| `prioritization-engine` | RICE, MoSCoW, WSJF ranking |
| `sprint-planner` | Capacity planning, story selection |
| `analytics-insights` | Metrics, user feedback, A/B tests, KPIs |
| `stakeholder-communicator` | Executive updates, release notes, roadmap presentations |
| `documentation-specialist` | ADRs, product docs, FAQs, onboarding |
| `esign-domain-expert` | eIDAS, ESIGN Act, compliance for eSign products |
| `writing-clearly-and-concisely` | Strunk's rules for docs/commits/UI text |

### Reference Files
- `.claude/agents/references/challenge-techniques.md` — question banks for challenge sub-phases
- `.claude/agents/references/user-interaction-patterns.md` — AskUserQuestion constraint documentation + 3 approved patterns

### Content Directories (actual vs expected)
| Directory | Expected | Actual |
|-----------|----------|--------|
| `product_documents/` | ✅ | ✅ (README + product-vision.md) |
| `brainstorm/` | ✅ | ✅ (README only, now + this review) |
| `backlog/` | ✅ | ❌ Missing |
| `sprints/` | ✅ | ❌ Missing |
| `requirements/` | ✅ | ❌ Missing |
| `roadmap/` | ✅ | ❌ Missing |
| `competitive_intel/` | Referenced in agent | ❌ Missing |
| `docs/` | ✅ | ✅ |

---

## Key Gaps Found

### CRITICAL (Break functionality)

#### GAP-1: Missing `tools` field in both agents
Both `feature-brainstormer.md` and `product-knowledge.md` are missing the `tools:` frontmatter field.
CLAUDE.md specifies this field as required. Without it, tool access is undefined.
**Fix**: Add `tools: Read, Write, Edit, Bash, Grep, Glob` to both agent frontmatter blocks.

#### GAP-2: Missing content directories
`product-knowledge` agent searches `backlog/`, `sprints/`, `requirements/`, `roadmap/`, `competitive_intel/`.
None of these directories exist. The agent will silently return "I don't know" for any question that would
be answered by those directories — without telling the PO that the directories are simply missing.
**Fix**: Scaffold all missing directories with `README.md` starters.

#### GAP-3: No "Unknown Unknowns" discovery capability
The system is entirely **reactive** — it answers questions you ask and brainstorms topics you bring.
There is no proactive mechanism to tell a PO: "Here are areas you haven't thought about."
A solo PO's biggest risk is not knowing what they don't know.
**Fix**: Add a Risk Radar / Blind Spot Detector workflow (see recommendations below).

---

### HIGH (Reduce effectiveness)

#### GAP-4: Brainstorm-to-backlog flow is manual with no bridge
The documented flow is: `brainstorm/ → backlog/ → sprint/ → requirements/`
The system generates SUMMARY.md and IDEAS.md in brainstorm/, and optionally draft user stories.
But there is no mechanism to formally move those draft stories into `backlog/` entries.
A PO would lose track of accepted ideas unless they manually create backlog files.
**Fix**: Add a "promote to backlog" step at the end of feature-brainstormer, or document the manual workflow.

#### GAP-5: Direct agent triggers bypass pre-discovery
`feature-brainstormer` auto-triggers on "brainstorm", "ideate", etc.
When triggered directly, the `po-brainstorm` skill's pre-discovery phase (AskUserQuestion for persona,
constraints, session type) is skipped entirely.
The agent doesn't know context it hasn't been given.
**Fix**: Either make trigger keywords exclusive to the skill (not the agent), or add a note in
feature-brainstormer to self-ask in output when context is missing.

#### GAP-6: `agile-product-owner` skill integration is misleading
Both agents say they "use" the agile-product-owner skill. Skills are static context files, not
dynamically loadable modules. The phrasing suggests runtime integration that doesn't exist.
**Fix**: Update the Skills Integration section in both agents to accurately describe that the
skill's knowledge is baked into the agent's context, not dynamically loaded.

---

### MEDIUM (Reduce discoverability)

#### GAP-7: No documentation flow for decisions
When brainstorming concludes with a recommendation, there's no automatic ADR creation.
The documentation-specialist skill can create ADRs, but it's never invoked by feature-brainstormer.
Decisions made in brainstorm sessions may not be formally recorded.
**Fix**: Add "Create ADR" as an optional post-brainstorm step.

#### GAP-8: `esign-domain-expert` is hardcoded to one domain
The skill provides deep eSign compliance knowledge. But if this PO moves to a different product,
this skill becomes irrelevant and there's no guidance on how to replace it.
**Fix**: Document a "domain expert swap" pattern in CLAUDE.md.

#### GAP-9: `analytics-insights` skill requires real data but has none
The skill describes analyzing feature adoption rates, A/B tests, KPIs. But the system has no
data sources configured. A solo PO using this skill will get template output with placeholder metrics.
**Fix**: Add a note in the skill description that it requires actual data input, and document
how to bring data in (paste CSV, describe metrics, upload report).

#### GAP-10: No PO onboarding guide
A new PO (or this PO returning after a break) has no "start here" document explaining how to
use the system from day 1: which skill to invoke first, what to fill in product_documents/, etc.
**Fix**: Create `docs/QUICKSTART.md`.

---

### LOW (Nice-to-have)

#### GAP-11: `competitive_intel/` referenced but undocumented
The product-knowledge agent lists this as a search location but the directory doesn't exist
and CLAUDE.md doesn't mention it.

#### GAP-12: `writing-clearly-and-concisely` skill has unclear PO trigger
Good skill, but the description and trigger scenarios don't mention PO-specific use cases
(e.g., "clean up my release notes", "rewrite this user story more clearly").

#### GAP-13: No Parking Lot review mechanism
feature-brainstormer correctly captures rejected/deferred ideas in a "Parking Lot" section.
But there's no mechanism to periodically review those ideas — they may be timely now.

---

## Idea Clusters (from IDEAS.md)

| Cluster | Theme | Ideas | Priority |
|---------|-------|-------|---------|
| A | Unknown Unknowns Discovery | A1-A10 | HIGH |
| B | Documentation Flow | B1-B8 | HIGH |
| C | Orchestration Consistency | C1-C8 | CRITICAL |
| D | PO-Specific Workflows | D1-D10 | MEDIUM |
| E | Meta / System-Level | E1-E7 | LOW |

---

## Evaluation of Top Ideas

| Idea | User Value | Business Impact | Feasibility | Total | Rank |
|------|-----------|----------------|-------------|-------|------|
| C1: Add tools fields to agents | 5 | 5 | 5 | 15 | #1 |
| B8: Scaffold missing directories | 5 | 5 | 5 | 15 | #1 |
| A1: Proactive Risk Radar Agent | 5 | 5 | 3 | 13 | #3 |
| B1: Brainstorm-to-Backlog Bridge | 4 | 5 | 4 | 13 | #3 |
| C3: Make po-brainstorm canonical | 4 | 4 | 5 | 13 | #3 |
| A3: Blind Spot Detector | 4 | 4 | 3 | 11 | #6 |
| B4: Decision Log Auto-Population | 4 | 4 | 4 | 12 | #4 |
| E6: PO Onboarding Quickstart | 3 | 4 | 5 | 12 | #4 |
| D2: Feature Hypothesis Builder | 4 | 4 | 3 | 11 | #6 |
| C7: Skill integration clarity | 3 | 3 | 5 | 11 | #6 |

---

## Challenge & Critique

### Pre-Mortem: What Could Go Wrong?

**Risk 1 — Agent overload**: Adding more agents/skills increases cognitive load. If PO doesn't know which
to invoke, the system becomes unusable. Mitigation: Good QUICKSTART.md and po-brainstorm as canonical entry.

**Risk 2 — Empty directories give false confidence**: Creating scaffold directories (backlog/, sprints/)
might give a PO false sense that the system is ready, when the directories are empty.
Mitigation: Each README should clearly state "No entries yet — use X skill to create first entry."

**Risk 3 — Risk Radar generates noise**: A proactive risk scanning agent could surface so many "blind spots"
that the PO becomes overwhelmed and ignores everything.
Mitigation: Limit to 3-5 highest-priority risks per scan, with severity scoring.

### Assumption Stress-Test

| Assumption | Evidence | If Wrong... | Blast Radius |
|------------|----------|-------------|--------------|
| Both agents work without explicit `tools` field | Not tested — may default correctly in Claude Code | Agents silently lack file access | HIGH — core workflow breaks |
| PO will fill in product_documents/ with real content | product-vision.md exists | product-knowledge returns "I don't know" to everything | MEDIUM — PO thinks system is broken |
| feature-brainstormer correctly detects sub-agent mode | Documented in agent | Agent tries to call AskUserQuestion, hangs | HIGH — po-brainstorm blocks |
| All skills are available in Claude Code skill registry | Listed in system reminder | Skills not found when invoked | MEDIUM — skill invocation fails |

### Devil's Advocate

**Against building Risk Radar (A1)**:
- The PO may not have enough product context loaded to generate meaningful risk insights
- The system doesn't know what it doesn't know — it can only surface risks in domains it's been trained on
- Better mitigation: Run the challenge phase of every brainstorm rigorously rather than a separate agent

**Against Brainstorm-to-Backlog Bridge (B1)**:
- Premature formalization — brainstorm ideas need time to mature before becoming backlog items
- A bridge could dump unqualified ideas into the backlog, polluting it
- Better mitigation: Keep the boundary intentional; require PO review before promotion

### Constraint Inversion

**If PO has 10x more time**: Would use multi-agent orchestration with Proactive Risk Radar + Analytics Integration
**If PO has 1/10th time (critical path)**: Focus only on C1 (tools field) + B8 (scaffold dirs) — everything else is optimization
**If another PO joins**: Need E6 (onboarding quickstart) immediately — current system has zero documentation for newcomers

### Ranking After Challenge

Post-challenge, the ranking remains:
1. **C1 + B8** (CRITICAL infrastructure fixes) — no challenge weakened this
2. **B1 (Brainstorm-to-Backlog Bridge)** — devil's advocate raises valid concern; recommend keeping intentional/manual with clear guidance
3. **A1 (Risk Radar)** — valuable but complex; start with extending challenge phase first (A3 is easier)
4. **E6 (Quickstart)** — moved up after constraint inversion revealed newcomer risk

---

## Recommended Approach

### Phase 1: Fix Infrastructure (Do This Now — 30 min)
1. Add `tools: Read, Write, Edit, Bash, Grep, Glob` to both agents
2. Scaffold missing directories: `backlog/`, `sprints/`, `requirements/`, `roadmap/`, `docs/decisions/`
3. Update `product-knowledge` agent to remove `competitive_intel/` or document it
4. Update CLAUDE.md to clarify skill integration (static context, not dynamic loading)

### Phase 2: Documentation Flow (This Week)
5. Add "promote to backlog" guidance at end of feature-brainstormer workflow
6. Add optional "Create ADR" step after brainstorm recommendation
7. Create `docs/QUICKSTART.md` — how to use this system from day 1
8. Add README starters to each scaffolded directory

### Phase 3: PO Discovery Enhancement (Next Sprint)
9. Add Blind Spot Detector (A3) to feature-brainstormer as a post-challenge sub-phase
10. Add "What's NOT in the Backlog?" prompt to product-knowledge
11. Add Assumption Ledger pattern — store assumptions in `docs/assumptions/`
12. Add Feature Hypothesis Builder to feature-brainstormer output

### Phase 4: Advanced Discovery (Future)
13. Proactive Risk Radar Agent (A1) — after Phase 1-3 have real data to scan
14. Multi-product support documentation
15. Parking Lot review mechanism

---

## Next Steps

1. [ ] **Immediately**: Fix GAP-1 (add tools fields to agents)
2. [ ] **Immediately**: Scaffold missing directories with README starters
3. [ ] **This week**: Create docs/QUICKSTART.md
4. [ ] **This week**: Add brainstorm → backlog guidance to feature-brainstormer
5. [ ] **Next sprint**: Extend feature-brainstormer with Blind Spot Detector (A3)
6. [ ] **Next sprint**: Add "What's NOT in Backlog?" to product-knowledge
7. [ ] **Future**: Build Proactive Risk Radar Agent

---

## Related Documents

- `.claude/agents/feature-brainstormer.md` — main discovery agent
- `.claude/agents/product-knowledge.md` — document search agent
- `.claude/agents/references/user-interaction-patterns.md` — AskUserQuestion constraint docs
- `.claude/agents/references/challenge-techniques.md` — challenge phase question banks
- `brainstorm/orchestration-review/IDEAS.md` — all 37 ideas generated

---

## Questions to Resolve

1. Does Claude Code actually require the `tools` field in agent frontmatter, or does it default to all tools?
2. Should brainstorm → backlog promotion be automatic or always require PO approval?
3. Is `esign-domain-expert` the permanent domain for this PO, or should it be replaceable?
4. Should the Risk Radar be a new agent or an extension to feature-brainstormer's challenge phase?

---

## Parking Lot (Ideas for Later)

- Multi-product support architecture
- Skill usage tracker / analytics
- Context scale strategy as product_documents/ grows
- Sprint retrospective brainstorm automation
- Dependency spider map visualization
