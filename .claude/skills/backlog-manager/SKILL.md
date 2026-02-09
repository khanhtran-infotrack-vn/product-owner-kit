---
name: backlog-manager
description: Manage product backlogs in Agile environments including user story creation, epic breakdown, backlog refinement, and INVEST criteria validation. Integrates with Jira and Azure DevOps. Use when asked to "create user stories", "break down this epic", "is this story ready for sprint", "refine the backlog", "generate acceptance criteria", "validate these stories", "what dependencies exist", or "estimate story points".
---

# Backlog Manager

## Core Capabilities

### User Story Generation
- Create well-formed user stories from requirements
- Apply standard format: "As a [role], I want [goal], so that [benefit]"
- Generate acceptance criteria (Given-When-Then format)
- Add technical notes and implementation hints
- Assign appropriate labels and tags

### Epic Management
- Break down epics into manageable user stories
- Maintain epic-story relationships
- Track epic progress and completion
- Identify epic scope creep
- Suggest epic splitting strategies

### Story Quality Validation (INVEST Criteria)
- **I**ndependent: Can be developed separately
- **N**egotiable: Details can be refined with team
- **V**aluable: Delivers value to users/business
- **E**stimable: Team can estimate effort
- **S**mall: Completable within a sprint
- **T**estable: Clear acceptance criteria

### Backlog Organization
- Categorize stories by theme/initiative
- Assign stories to epics
- Tag stories with labels (bug, feature, tech-debt, spike)
- Identify and manage technical debt items
- Organize by release/version

### Dependency Management
- Detect dependencies between stories
- Identify blocking relationships
- Suggest optimal story sequencing
- Flag circular dependencies
- Create dependency visualization

### Estimation Support
- Suggest story point estimates based on historical data
- Identify stories that are too large (>8 points)
- Compare similar stories for estimation consistency
- Track estimation accuracy over time
- Recommend re-estimation when scope changes

## Project Management Integrations

### Jira Cloud/Server API
- Create/update issues
- Link stories to epics
- Add comments and attachments
- Manage sprints and versions

### Azure DevOps API
- Work item management
- Query work item relations
- Update iteration paths
- Manage area paths

### Linear API
- Issue creation and updates
- Project and cycle management
- Label and priority assignment

## Output Formats

### Backlog Health Report

```markdown
## Backlog Health Report
**Generated**: [Date/Time]
**Total Stories**: [Count]
**Ready for Sprint**: [Count]

### Quality Metrics
- ✓ Stories meeting INVEST criteria: 85% (68/80)
- ⚠ Stories needing refinement: 15% (12/80)
- ⚠ Stories missing acceptance criteria: 5% (4/80)
- ✓ Stories with estimates: 90% (72/80)

### Refinement Needed
**High Priority - Missing Acceptance Criteria:**
- STORY-042: User login via SSO
- STORY-053: PDF rendering optimization

**Medium Priority - Too Large (>8 points):**
- EPIC-005: Complete payment integration (21 points)
  → Recommend splitting into 3-4 stories

### Dependency Analysis
**Blocking Chains Detected:**
- STORY-012 blocks STORY-015, STORY-018, STORY-022 (4 stories)

**Circular Dependencies:**
- None detected ✓

### Recommended Actions
1. Refine 12 stories before next sprint planning
2. Split EPIC-005 into smaller deliverables
3. Add acceptance criteria to 4 high-priority stories
4. Resolve blocking chain starting with STORY-012
```

### Story Quality Validation Example

When validating a vague story like:
```
As a user
I want better performance
So that the app is fast
```

Output:
```markdown
## Story Quality Assessment: FAIL ❌

### INVEST Criteria Analysis
**❌ Valuable**: FAIL - Business value unclear ("better" and "fast" are unmeasurable)
**❌ Estimable**: FAIL - Cannot estimate without specific performance targets
**❌ Testable**: FAIL - No measurable acceptance criteria

### Critical Issues
1. **Vague User Role** - "As a user" is too generic. Specify user type (admin, signer, viewer)
2. **Unmeasurable Goal** - "Better performance" lacks specificity. What aspect? Page load? API response?
3. **No Acceptance Criteria** - Missing Given-When-Then scenarios and performance metrics

### Recommended Improvements

**Option A: Page Load Performance**
```
As a document signer
I want document pages to load in under 2 seconds
So that I can review and sign documents without delays

Acceptance Criteria:
1. Given a PDF document of up to 50 pages
   When I open any page
   Then the page should render in <2 seconds on 4G connection
```

### Questions to Ask Stakeholder
1. Which part of the system needs performance improvement?
2. What is the current performance metric?
3. What is the target performance metric?
```

## Best Practices

### Story Writing Guidelines
1. **Be Specific**: Replace vague terms with measurable criteria
2. **User-Centric**: Focus on user value, not implementation
3. **One Capability**: Each story should deliver one testable feature
4. **Independent**: Minimize dependencies between stories
5. **Sized Right**: Stories should fit in one sprint (1-8 points)

### Epic Decomposition Strategy
1. **Horizontal Slicing**: Break by feature completeness (MVP → enhancements)
2. **Vertical Slicing**: Break by user journey (end-to-end thin slices)
3. **Technical Layers**: Separate infrastructure from features when appropriate
4. **Risk-Based**: Tackle high-risk/high-uncertainty stories early

### Acceptance Criteria Guidelines
1. Use Given-When-Then format consistently
2. Include happy path and key edge cases
3. Make criteria measurable and verifiable
4. Specify error conditions and handling
5. Include non-functional requirements (performance, security)

## Reference Files

For detailed templates and examples, see:
- **[story-templates.md](references/story-templates.md)**: User story, epic breakdown, and eSign domain story templates
- **[epic-breakdown-example.md](references/epic-breakdown-example.md)**: Complete example of epic decomposition with dependencies and sprint allocation

## Integration with Other Agents

### Input from Requirements Analyst
- Structured requirements → User stories
- Acceptance criteria → Story acceptance criteria
- Dependencies → Story dependencies
- Compliance needs → Story constraints

### Output to Prioritization Engine
- Story business value assessments
- Story complexity estimates
- Story dependencies
- Story categorization (feature/bug/tech-debt)

### Output to Sprint Planner
- Ready stories (meeting Definition of Ready)
- Story point estimates
- Dependency information
- Story categorization for sprint balance

## Monitoring Metrics

### Quality Metrics
- **Story Quality Score**: % of stories meeting INVEST criteria
- **Refinement Cycle Time**: Days from creation to "Ready" status
- **Estimation Accuracy**: Actual vs. estimated story points
- **Definition of Ready Compliance**: % meeting DoR checklist
- **Dependency Ratio**: Stories with dependencies / total stories

### Productivity Metrics
- **Stories Created per Week**: Backlog growth rate
- **Stories Refined per Week**: Preparation velocity
- **Epic Completion Rate**: % of epics fully broken down
- **Backlog Age**: Average age of unrefined stories
- **Sprint Readiness**: Stories ready / stories needed for sprint
