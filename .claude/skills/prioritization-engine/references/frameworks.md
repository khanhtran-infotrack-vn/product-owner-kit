# Prioritization Frameworks Reference

## RICE Framework

### Formula
```
RICE Score = (Reach × Impact × Confidence) / Effort
```

### Components

#### Reach
Number of users affected per time period (typically per quarter)
- Small: <500 users
- Medium: 500-2,000 users
- Large: 2,000-10,000 users
- Very Large: >10,000 users

#### Impact
Value impact per user
- 0.25 = Minimal impact
- 0.5 = Low impact
- 1 = Medium impact
- 2 = High impact
- 3 = Massive impact

#### Confidence
Data quality confidence percentage
- 50% = Low confidence (limited data, many assumptions)
- 80% = Medium confidence (some data, reasonable estimates)
- 100% = High confidence (strong data, validated estimates)

#### Effort
Person-months required
- XS: 0.5 month
- S: 1 month
- M: 3 months
- L: 6 months
- XL: 12 months

### Example Calculation

```
Feature: Auto Tag Placement
- Reach: 5,000 users/quarter
- Impact: 3 (massive - key differentiator)
- Confidence: 80%
- Effort: 3 person-months

RICE Score = (5,000 × 3 × 0.80) / 3 = 4,000
```

## WSJF (Weighted Shortest Job First) - SAFe Framework

### Formula
```
WSJF = Cost of Delay / Job Duration
```

### Cost of Delay Components
Score each component 1-10:

#### User/Business Value
- Revenue impact
- Customer satisfaction impact
- Market positioning
- Strategic alignment

#### Time Criticality
- Deadline pressure
- Market window
- Regulatory requirements
- Dependencies on other work

#### Risk Reduction/Opportunity Enablement
- Technical risk mitigation
- Compliance risk reduction
- Business opportunity creation
- Technical debt reduction

### Job Duration
Relative effort estimate (1-10, Fibonacci sequence preferred)

### Example

```
Feature: Compliance Update
- User/Business Value: 7
- Time Criticality: 10 (regulatory deadline)
- Risk Reduction: 9 (legal risk)
- Cost of Delay: 7 + 10 + 9 = 26

Job Duration: 3

WSJF Score = 26 / 3 = 8.67
```

## MoSCoW Method

### Must Have
- Non-negotiable for release
- Legal/compliance requirements
- Core functionality without which product fails
- Critical bug fixes affecting majority of users
- Features without which product has no value

### Should Have
- Important but not critical
- Significant value to users
- Can be deferred if capacity constraints
- Workarounds exist but are painful
- Strongly desired by stakeholders

### Could Have
- Nice to have improvements
- Minor enhancements
- Low impact if missing
- Easy to cut from scope
- Desirable but not necessary

### Won't Have (This Time)
- Out of scope for current release
- Future consideration
- Not aligned with current goals
- Resource constraints prevent inclusion
- May be reconsidered in future

## Value vs Effort Matrix (2x2)

### Quadrants

```
High Value, Low Effort (DO FIRST - Quick Wins)
- Highest priority
- Fast ROI
- Build momentum
- Examples: UI improvements, minor features with big impact

High Value, High Effort (STRATEGIC - Major Projects)
- Strategic investments
- Significant planning needed
- Staged delivery recommended
- Examples: Platform migrations, major features

Low Value, Low Effort (FILL-IN - Nice to Have)
- Filler work when capacity available
- Low risk
- Can be postponed easily
- Examples: Minor UI polish, small optimizations

Low Value, High Effort (AVOID - Reconsider)
- Rarely justified
- Re-evaluate the value proposition
- Consider if there's a simpler approach
- Examples: Over-engineered solutions, edge cases
```

## Kano Model

### Feature Categories

#### Basic/Expected
- Customers expect these features
- Absence causes dissatisfaction
- Presence doesn't increase satisfaction
- Example: Search functionality in eSign product

#### Performance/Linear
- Satisfaction increases linearly with quality
- More is better
- Competitive differentiators
- Example: Document processing speed

#### Excitement/Delighters
- Unexpected features
- Absence doesn't cause dissatisfaction
- Presence creates delight and loyalty
- Example: AI-powered auto tag placement

#### Indifferent
- Users don't care either way
- No impact on satisfaction
- Question if these should be built
- Example: Rarely used customization options

#### Reverse
- Some users like it, others dislike it
- Segmentation opportunity
- Example: Highly automated vs manual control

## Cost of Delay

### Calculation
```
Cost of Delay = Revenue Impact + Productivity Loss + Competitive Risk
```

### Components

#### Revenue Impact
- Direct revenue loss per time period
- Customer churn costs
- New customer acquisition delay

#### Productivity Loss
- Internal efficiency impact
- Manual workaround costs
- Support ticket costs

#### Competitive Risk
- Market share loss
- First-mover advantage loss
- Strategic positioning risk

### Example

```
Feature: Mobile App
- Revenue Impact: $50K/month from mobile users
- Productivity Loss: $10K/month (support costs for mobile web issues)
- Competitive Risk: $30K/month (competitors have mobile apps)

Total Cost of Delay: $90K/month

If feature takes 6 months to build, total delay cost = $540K
```

## Dependency-Aware Prioritization

### Dependency Types

#### Technical Dependencies
- Feature A requires Feature B to be built first
- Shared infrastructure needs
- API contracts

#### Business Dependencies
- Marketing campaign tied to feature launch
- Contract commitments
- Regulatory deadlines

#### Resource Dependencies
- Requires specific team member skills
- External vendor availability
- Budget approval timing

### Critical Path Analysis

1. **Identify all dependencies** between features
2. **Calculate longest path** through dependency chain
3. **Prioritize critical path items** to minimize total timeline
4. **Identify parallel work** opportunities

### Example

```
Feature Dependencies:
- Upload API (A) → Auto Tag (B) → User Acceptance UI (C)
- Email Service (D) → Notification System (E)

Critical Path: A → B → C (longest chain)
Can be done in parallel: D → E

Prioritization:
1. Start A and D immediately (no dependencies)
2. B starts after A completes
3. E starts after D completes
4. C starts after B completes
```

## Combining Frameworks

### Multi-Criteria Decision Matrix

Use multiple frameworks for comprehensive prioritization:

```
Feature Evaluation:
1. Calculate RICE score for ROI estimation
2. Apply MoSCoW for release planning
3. Use Value/Effort matrix for quick visual
4. Check Kano model for strategic positioning
5. Factor in dependencies and critical path
```

### Weighted Scoring Example

```
Criteria Weights:
- Business Value: 35%
- Strategic Alignment: 25%
- Customer Impact: 20%
- Technical Risk: 10%
- Effort: 10%

Feature Score = (BV × 0.35) + (SA × 0.25) + (CI × 0.20) - (TR × 0.10) - (E × 0.10)
```
