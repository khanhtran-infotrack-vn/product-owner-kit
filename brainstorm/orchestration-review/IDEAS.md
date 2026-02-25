# Orchestration Review — All Ideas Generated

**Session**: Orchestration review + PO discovery workflow improvement
**Date**: 2026-02-26
**Source**: Direct codebase audit of `.claude/` folder

---

## Cluster A: Unknown Unknowns Discovery (Critical PO Blind Spot)

| # | Idea | Notes |
|---|------|-------|
| A1 | **Proactive Risk Radar Agent** — scans brainstorm/, backlog/, requirements/ and surfaces domains NOT yet covered | New agent needed |
| A2 | **Weekly PO Health Check Prompt** — "What domains haven't you brainstormed about this sprint?" checklist | Skill or prompt template |
| A3 | **Blind Spot Detector** — after each brainstorm, auto-runs esign-domain-expert compliance/regulatory lenses on top ideas | Extend feature-brainstormer |
| A4 | **Competitor Gap Analysis Workflow** — compares documented features against common industry patterns | Needs competitive_intel/ directory |
| A5 | **User Journey Audit** — walks through typical flows step-by-step and asks "what could go wrong at each step?" | New skill or prompt |
| A6 | **5 Whys Auto-Trigger** — when creating a user story, auto-run 5 Whys to ensure root problem is understood | Extend backlog-manager |
| A7 | **Assumption Ledger** — running list of assumptions across all brainstorming sessions; reviewable by PO periodically | New directory + product-knowledge hook |
| A8 | **"What Would Users Hate?" Adversarial Session** — quick adversarial discovery for any proposed feature | Mode flag for feature-brainstormer |
| A9 | **Stakeholder Blindspot Audit** — who are the stakeholders NOT represented in current documentation? | Prompt in requirements-analyst |
| A10 | **Technical Debt Radar** — workflow specifically for discovering hidden tech debt that affects PO planning | New skill or prompt |

---

## Cluster B: Documentation Flow & Consistency

| # | Idea | Notes |
|---|------|-------|
| B1 | **Brainstorm-to-Backlog Bridge** — automated conversion from brainstorm/SUMMARY.md → backlog/US-XXX.md | Currently manual, gap exists |
| B2 | **Documentation Status Dashboard** — README showing which features have brainstorm → backlog → sprint → requirements coverage | New docs/STATUS.md |
| B3 | **Cross-Reference Validator** — checks if stories in backlog/ are referenced in any sprint plan | New agent or script |
| B4 | **Decision Log Auto-Population** — when brainstorm concludes with a recommendation, auto-create ADR in docs/decisions/ | Extend feature-brainstormer |
| B5 | **Story Completeness Checker** — validates all acceptance criteria, dependencies, and risks are documented | Extend backlog-manager |
| B6 | **Release Readiness Checklist** — before sprint ends, check what documentation/communication is needed | New sprint-planner extension |
| B7 | **Parking Lot Review Prompt** — periodic review of IDEAS.md "Parking Lot" sections to revive shelved ideas | New skill or scheduled prompt |
| B8 | **Scaffold Missing Directories** — create backlog/, sprints/, requirements/, roadmap/ with README starters | One-time fix (CRITICAL) |

---

## Cluster C: Orchestration Consistency (Technical Fixes)

| # | Idea | Notes |
|---|------|-------|
| C1 | **Add `tools` field to both agents** — feature-brainstormer and product-knowledge are missing tools frontmatter | CRITICAL fix |
| C2 | **Remove `competitive_intel/` reference** from product-knowledge or create the directory | Causes silent search failures |
| C3 | **Make po-brainstorm canonical entry point** — reduce direct feature-brainstormer auto-triggers to avoid skipping pre-discovery | Trigger keyword deduplication |
| C4 | **Domain Expert Swap Pattern** — document how to replace esign-domain-expert with a different domain for non-eSign products | Docs addition |
| C5 | **Product Context Template** — starter product_documents/ structure so PO knows what to fill in | New template file |
| C6 | **Consistent output path convention** — ensure all agents write to documented locations (currently implicit) | Docs or agent update |
| C7 | **agile-product-owner skill integration clarity** — both agents say they "use" it, but skill loading is static context; document how this actually works | CLAUDE.md update |
| C8 | **writing-clearly-and-concisely PO integration** — clarify when this skill is used in PO workflows | SKILL.md description update |

---

## Cluster D: PO-Specific Discovery Workflows

| # | Idea | Notes |
|---|------|-------|
| D1 | **Sprint Retrospective Brainstorm** — post-sprint, auto-brainstorm "what did we learn, what should we do differently?" | New skill |
| D2 | **Feature Hypothesis Builder** — for any feature idea, auto-generate testable hypotheses with measurable success metrics | Extend feature-brainstormer |
| D3 | **Persona-Driven Ideation Checklist** — ensure every brainstorm covers at least 3 different user personas | Extend feature-brainstormer |
| D4 | **"What's NOT in the Backlog?" Prompt** — cross-reference product vision against backlog to find gaps | product-knowledge extension |
| D5 | **Dependency Spider Map** — visualize dependencies across all backlog items to find hidden coupling | New skill |
| D6 | **Risk Register Auto-Generation** — after each brainstorm, extract all risks into a running risk register | New artifact directory |
| D7 | **"If We Had to Cut 50%" Scenario** — constraint inversion prompt that forces prioritization clarity | Mode for prioritization-engine |
| D8 | **User Feedback Integration Prompt** — structured workflow to bring external user feedback into brainstorm context | analytics-insights extension |
| D9 | **Edge Case Persona** — systematically brainstorm for "extreme users" (beginners, power users, accessibility needs, international) | Anti-bias addition to feature-brainstormer |
| D10 | **Quiet Signals Detector** — prompt that asks "what weak signals in user feedback might indicate future big problems?" | analytics-insights extension |

---

## Cluster E: Meta / System-Level Improvements

| # | Idea | Notes |
|---|------|-------|
| E1 | **Orchestration Health Checker Agent** — validates .claude/ folder for consistency (missing tools fields, dead references, etc.) | New agent |
| E2 | **Skill Usage Tracker** — simple doc tracking which skills are invoked most/least | docs/skill-usage.md |
| E3 | **Context Scale Strategy** — as product_documents/ grows, how does product-knowledge handle it? | Document or add chunking guidance |
| E4 | **Memory Update Protocol** — neither agent has a documented strategy for updating its own memory across sessions | Add to both agents |
| E5 | **Multi-Product Support** — how would system work for a PO managing multiple products? | Architecture consideration |
| E6 | **Onboarding Guide for New PO** — "here's how to use this system from day 1" quick-start document | docs/QUICKSTART.md |
| E7 | **Skill Deprecation Signal** — mechanism to mark skills as "not yet useful without X data" (e.g., analytics-insights needs real data) | Documentation |
