---
name: po-risk-radar
description: "Proactive PO blind spot detector. Scans all product documentation (brainstorm/, backlog/, requirements/, roadmap/, product_documents/) and identifies which strategic concern domains are NOT covered — surfacing unknown unknowns for the Product Owner. Use when asked to 'find my blind spots', 'what am I not thinking about', 'run a risk radar', 'what domains are uncovered', 'find gaps in my product strategy', or 'what risks am I missing'."
---

# PO Risk Radar

## Purpose

Surface what you don't know you don't know.

This skill scans all documented product artifacts and maps coverage against a
comprehensive taxonomy of PO concern domains. Any domain with no coverage is a
potential blind spot — something you haven't thought to brainstorm or document yet.

---

## Invocation

```
/po-risk-radar
/po-risk-radar [optional focus area, e.g. "compliance" or "user experience"]
```

---

## How to Run the Radar (Instruction for Claude)

When this skill is invoked, Claude should execute the following steps directly
in the main conversation (Claude has file access in the main context):

### Step 1: Scan All Product Directories

Search these directories for all `.md` files and read their content or headings:
- `product_documents/`
- `brainstorm/` (all SUMMARY.md and IDEAS.md files)
- `backlog/` (all US-*.md and README.md files)
- `requirements/`
- `roadmap/`
- `docs/decisions/`
- `docs/assumptions/`

### Step 2: Map Coverage Against the Domain Taxonomy

For each domain below, determine if the scanned content contains **meaningful
coverage** (at least one idea, story, requirement, or decision mentioning it).

Mark each domain as:
- ✅ **Covered** — documented in at least one artifact
- ⚠️ **Partial** — mentioned briefly but not explored or documented
- ❌ **Missing** — no coverage found in any artifact

### Step 3: Report Blind Spots

Output:
1. **Coverage Map** — table of all domains with status
2. **Top 3-5 Blind Spots** — the most critical uncovered domains with severity
3. **Suggested Next Steps** — for each blind spot, a ready-to-use `/po-brainstorm` command

---

## Domain Taxonomy

A complete PO should have at least considered each of these domains.
Gaps are blind spots — not necessarily problems, but worth examining.

### Tier 1 — Core Product Domains (Critical to address)

| Domain | What to look for |
|--------|-----------------|
| **User Personas & Segments** | Who are our users? Are multiple segments considered? |
| **Core User Journey** | What does a user do from sign-up to value delivery? |
| **Onboarding & Adoption** | How do new users discover and adopt features? |
| **User Pain Points** | What problems are we solving? Are they documented? |
| **Competitive Differentiation** | What makes us different? Is this in the roadmap? |
| **Pricing & Monetization** | How does the product generate value/revenue? |
| **Key Success Metrics (KPIs)** | How do we measure if the product is working? |

### Tier 2 — Risk & Compliance Domains (High consequence if missed)

| Domain | What to look for |
|--------|-----------------|
| **Security & Data Privacy** | Authentication, authorization, data handling, GDPR |
| **Regulatory Compliance** | Industry-specific regulations (eIDAS, HIPAA, SOC2, etc.) |
| **Audit & Traceability** | Are actions logged? Can we reconstruct what happened? |
| **Data Governance** | Who owns data? Retention policies? Right to deletion? |
| **Error Handling & Edge Cases** | What happens when things go wrong? |
| **Business Continuity** | What if our service goes down? Data backup? |

### Tier 3 — Scale & Operations Domains (Becomes critical at growth)

| Domain | What to look for |
|--------|-----------------|
| **Performance & Scalability** | Can the system handle growth? Response time goals? |
| **Internationalization (i18n)** | Multiple languages? Time zones? Currency? |
| **Accessibility (a11y)** | Does the product work for users with disabilities? |
| **Support & Operations Burden** | How does this feature affect customer support? |
| **Technical Debt** | Are there known areas that need rework? |
| **Integrations & APIs** | What external systems must we connect to? |

### Tier 4 — Strategic & Future Domains (For longer-term vision)

| Domain | What to look for |
|--------|-----------------|
| **Market Trends & Future Opportunities** | What's changing in the market? |
| **Customer Retention & Churn** | Why do users leave? What keeps them? |
| **Developer/Partner Ecosystem** | APIs for partners? Third-party integrations? |
| **Mobile & Cross-Platform** | Is the experience consistent across devices? |
| **AI & Automation Opportunities** | Where could AI reduce friction or add value? |
| **Stakeholder Alignment** | Are all stakeholder groups represented in the backlog? |

---

## Output Format

### Coverage Map

```markdown
## Risk Radar — Coverage Map

Scanned: [N] files across [N] directories
Date: [YYYY-MM-DD]

### Tier 1 — Core Product Domains
| Domain | Status | Evidence |
|--------|--------|---------|
| User Personas & Segments | ✅ Covered | product_documents/product-vision.md |
| Core User Journey | ❌ Missing | Not found in any artifact |
| Onboarding & Adoption | ⚠️ Partial | Mentioned in brainstorm/X but not documented |
| ... | | |

### Tier 2 — Risk & Compliance Domains
| Domain | Status | Evidence |
|--------|--------|---------|
| Security & Data Privacy | ❌ Missing | Not found |
| Regulatory Compliance | ✅ Covered | esign-domain-expert skill + brainstorm/Y |
| ... | | |

[Repeat for Tier 3 and Tier 4]
```

### Top Blind Spots

```markdown
## Top [N] Blind Spots Requiring Attention

### 🔴 CRITICAL: [Domain Name]
**Why critical**: [1 sentence on risk if ignored]
**Suggested action**:
> /po-brainstorm [specific topic for this domain]

### 🟡 HIGH: [Domain Name]
**Why high**: [1 sentence on risk if ignored]
**Suggested action**:
> /po-brainstorm [specific topic for this domain]

[Repeat for each blind spot, ordered by severity]
```

### Summary

```markdown
## Radar Summary

- Total domains evaluated: [N]
- Covered: [N] (✅)
- Partial: [N] (⚠️)
- Missing: [N] (❌)
- Coverage score: [N]%

**Most urgent blind spot**: [Domain]
**Recommended first action**: /po-brainstorm [topic]
```

---

## Severity Rating Guide

Rate each missing domain:

| Severity | Criteria |
|---------|---------|
| 🔴 CRITICAL | Directly affects legal compliance, security, or core user value |
| 🟡 HIGH | Significantly affects user experience or business outcomes |
| 🟠 MEDIUM | Important for scale or retention but not immediately blocking |
| 🟢 LOW | Strategic or future-facing; worth tracking but not urgent |

---

## Optional: Save Radar Report

After running the radar, optionally save the output:
```
docs/risk-radar-YYYY-MM-DD.md
```

This allows you to track coverage improvement over time and compare radar scans
across sprints.

---

## Tips for Using the Radar

1. **Run at the start of each quarter** — before roadmap planning to ensure no domains are neglected
2. **Run before a new feature brainstorm** — to give context on which domains need attention
3. **Run after a major pivot** — to check if existing artifacts still reflect the new direction
4. **Don't try to cover everything at once** — pick the top 3 blind spots and brainstorm one per sprint

---

## Integration with Other Skills

After the radar identifies blind spots:

| Blind Spot Domain | Recommended Skill/Agent |
|-------------------|------------------------|
| Any unexplored domain | `/po-brainstorm [domain topic]` |
| Compliance gaps | `esign-domain-expert` skill |
| Missing requirements | `requirements-analyst` skill |
| Unvalidated assumptions | Review `docs/assumptions/` |
| Missing user research | `analytics-insights` skill |
| Backlog gaps | `backlog-manager` skill |
| Strategic gaps | `prioritization-engine` skill |
