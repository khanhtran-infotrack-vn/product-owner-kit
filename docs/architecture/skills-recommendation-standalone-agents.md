# Skills for Standalone Agents - Recommendation

**Date**: February 6, 2026  
**Purpose**: Analyze which standalone agents (competitive-intel, risk-assessor, roadmap-planner, user-research) would benefit from dedicated skills

---

## Summary Recommendation

### ✅ High Priority: Create Skills (Significant Benefit)
1. **roadmap-planner-skill** - High value, substantial domain knowledge to extract
2. **user-research-skill** - High value, rich methodologies and frameworks

### 🔄 Medium Priority: Create Skills (Moderate Benefit)
3. **risk-assessment-skill** - Moderate value, structured frameworks exist
4. **competitive-intel-skill** - Moderate value, analysis frameworks to document

---

## Detailed Analysis

### 1. Roadmap Planner Agent

**Current State**: 80 lines, includes methodology inline

**Potential Skill Content**:
- ✅ **Now/Next/Later framework** (detailed explanation, examples)
- ✅ **OKR mapping methodology** (how to align initiatives with goals)
- ✅ **Dependency mapping techniques** (critical path analysis, PERT charts)
- ✅ **Forecasting formulas** (velocity-based estimation, confidence intervals)
- ✅ **Scenario planning templates** (what-if analysis structures)
- ✅ **Roadmap visualization formats** (timeline, swimlane, Gantt)
- ✅ **Theme definition frameworks** (strategic themes, initiative grouping)

**Estimated Skill Size**:
- SKILL.md: ~150 lines
- references/frameworks.md: ~200 lines (Now/Next/Later deep dive, OKR examples)
- references/templates.md: ~150 lines (roadmap templates, visualization formats)
- references/forecasting.md: ~100 lines (formulas, examples, confidence calculations)

**Agent Size After Extraction**: ~70 lines (workflow orchestration only)

**Benefit**:
- ⭐⭐⭐⭐⭐ **Very High** - Substantial domain knowledge (frameworks, forecasting, visualization)
- Clear separation: Skill = planning methodologies, Agent = tool orchestration
- Reusable across different roadmap planning contexts

**Recommendation**: ✅ **CREATE SKILL** (High priority)

---

### 2. User Research Agent

**Current State**: 80 lines, includes research methodologies inline

**Potential Skill Content**:
- ✅ **Research methodologies** (thematic coding, sentiment analysis, journey mapping)
- ✅ **Persona templates** (demographics, goals, pain points, behaviors)
- ✅ **Interview guide templates** (question frameworks, probing techniques)
- ✅ **Survey design principles** (question types, bias avoidance, analysis)
- ✅ **Sentiment analysis frameworks** (categorization, scoring, interpretation)
- ✅ **Journey mapping techniques** (stages, touchpoints, pain points, emotions)
- ✅ **Research synthesis frameworks** (affinity mapping, insight generation)
- ✅ **Sample research artifacts** (example personas, journey maps, reports)

**Estimated Skill Size**:
- SKILL.md: ~120 lines
- references/methodologies.md: ~250 lines (research techniques, analysis frameworks)
- references/persona-templates.md: ~150 lines (detailed persona examples)
- references/journey-mapping.md: ~150 lines (journey map structures, examples)
- references/research-report-template.md: ~100 lines (standard report structure)

**Agent Size After Extraction**: ~65 lines (workflow orchestration only)

**Benefit**:
- ⭐⭐⭐⭐⭐ **Very High** - Rich domain knowledge (methodologies, templates, frameworks)
- Clear separation: Skill = research expertise, Agent = data aggregation and tool use
- Reusable for different research contexts (discovery, validation, feedback analysis)

**Recommendation**: ✅ **CREATE SKILL** (High priority)

---

### 3. Risk Assessor Agent

**Current State**: 85 lines, includes risk frameworks inline

**Potential Skill Content**:
- ✅ **Risk scoring formulas** (Probability × Impact calculations)
- ✅ **Risk categories taxonomy** (Technical, Dependency, Scope, Resource, Security, Timeline)
- ✅ **Risk severity levels** (Critical/High/Medium/Low definitions)
- ✅ **Mitigation strategy templates** (Avoid, Mitigate, Transfer, Accept)
- ✅ **Risk matrix visualization** (heatmap format)
- ✅ **Common risk indicators** (red flags to watch for)
- ✅ **Technical debt assessment frameworks** (SQALE, CodeScene)

**Estimated Skill Size**:
- SKILL.md: ~100 lines
- references/frameworks.md: ~150 lines (scoring, categorization, mitigation)
- references/risk-indicators.md: ~100 lines (common risks by category)
- references/technical-debt.md: ~100 lines (debt assessment methodologies)

**Agent Size After Extraction**: ~70 lines (workflow orchestration only)

**Benefit**:
- ⭐⭐⭐⭐ **High** - Structured domain knowledge (scoring, categorization, mitigation)
- Moderate separation: Skill = risk frameworks, Agent = risk identification and tool use
- Somewhat reusable (risk concepts apply broadly)

**Recommendation**: 🔄 **CONSIDER SKILL** (Medium priority)
- Worth creating if you want standardized risk assessment across teams
- Can defer if agent size is acceptable (85 lines is manageable)

---

### 4. Competitive Intelligence Agent

**Current State**: 80 lines, includes analysis frameworks inline

**Potential Skill Content**:
- ✅ **SWOT analysis framework** (Strengths, Weaknesses, Opportunities, Threats)
- ✅ **Porter's Five Forces** (competitive rivalry, supplier power, buyer power, substitutes, new entrants)
- ✅ **Feature matrix templates** (comparison grid structures)
- ✅ **Positioning frameworks** (perceptual mapping, differentiation strategies)
- ✅ **Market analysis methodologies** (TAM/SAM/SOM, market segmentation)
- ✅ **Competitor tracking templates** (changelog monitoring, feature comparison)

**Estimated Skill Size**:
- SKILL.md: ~100 lines
- references/frameworks.md: ~200 lines (SWOT, Porter's Five Forces, positioning)
- references/templates.md: ~150 lines (feature matrix, competitor profiles)
- references/market-analysis.md: ~100 lines (TAM/SAM/SOM, segmentation)

**Agent Size After Extraction**: ~70 lines (workflow orchestration only)

**Benefit**:
- ⭐⭐⭐⭐ **High** - Established business frameworks (SWOT, Porter's)
- Moderate separation: Skill = business strategy frameworks, Agent = data collection and analysis
- Somewhat reusable (competitive analysis frameworks are standard)

**Recommendation**: 🔄 **CONSIDER SKILL** (Medium priority)
- Worth creating if you want to document strategic analysis frameworks
- Can defer if agent inline documentation is sufficient

---

## Implementation Priority

### Phase 1 (High Priority) - Implement First
1. **roadmap-planner-skill**
   - Reason: Richest domain knowledge, clear separation, high reusability
   - Timeline: 2-3 hours to create skill and extract from agent
   - Impact: Significantly cleaner agent, reusable planning frameworks

2. **user-research-skill**
   - Reason: Rich methodologies, clear templates, high value
   - Timeline: 2-3 hours to create skill and extract from agent
   - Impact: Agent focuses on data aggregation, skill provides research expertise

### Phase 2 (Medium Priority) - Implement If Needed
3. **risk-assessment-skill**
   - Reason: Structured frameworks, moderate benefit
   - Timeline: 1-2 hours to create skill and extract from agent
   - Impact: Standardizes risk assessment across teams

4. **competitive-intel-skill**
   - Reason: Established business frameworks, moderate benefit
   - Timeline: 1-2 hours to create skill and extract from agent
   - Impact: Documents strategic analysis methodologies

---

## Implementation Plan for Phase 1

### Step 1: Create roadmap-planner-skill

**1.1 Create Skill Structure**
```bash
mkdir -p skills/roadmap-planner/references
```

**1.2 Create SKILL.md**
```yaml
---
name: roadmap-planner
description: Strategic product roadmap planning, Now/Next/Later framework, OKR alignment, dependency mapping, timeline forecasting, scenario analysis
---

# Roadmap Planning Skill

[Core concepts: Now/Next/Later, OKR mapping, forecasting]
```

**1.3 Create Reference Files**
```
references/
├── frameworks.md (Now/Next/Later, OKR mapping, theme definition)
├── templates.md (roadmap formats, visualization templates)
├── forecasting.md (velocity-based estimation, confidence intervals)
└── examples.md (sample roadmaps for different scenarios)
```

**1.4 Extract from Agent**
- Move domain knowledge to skill
- Keep workflow orchestration in agent
- Add `skills: [roadmap-planner]` to agent frontmatter

**1.5 Validate**
```bash
cd skills/ && ./package_skill.py roadmap-planner
```

---

### Step 2: Create user-research-skill

**2.1 Create Skill Structure**
```bash
mkdir -p skills/user-research/references
```

**2.2 Create SKILL.md**
```yaml
---
name: user-research
description: User research methodologies, thematic coding, sentiment analysis, persona creation, journey mapping, research synthesis, interview techniques
---

# User Research Skill

[Core concepts: research methods, analysis frameworks, persona templates]
```

**2.3 Create Reference Files**
```
references/
├── methodologies.md (thematic coding, sentiment analysis, journey mapping)
├── persona-templates.md (persona structure, examples)
├── journey-mapping.md (journey map techniques, touchpoints, examples)
├── interview-guides.md (question frameworks, probing techniques)
└── research-report-template.md (standard report structure)
```

**2.4 Extract from Agent**
- Move research methodologies to skill
- Keep data aggregation workflow in agent
- Add `skills: [user-research]` to agent frontmatter

**2.5 Validate**
```bash
cd skills/ && ./package_skill.py user-research
```

---

## Benefits of Creating These Skills

### For roadmap-planner-skill:
1. ✅ **Standardization**: Consistent roadmap planning approach across teams
2. ✅ **Education**: New PMs learn Now/Next/Later framework quickly
3. ✅ **Reusability**: Forecasting formulas apply to different products
4. ✅ **Clarity**: Agent focuses on tool orchestration, skill provides strategy

### For user-research-skill:
1. ✅ **Methodology**: Documented research techniques (thematic coding, journey mapping)
2. ✅ **Templates**: Reusable persona and journey map structures
3. ✅ **Quality**: Consistent research standards across projects
4. ✅ **Training**: Helps team learn user research best practices

### For Both:
1. ✅ **Maintainability**: Domain knowledge in one place (skill), easier to update
2. ✅ **Separation of Concerns**: Skills = knowledge, Agents = execution
3. ✅ **Progressive Disclosure**: Start with SKILL.md, dive into references/ as needed
4. ✅ **Scalability**: Easy to add new frameworks/templates without bloating agents

---

## When NOT to Create Skills

### Red Flags (Don't Create Skill If):
- ❌ Agent is already concise (<80 lines) and mostly workflow
- ❌ Domain knowledge is minimal or generic
- ❌ Knowledge is project-specific (not reusable)
- ❌ Duplication doesn't exist (single agent uses this knowledge)
- ❌ Frameworks are obvious (no need to document common sense)

### Example: Feature Brainstormer Agent
- **Why no skill?**: Agent already uses well-known techniques (SCAMPER, HMW)
- **Status**: Agent documents workflow, techniques are self-explanatory
- **Conclusion**: No skill needed (agent size is reasonable)

---

## Next Steps

### If Proceeding with Phase 1:

1. **Create roadmap-planner-skill** (2-3 hours)
   - Set up skill structure
   - Extract Now/Next/Later framework from agent
   - Create reference files (forecasting, templates)
   - Update agent to reference skill
   - Validate with package_skill.py

2. **Create user-research-skill** (2-3 hours)
   - Set up skill structure
   - Extract research methodologies from agent
   - Create reference files (personas, journey maps, methodologies)
   - Update agent to reference skill
   - Validate with package_skill.py

3. **Test Integration** (1 hour)
   - Invoke agents and verify they reference skills correctly
   - Ensure no functionality is lost
   - Validate progressive disclosure (skill references work)

4. **Document** (30 minutes)
   - Update agent README with new skills
   - Add skills to skills/ folder README
   - Document creation decision in ADR (optional)

### If Deferring:
- Current standalone agents (80-85 lines) are acceptable
- Can create skills later if duplication emerges
- Focus on using the system and gathering real-world feedback

---

## Decision

**Recommendation**: 
- ✅ **CREATE** roadmap-planner-skill and user-research-skill (Phase 1)
- 🔄 **DEFER** risk-assessment-skill and competitive-intel-skill (Phase 2, if needed)

**Rationale**:
- Roadmap and research have the richest domain knowledge (high ROI)
- Risk and competitive analysis are already reasonably concise (lower ROI)
- Focus on high-value skills first, defer others until needed

**Total Effort**: 5-6 hours for Phase 1 (both skills + testing + documentation)

---

## Questions to Consider

1. **Do we have time?** Phase 1 takes 5-6 hours. Is this worth the investment now?
2. **Do we have use cases?** Will multiple teams use these skills, or just one project?
3. **Do we have expertise?** Do we have PMs who can validate roadmap/research methodologies?
4. **What's the priority?** Should we create skills, or focus on using existing agents first?

**If unsure**: Defer skill creation. Use agents for 1-2 weeks, then decide based on real usage patterns.

---

## Conclusion

Creating skills for **roadmap-planner** and **user-research** agents will:
- ✅ Standardize strategic planning and research methodologies
- ✅ Reduce agent size by 15-20 lines each (cleaner, more focused)
- ✅ Improve maintainability (single source of truth for frameworks)
- ✅ Enable progressive disclosure (skill references for deep dives)

However, this is **optional** - the current agents are functional and reasonably sized. The main benefit is **standardization** and **reusability**, not immediate functionality.

**Final Recommendation**: 
- If you want a polished, standardized system → **Create Phase 1 skills now**
- If you want to test the system first → **Defer and revisit after real usage**
