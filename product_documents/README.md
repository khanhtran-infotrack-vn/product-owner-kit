# Product Documents Folder

This folder contains all product-related documents that provide context for the Product Owner Orchestration System.

## Purpose

Store your product documents here so that agents (especially @feature-brainstormer) can:
- Understand product context
- Reference requirements and specs
- Stay aligned with product vision
- Generate relevant ideas and recommendations

## Recommended Structure

```
product_documents/
├── vision/
│   ├── product-vision.md
│   ├── strategy.md
│   └── goals-2024.md
│
├── requirements/
│   ├── functional-requirements.md
│   ├── non-functional-requirements.md
│   └── user-needs.md
│
├── specifications/
│   ├── feature-specs/
│   └── technical-specs/
│
├── research/
│   ├── user-interviews/
│   ├── surveys/
│   └── analytics-reports/
│
├── design/
│   ├── wireframes/
│   ├── mockups/
│   └── design-system.md
│
└── reference/
    ├── competitor-analysis.md
    ├── market-research.md
    └── industry-standards.md
```

## How Agents Use This Folder

### @feature-brainstormer
- Reads product context before ideation
- References user needs and pain points
- Ensures ideas align with vision
- Links brainstorming results to relevant docs

### @requirements-analyst
- Validates requirements completeness
- Identifies gaps and conflicts
- Ensures traceability

### @backlog-manager
- Creates user stories from requirements
- References acceptance criteria patterns

### @competitive-intel
- Compares features against market
- Updates competitive analysis

### @documentation-agent
- Creates and updates product docs
- Maintains documentation standards

## Getting Started

1. **Add Your Product Vision**:
   - Create `product_documents/vision/product-vision.md`
   - Include: Mission, vision, target users, value proposition

2. **Document Current Features**:
   - Create `product_documents/specifications/feature-specs/`
   - One file per major feature

3. **Add User Research**:
   - Store interview transcripts, survey results
   - Create `product_documents/research/`

4. **Include Competitive Analysis**:
   - Document competitor features and positioning
   - Create `product_documents/reference/competitor-analysis.md`

## Example: Product Vision Template

```markdown
# Product Vision

## Mission
[Why does this product exist?]

## Vision
[What do we aspire to become?]

## Target Users
- Primary: [Who are main users?]
- Secondary: [Who else benefits?]

## Value Proposition
For [target user] who [need/pain point],
Our product is [product category]
That [key benefit],
Unlike [competitors],
We [unique differentiator].

## Strategic Priorities (2024)
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

## Success Metrics
- [Metric 1]: Target
- [Metric 2]: Target
- [Metric 3]: Target
```

## Best Practices

1. **Keep Documents Updated**: Review and update quarterly
2. **Use Clear Naming**: Descriptive filenames (e.g., `mobile-signature-spec.md`)
3. **Link Between Docs**: Reference related documents
4. **Version Control**: Use Git to track changes
5. **Single Source of Truth**: Avoid duplication

## Next Steps

1. Create your initial product vision document
2. Add current feature specifications
3. Include any user research or feedback
4. Start using @feature-brainstormer with this context!

---

**Need Help?**
- Use @documentation-agent to create product docs
- Use @requirements-analyst to structure requirements
- Use @feature-brainstormer to explore new ideas (it will read these docs!)
