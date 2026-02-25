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

Apply one or more of these personas to stress-test top ideas. Give each persona a voice.

### The Skeptical Enterprise Buyer
**Background**: IT Director or procurement lead at a mid-large organization.
**Concerns**: Security compliance, integration with existing systems, vendor lock-in, data sovereignty.
**Signature objections**:
- "How does this integrate with our SSO / SIEM / existing workflow tools?"
- "Who owns the data, and where is it stored?"
- "What is the audit trail for regulatory compliance?"
- "What happens to our data if we stop using this product?"

### The Overwhelmed New User
**Background**: First-time user, low technical sophistication, high task pressure.
**Concerns**: Learning curve, cognitive overload, fear of making mistakes.
**Signature objections**:
- "I do not have time to learn a new workflow."
- "What happens if I do it wrong? Can I undo it?"
- "Why is there no simple guided path?"

### The Cost-Conscious CFO
**Background**: Finance executive focused on ROI and total cost of ownership.
**Concerns**: Incremental licensing cost, implementation/migration cost, opportunity cost.
**Signature objections**:
- "What is the measurable ROI and over what time horizon?"
- "What is the total cost including implementation, training, and support?"
- "What is the downside risk if this does not deliver the projected value?"

### The Competitor Analyst
**Background**: Rival PM or strategy team monitoring the market.
**Concerns**: Differentiation gaps, copying, response strategy.
**Perspective**:
- "This is easy to replicate. What is our 6-month head start advantage?"
- "Their approach has this weakness we can exploit..."
- "If we launched this, how would they respond within 90 days?"

### The Support Team Lead
**Background**: Head of customer support, responsible for ticket volume and team capacity.
**Concerns**: Edge cases that generate support tickets, complexity in explaining to users.
**Signature objections**:
- "This will generate a flood of 'how do I...' tickets because..."
- "The error messages are not actionable — users will call us when it fails."
- "We do not have documentation or training for this yet."

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
