---
name: prioritization-engine
description: Analyze and prioritize features using frameworks like RICE, MoSCoW, WSJF, Value vs Effort matrix, Kano model, and Cost of Delay. Provides data-driven prioritization with dependency analysis. Use when asked to "prioritize these features", "what should we build next", "apply RICE scoring", "recommend sprint backlog", "rank by value", or "dependency-aware roadmap".
---

# Prioritization Engine

## Core Capabilities

### Prioritization Frameworks
- **RICE Scoring**: Reach × Impact × Confidence / Effort
- **MoSCoW**: Must have, Should have, Could have, Won't have
- **WSJF**: Weighted Shortest Job First (SAFe framework)
- **Value vs Effort Matrix**: 2×2 prioritization grid
- **Kano Model**: Categorize features by customer satisfaction
- **Cost of Delay**: Calculate economic impact of delays

### Multi-Criteria Analysis
- Business value assessment
- Technical complexity evaluation
- Strategic alignment scoring
- Risk assessment
- Customer impact analysis
- Resource requirements
- Time-to-market considerations

### Dependency-Aware Prioritization
- Identify technical dependencies
- Consider prerequisite features
- Account for blocking relationships
- Suggest optimal sequencing
- Critical path analysis

## Output Examples

### RICE Scoring Result

```markdown
## Prioritization Results: RICE Framework

### Methodology
- **Reach**: Users affected per quarter
- **Impact**: 0.25=minimal, 0.5=low, 1=medium, 2=high, 3=massive
- **Confidence**: 50%=low, 80%=medium, 100%=high
- **Effort**: Person-months required

### Ranked Features

**1. FEAT-001: Auto Tag Placement**
- Reach: 5,000 users/quarter
- Impact: 3 (massive - key differentiator)
- Confidence: 80%
- Effort: 3 person-months
- **RICE Score: 4,000**
- **Rationale**: High-impact differentiator, strong market demand

**2. FEAT-003: Bulk Upload**
- Reach: 2,000 users/quarter
- Impact: 2 (high - efficiency gain)
- Confidence: 100%
- Effort: 1 person-month
- **RICE Score: 4,000**
- **Rationale**: Quick win, high user demand

### Recommendations

**Immediate (Next Sprint)**:
- FEAT-003: Bulk Upload (quick win)

**Short-term (Q1 2026)**:
- FEAT-001: Auto Tag Placement (strategic investment)

### Trade-off Analysis
- **Quick Wins**: FEAT-003 delivers high value with low effort
- **Strategic Bets**: FEAT-001 requires investment but creates differentiation
```

### Value vs Effort Matrix

```
High Value, Low Effort (DO FIRST)     | High Value, High Effort (STRATEGIC)
  ✓ FEAT-003: Bulk Upload             |   ✓ FEAT-001: Auto Tag Placement
  ✓ FEAT-005: Email Notifications     |   ○ FEAT-002: Mobile App
--------------------------------------|---------------------------------------
Low Value, Low Effort (FILL-IN)      | Low Value, High Effort (AVOID)
  ○ FEAT-009: UI Theme Customization  |   ✗ FEAT-010: Legacy Format Support
```

### Dependency-Aware Roadmap

```markdown
## Recommended Development Sequence

### Phase 1: Foundation (Sprint 1-2)
- FEAT-004: Document Upload API
  - **Why First**: Required by FEAT-001, FEAT-003
  - **Risk**: None, well-understood
  - **Dependencies**: None

### Phase 2: Quick Wins (Sprint 3-4)
- FEAT-003: Bulk Upload
  - **Why Now**: Depends on FEAT-004, high RICE score
  - **Risk**: Low
  - **Dependencies**: FEAT-004 ✓

### Phase 3: Strategic Investment (Sprint 5-8)
- FEAT-001: Auto Tag Placement
  - **Why Now**: Foundation ready, differentiator
  - **Risk**: Medium (ML complexity)
  - **Dependencies**: FEAT-004 ✓

### Blocked Items (Need Resolution)
- FEAT-006: Integration with DocuSign
  - **Blocker**: API contract negotiation pending
  - **Action**: Escalate to partnerships team
```

## Domain-Specific Considerations

### eSign Product Priorities

```markdown
### Compliance-Driven Priorities
**Must Have:**
- eIDAS/ESIGN compliance features (legal requirement)
- Audit trail completeness
- Data retention capabilities
- Certificate management

**High Priority:**
- Security enhancements
- Performance at scale
- Integration capabilities

**Lower Priority (unless customer-driven):**
- UI customizations
- Advanced reporting
- Workflow automation (beyond core)
```

## Reference Files

For detailed framework documentation, see:
- **[frameworks.md](references/frameworks.md)**: Complete details on RICE, WSJF, MoSCoW, Value vs Effort Matrix, Kano Model, Cost of Delay, dependency analysis, and multi-criteria decision making

## Integration with Other Agents

### Input from Requirements Analyst
- Business value statements
- Complexity indicators
- Strategic importance

### Input from Backlog Manager
- Story point estimates
- Dependency graphs
- Technical debt indicators

### Output to Sprint Planner
- Prioritized backlog
- Recommended sprint composition
- Sequencing suggestions

## Monitoring Metrics

### Prioritization Accuracy
- Features delivered vs. planned priority
- Business impact vs. predicted impact
- Customer satisfaction with releases
- Strategy alignment score

### Decision Quality
- Stakeholder agreement rate
- Priority change frequency
- Delivered value vs. effort spent
