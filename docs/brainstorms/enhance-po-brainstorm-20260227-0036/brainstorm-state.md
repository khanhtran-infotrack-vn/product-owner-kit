# Brainstorm State
**Topic**: How to enhance po-brainstorm for a solo product owner and project manager who wants more ideas and stronger challenges during brainstorm sessions
**Mode**: Full (default — all phases)
**DateTime**: 20260227-0036
**Slug**: enhance-po-brainstorm-20260227-0036

---

## Discovery Answers

**Requirements / Success Criteria**
Both more ideas AND stronger challenge. A better session produces: (1) a higher volume of diverse ideas that don't cluster around the same few angles, AND (2) challenges that genuinely stress-test assumptions and expose real risks — not just go through the motions.

**Context / Pain Point**
Solo PO with no team. The biggest pain point is no external perspective — AI generates ideas and challenges from a similar angle every time. Missing the cognitive diversity a real team provides: the skeptical CFO, the power user, the regulator, the competitor, the overwhelmed new employee.

**Preferences**
Mix personas AND frameworks — combine role-play simulation of specific stakeholder personas with structured ideation frameworks (Six Thinking Hats, JTBD, TRIZ, etc.) for maximum coverage.

---

## Raw Ideas (25 total)

### Technology Domain
1. Multi-Persona Council — AI role-plays 5–7 named stakeholder personas simultaneously; each generates ideas AND challenges from their unique POV
2. Six Thinking Hats Pass — structured ideation layer using de Bono's 6 hats before clustering
3. Socratic Depth Protocol — after each cluster, agent enters Socratic mode; refuses to accept any answer without demanding evidence, 3–5 levels deep
4. Steelman Protocol — build strongest possible case FOR each idea before critiquing; prevents premature dismissal
5. Question Storming Mode — generate 50+ questions about the problem before any solutions
6. Constraint Ladder — progressively remove constraints (budget, timeline, regulation, team size) and generate what ideas emerge

### UX / User Domain
7. Empathy Map per Persona — for each simulated persona: what they think/feel/say/do/hear/see
8. User Journey Inversion — trace worst possible user journey through a feature to surface design failures
9. Jobs-to-be-Done Lens — reframe every idea as JTBD: functional/emotional/social jobs

### Business Model Domain
10. Red Team / Blue Team — two parallel AI tracks: one defends, one attacks each idea
11. Futures Cone — ideas across 4 futures: Probable / Plausible / Possible / Preposterous
12. Competitive Backstab Analysis — "If a top competitor launched this, what would they do differently to beat us?"

### Edge Cases / Failure Domain
13. Negative Brainstorming / Inversion — "How would we make this product fail?" then invert
14. Second-Order Consequences — chain: "If X → users do Y → competitors respond Z → market shifts W"
15. First Principles Decomposition — break to atomic truths, discard assumptions, rebuild solutions

### Operations Domain
16. Time Horizon Matrix — Quick Win (1mo) / Strategic (6mo) / Transformative (2yr) × effort
17. Assumption Ladder — Data → Interpretation → Assumption → Belief → Identity; challenge at each rung

### Security / Compliance / Risk Domain
18. Regulatory Pre-Mortem — "Which specific regulation kills this in 18 months?"
19. Anti-Pattern Library — check if ideas inadvertently implement known failure patterns
20. Stakeholder Impact Map — map affected stakeholders before challenge; challenge from each perspective

### Meta / Reflection Domain
21. Provocateur Mode — AI takes extreme position ("This feature should not exist") and argues persistently
22. Zettelkasten Idea Linking — connect each surviving idea to existing ADRs, past brainstorm outputs
23. Solo PO Reflection Protocol — "What did you defend too quickly? What did you dismiss too quickly?"
24. TRIZ Inventive Principles — apply contradiction-resolution; identify conflict, apply one of 40 principles
25. Idea Genealogy Tracking — track how each surviving idea mutated through challenge phases

---

## Clusters

### Cluster A — Multi-Persona & Role Simulation ⭐ SELECTED
**Ideas**: 1, 7, 10, 21, 20
**Scores**: Novelty 5 / Feasibility 4 / Impact 5 = **14/15**
**Theme**: Simulate team cognitive diversity for a solo PO — give the AI specific named personas (CFO, Power User, Regulator, Competitor, New Employee) that generate ideas AND challenges from their POV. Key techniques: Multi-Persona Council, Empathy Map per Persona, Red Team/Blue Team, Provocateur Mode, Stakeholder Impact Map.
**Why selected**: Directly addresses the #1 pain point (no external perspective).

### Cluster B — Structured Ideation Frameworks
**Ideas**: 2, 5, 9, 24, 13, 15
**Scores**: Novelty 3 / Feasibility 5 / Impact 4 = **12/15**
**Theme**: Layer in additional structured frameworks (Six Hats, JTBD, TRIZ, Question Storming, Negative Brainstorming) to supplement SCAMPER and HMW for more idea volume and diversity.
**Not selected for deep research** (lower novelty; many frameworks can be added incrementally).

### Cluster C — Challenge Depth & Rigor ⭐ SELECTED
**Ideas**: 3, 4, 17, 18, 19
**Scores**: Novelty 4 / Feasibility 5 / Impact 5 = **14/15**
**Theme**: Make challenges harder and more rigorous — Socratic Protocol, Steelman Protocol, Assumption Ladder, Regulatory Pre-Mortem, Anti-Pattern Library. Forces the solo PO to earn their convictions rather than sliding through soft critique.
**Why selected**: Directly addresses challenge rigidity; builds on existing challenge infrastructure.

### Cluster D — Strategic Perspective Expansion
**Ideas**: 11, 12, 14, 16, 6
**Scores**: Novelty 4 / Feasibility 3 / Impact 4 = **11/15**
**Theme**: Long-horizon thinking — Futures Cone, Competitive Backstab, Second-Order Consequences, Time Horizon Matrix, Constraint Ladder.
**Not selected** (highest implementation complexity; can be added later).

### Cluster E — Meta-Reflection & Session Learning
**Ideas**: 21, 22, 23, 25, 8
**Scores**: Novelty 5 / Feasibility 4 / Impact 3 = **12/15**
**Theme**: Compound learning across sessions — Solo PO Reflection Protocol, Zettelkasten Linking, Idea Genealogy.
**Not selected for deep research** (lower immediate session impact; good for future iteration).

---

## Confirmed Clusters for Deep Research
- **Cluster A**: Multi-Persona & Role Simulation
- **Cluster C**: Challenge Depth & Rigor

---

## Research Instructions for Analyzer

The analyzer should run Phases 5-8 on Clusters A and C:

**Phase 5 — Deep Research**:
- Investigate best practices for AI persona simulation in product management contexts
- Research Six Thinking Hats, Steelman argumentation, Socratic questioning, Assumption Ladder, Anti-Pattern libraries in product/software contexts
- Look at how existing AI brainstorm tools (ChatGPT, Claude Projects, Notion AI) handle multi-persona simulation
- Review existing feature-brainstormer.md at `.claude/agents/feature-brainstormer.md` and po-brainstorm SKILL.md for integration points

**Phase 6 — Decision Matrix**:
- Compare implementation approaches: (a) add personas to existing challenge phase, (b) create new pre-ideation persona layer, (c) create standalone `persona-simulator` sub-agent
- Compare challenge enhancement approaches: (a) add Steelman + Socratic inline to existing phases, (b) create separate challenge sub-phases, (c) create a new `--deep` mode flag

**Phase 7 — Visual Architecture**:
- Draw the enhanced brainstorm workflow showing where personas inject and where new challenge sub-phases fit in the existing 7-step workflow

**Phase 8 — Adversarial Debate**:
- Challenge: "Does adding more structure to brainstorming actually produce better outcomes or just more output?"
- Challenge: "Will persona simulation feel like role-play theater that adds noise rather than signal?"
- Challenge: "Is the Socratic depth protocol useful or will it just frustrate users by blocking flow?"

**Output**: Write results to `docs/brainstorms/enhance-po-brainstorm-20260227-0036/brainstorm-results.md`
