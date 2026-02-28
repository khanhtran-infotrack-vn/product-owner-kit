# Challenge Techniques Reference

**Purpose**: Expanded templates and question banks for the feature-brainstormer Challenge & Critique phase.
**Note**: All core challenge instructions are inline in the agent file. This reference provides additional depth.

---

## 1. Pre-Mortem Templates

Use these prompts to trigger specific failure scenario categories. Apply to each top idea in turn.

### Market Failure
- "Users did not adopt because the feature did not address the real pain point..."
- "Adoption stalled at [X]% because competing habits were too entrenched..."
- "The market segment we targeted was smaller than projected because..."

### Technical Failure
- "The feature broke in production because the underlying assumption about [system] was wrong..."
- "Performance degraded at scale because we did not account for [factor]..."
- "Integration with [existing component] failed because of [undiscovered dependency]..."

### Business Failure
- "Revenue targets were missed because pricing/packaging did not match user expectations..."
- "The feature increased churn instead of reducing it because it changed a workflow users depended on..."
- "Cost to support the feature exceeded projected revenue because..."

### Competitive Failure
- "A competitor launched a better version 3 months after us because they solved [problem] we overlooked..."
- "We lost market share because our implementation required [friction] that theirs did not..."

---

## 2. Devil's Advocate Question Bank

Use 3-5 questions per idea. Rotate through to avoid repetition across ideas.

### Value Challenges
- "What is the strongest reason NOT to build this?"
- "Which user segment would actively dislike this feature and why?"
- "What existing workflow does this break or complicate?"
- "If this feature were free to build, would we still prioritize it over alternatives?"
- "What is the opportunity cost of building this instead of [top alternative]?"

### Assumption Challenges
- "What assumption are we most confident about — and what if it is wrong?"
- "We are assuming users will [behavior]. What evidence do we have for this?"
- "What would have to be true for this idea to fail despite a perfect execution?"

### Market & Competitive Challenges
- "Why has no competitor built this yet? Is it harder than it looks, or lower value than we think?"
- "What would a well-funded competitor do differently if they saw our roadmap?"
- "Who is the most skeptical buyer persona for this, and what is their strongest objection?"

### Execution Challenges
- "What is the most likely way our team underestimates the complexity here?"
- "Which downstream team (support, ops, legal) has the strongest objection to this?"
- "What does success look like at 10x scale — and does the design hold?"

### Strategic Challenges
- "Does building this make us better at our core, or does it dilute our focus?"
- "In 2 years, will we wish we had built this sooner, or wish we had not built it at all?"

---

## 3. Persona Challenge Profiles

Apply one or more of these personas to stress-test top ideas during Devil's Advocate (4c). Give each persona a voice.

**Full persona profiles** (concerns, objections, decision criteria, empathy maps): see `.claude/agents/references/persona-profiles.md`.

**Quick reference — signature questions per persona:**

| Persona | Signature Objection |
|---------|---------------------|
| Enterprise Buyer | "How does this integrate with our SSO? Who owns the data?" |
| New User | "I do not have time to learn this. What if I make a mistake?" |
| CFO | "What is the measurable ROI? What is the all-in cost?" |
| Competitor Analyst | "This is easy to replicate. What is our 6-month head start?" |
| Support Lead | "This will flood us with tickets. Error messages are not actionable." |
| Power User | "This breaks my expert workflow. Where is the bulk operation?" |
| Regulator | "Which regulation clause does this activate? Where is the audit trail?" |

---

## 4. Constraint Inversion Scenarios

Apply these scenarios to the top 1-3 ideas to test robustness.

### Budget Variations
| Scenario | Question |
|----------|----------|
| 10x budget | "With 10x resources, how does the approach change? Does it unlock a fundamentally better solution?" |
| 1/10th budget | "If we had to build this with 10% of the planned budget, what is the minimal version that still delivers core value?" |
| Zero incremental cost | "If engineering cost were zero, would this still be our top priority? Does the answer reveal anything?" |

### Timeline Variations
| Scenario | Question |
|----------|----------|
| Half the time | "If we had to ship in half the time, what gets cut? Is what remains still valuable?" |
| Double the time | "If we had twice as long, what would we do differently? Does that expose shortcuts in the current plan?" |
| Ship tomorrow | "What is the absolute minimum we could release tomorrow? Would that version embarrass us or delight users?" |

### Team Variations
| Scenario | Question |
|----------|----------|
| Solo developer | "If one engineer had to build this alone, what would they prioritize?" |
| Outsourced | "If an external team built this with our spec, what would they misunderstand?" |
| Full squad (2x normal) | "With 2x the team, does this become a bigger feature, or do we ship faster?" |

### Market Variations
| Scenario | Question |
|----------|----------|
| Monopoly | "If we had no competition, would we still prioritize this? Does competition anxiety drive this decision?" |
| Crowded market | "In a market with 5 strong competitors, does this feature differentiate us or match the table stakes?" |
| New market | "If we were entering this market fresh with no existing customers, would we still build this first?" |

---

## 5. Advanced Elicitation Methods

Use these for high-stakes decisions or strategic exploration sessions.

### Red Team vs Blue Team
**Format**: Split into two perspectives for the same idea.
- **Red Team**: Attacks the proposal. Goal: find every flaw, risk, and failure mode.
- **Blue Team**: Defends and strengthens the proposal. Goal: counter the red team's objections with evidence or mitigations.
- **Outcome**: Document which red team objections survived the blue team defense — these are real risks.

### Shark Tank Pitch
**Format**: Present the top idea as if pitching to a panel of skeptical investors.
- State the problem and market size
- Present the solution and differentiation
- Show the business model and revenue potential
- Anticipate: "Why will you win?" / "Why now?" / "What is the risk?"
- **Outcome**: Surfaces gaps in the value proposition and market justification.

### Thesis Defense
**Format**: Treat the recommendation as a thesis that must withstand expert examination.
- Present: "Our recommendation is [idea] because [reasoning]."
- Panel challenge: Three rounds of objections from different stakeholder perspectives.
- Response: Defend each objection with evidence or acknowledge the limitation.
- **Outcome**: Forces explicit justification for every key assumption. Undefendable positions become visible.

---

## 6. Deep Challenge Techniques (activated by `--deep` flag)

These techniques run after the standard 6 sub-phases (4a-4f), on the **top 3 ideas only** to manage context. See `feature-brainstormer.md` for the workflow trigger.

### 4g: Steelman Protocol

Build the strongest possible case FOR each top idea, incorporating what survived the standard challenge (4a-4f).

**Purpose**: Prevents premature dismissal after adversarial challenge. Forces explicit articulation of the best case after scrutiny. Reduces confirmation bias going into the deeper challenge sub-phases.

**Process**:
1. "Assume this idea succeeds completely. What did we get right?"
2. Articulate the 3 strongest arguments for building this idea, using surviving challenge findings as support.
3. Identify the scenario under which this idea would be transformative.
4. Document the steel-manned version in the challenge findings.

**Note**: The steel-manned version becomes the benchmark for the remaining deep challenges (4h-4k). If those sub-phases cannot defeat the steel-man, the objections are weak.

---

### 4h: Socratic Depth Protocol

Ask progressively deeper questions to expose unstated assumptions. Default: 2 levels. Maximum under `--deep`: 5 levels.

**Tone**: Collaborative curiosity — not interrogation. "What data most strongly supports this?" not "Prove it or I reject it."

**Escape valve**: If the user says "I accept this risk" or "moving on," the protocol ends immediately and documents the depth reached.

**Question progression (per surviving idea)** — ask up to 5 levels:
- Level 1: "What is the key claim this idea depends on?"
- Level 2: "What evidence supports that claim? How strong is it?"
- Level 3: "If that evidence were wrong, what else changes?"
- Level 4: "What assumption underlies even that evidence?"
- Level 5: "What would falsify this idea entirely?"

Document: the depth reached, the weakest link exposed, and whether the idea survived.

---

### 4i: Assumption Ladder

Walk each top idea through the Ladder of Inference (Argyris/Senge). Challenge at every rung.

**Rungs** (bottom to top):
1. **Data observed**: What facts do we actually have? (not interpretations)
2. **Data selected**: Which data did we choose to focus on? What did we ignore?
3. **Interpreted as**: What meaning did we assign to that data?
4. **Assumed**: What did we take for granted without checking?
5. **Concluded**: What decision did we reach from those assumptions?
6. **Believed**: What belief does this conclusion reinforce?
7. **Act on**: What would we do if this belief is correct?

**Challenge prompt**: "At rung [X], we [assumed/interpreted/concluded]. What if that rung is wrong? How does the idea hold up if we descend back to the raw data?"

---

### 4j: Regulatory Pre-Mortem

Surface regulatory, legal, and compliance risks before commitment.

**Core question**: "Which specific regulation, standard, or compliance requirement could block, delay, or kill this feature in the next 18 months?"

**Probe by domain**:
- **Data privacy**: GDPR, CCPA, data residency laws — does this feature touch personal data?
- **Industry regulation**: eIDAS, HIPAA, PCI-DSS, SOC 2, 21 CFR Part 11 — which apply?
- **Accessibility**: WCAG 2.1 AA, ADA, Section 508 — does this create new a11y obligations?
- **Export / jurisdiction**: Does this feature behave differently in EU, US, APAC regulatory regimes?
- **Contractual**: Do existing enterprise contracts restrict this capability?

**Output**: Regulatory risk table — Regulation | Applicability (High/Med/Low) | If violated: | Mitigation

---

### 4k: Anti-Pattern Check

Compare top ideas against a catalog of known product management failure patterns.

**Core prompt**: "Does this idea implement a known anti-pattern? Be specific."

**Anti-pattern catalog**:

| Anti-Pattern | Description | Warning Sign |
|---|---|---|
| **Build Trap** | Measuring success by features shipped, not outcomes delivered | "We need to build this to show progress" |
| **Feature Parity** | Building features only because competitors have them | "They have it, so we need it too" |
| **Premature Scaling** | Designing for 10x users before achieving 1x | Architecture decisions driven by hypothetical scale |
| **Solution-First Thinking** | Starting with a solution before validating the problem | "We have this technology, let's find a use for it" |
| **Scope Creep Metamorphosis** | Each new capability creates complexity outweighing its value | The feature needs 3 other features to work |
| **Complexity Escalator** | Each release requires more user knowledge than the last | Power users love it; new users are lost |
| **Notification Overload** | Adding value through interruption | "Users need to know about this" |
| **Dark Pattern Pressure** | Driving metrics through friction, not genuine value | Engagement metrics rise but satisfaction drops |

**Process**: For each top idea, check: does it match any pattern? If yes, document it. If the anti-pattern is unavoidable, document the mitigation.
