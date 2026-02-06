# Product Knowledge Agent - Documentation

**Date**: February 6, 2026  
**Agent Type**: New Agent  
**Agent Name**: product-knowledge

---

## Overview

The **product-knowledge agent** is a specialized Q&A agent that answers questions about your product by reading and synthesizing information from all available documentation.

**Core Principle**: **Never guess - only answer based on documented information.**

---

## Purpose

### What It Does ✅
- Answers questions about product features, roadmap, decisions, user research
- Searches all documentation sources comprehensively
- Synthesizes information from multiple documents
- Provides citations to specific documents
- Says "I don't know" when information is not found

### What It Doesn't Do ❌
- Make assumptions or guesses
- Provide opinions or recommendations (only facts from docs)
- Create new content (use other agents for that)
- Answer questions outside documented knowledge

---

## Key Features

### 1. Comprehensive Document Search 🔍
Searches these locations automatically:
- `product_documents/` - Product vision, user research, strategy
- `brainstorm/` - Brainstorming sessions and ideas
- `backlog/` - User stories and backlogs
- `requirements/` - Detailed requirements
- `sprints/` - Sprint plans and execution
- `docs/` - Product and architecture documentation
- `competitive_intel/` - Competitive analysis
- `roadmap/` - Roadmap plans
- Any other relevant folders

### 2. Systematic Search Workflow
```
1. Analyze question → Identify key terms and document types
2. Use Glob → Find all potentially relevant files
3. Use Grep → Search for specific terms in content
4. Use Read → Extract detailed information
5. Synthesize → Combine from multiple sources
6. Cite → Reference specific documents
7. Answer → Provide comprehensive response OR "I don't know"
```

### 3. Always Cites Sources 📚
Every answer includes:
- Specific file paths
- Document names
- Sections or quotes referenced
- Multiple sources if information is synthesized

### 4. Honest About Uncertainty 🎯
When information is not found:
- Says clearly: "I don't know"
- Explains what was searched
- Suggests where information might exist
- Never fills gaps with assumptions

---

## Question Types Supported

### Feature Questions
- "What AI features are we building?"
- "Do we have mobile signature support?"
- "What's the status of field detection?"

### Roadmap Questions
- "What are we building in Q2?"
- "When will feature X be delivered?"
- "What's our product roadmap?"

### User Research Questions
- "What do users say about mobile experience?"
- "What are the top user pain points?"
- "Who are our target users?"

### Decision Questions
- "Why did we choose approach X over Y?"
- "What's the rationale for prioritizing feature Z?"
- "Why are we building this?"

### Technical Questions
- "What are the technical dependencies for feature X?"
- "What's the estimated effort for this feature?"
- "What technical risks exist?"

### Status Questions
- "What's the status of feature X?"
- "Is feature Y in the backlog?"
- "What stories are in the current sprint?"

---

## How to Use

### Invoke the Agent
```
@product-knowledge - [Your question]
```

### Example Invocations

**Simple Feature Question**:
```
@product-knowledge - Do we have mobile signature support?
```

**Timeline Question**:
```
@product-knowledge - When will Computer Vision Field Detection be ready?
```

**User Research Question**:
```
@product-knowledge - What did users say about mobile document preparation?
```

**Strategic Question**:
```
@product-knowledge - Why did we prioritize AI features over workflow automation?
```

**Multi-Part Question**:
```
@product-knowledge - What's our mobile strategy, who are the target users, 
and when will it launch?
```

---

## Answer Quality Examples

### ✅ Good Answer Example

**Question**: "What AI features are we building for mobile?"

**Answer from Agent**:
```
Based on brainstorm/ai-mobile-document-prep/SUMMARY.md and 
backlog/ai-mobile-prep/README.md:

We are building 3 AI features for mobile document preparation:

1. **Computer Vision Field Detection** (US-001)
   - Status: Backlog - HIGH priority
   - Story Points: 13 points (~6-8 weeks)
   - Description: ML model automatically detects signature, date, 
     and initial fields with ≥85% accuracy
   - Rationale: 92% of surveyed users want auto-detection

2. **Confidence Scores + Visual Indicators** (US-002)
   - Status: Backlog - HIGH priority  
   - Story Points: 5 points (~1-2 weeks)
   - Description: Color-coded confidence levels for AI-detected fields
   - Rationale: Builds user trust in AI decisions

3. **Document Understanding + Contact Intelligence** (US-003)
   - Status: Backlog - HIGH priority
   - Story Points: 8 points (~4-6 weeks)
   - Description: AI extracts names/roles, auto-matches to contacts
   - Rationale: Eliminates manual signer assignment

Total estimated effort: 26 story points (~3 months for Phase 1)

Sources:
- brainstorm/ai-mobile-document-prep/SUMMARY.md
- backlog/ai-mobile-prep/US-001-computer-vision-field-detection.md
- backlog/ai-mobile-prep/US-002-confidence-scores-visual-indicators.md
- backlog/ai-mobile-prep/US-003-document-understanding-contact-intelligence.md
- backlog/ai-mobile-prep/README.md
```

**Why Good**:
- ✅ Specific details (story IDs, points, timelines)
- ✅ Multiple sources cited
- ✅ Rationale included
- ✅ Complete context provided
- ✅ File paths listed

---

### 🚫 "I Don't Know" Example

**Question**: "What's our pricing strategy for enterprise customers?"

**Answer from Agent**:
```
I don't know - I couldn't find detailed information about enterprise 
pricing strategy in the available documentation.

I searched:
- product_documents/ (product vision, strategy docs)
- docs/product/ (product documentation)
- competitive_intel/ (competitive analysis)
- All files for keywords: "pricing", "enterprise", "price"

What I did find:
- product_documents/product-vision.md mentions "Transparent pricing 
  (no per-envelope charges)" as a differentiator
- Unlimited templates and users as a feature

But I did not find specific enterprise pricing tiers, contract terms, 
or pricing strategy details.

You may need to ask the product or business team directly about 
enterprise pricing strategy.
```

**Why Good**:
- ✅ Honest about not knowing
- ✅ Explains search performed
- ✅ Mentions related info that WAS found
- ✅ Suggests next steps
- ✅ No guessing or assumptions

---

## Benefits

### 1. Single Source of Truth 📖
- Don't need to remember where information is documented
- Agent searches all locations automatically
- Comprehensive answers from multiple sources

### 2. Accurate Information ✅
- Never guesses or assumes
- Only provides documented facts
- Cites sources for verification

### 3. Time Savings ⚡
- **Before**: Search multiple folders manually (10-20 minutes)
- **After**: Ask agent, get answer with citations (1-2 minutes)
- **Time saved**: 80-90% per question

### 4. Onboarding Support 🎓
- New team members can ask questions
- Learn product context quickly
- Discover what's documented

### 5. Knowledge Validation 🔍
- Verify what's actually documented
- Find gaps in documentation
- Cross-reference conflicting information

---

## Integration with Other Agents

### Information vs Action

**Information Questions** (product-knowledge handles):
- "What features are we building?"
- "What's the status of X?"
- "What did user research say?"
- "When will Y ship?"

**Action Questions** (delegate to other agents):
- "Create user stories for X" → @backlog-manager
- "Brainstorm ideas for Y" → @feature-brainstormer
- "Analyze risk for Z" → @risk-assessor

**Agent Response for Action Questions**:
```
Based on the documentation, [provides current state].

To [perform action], you should use:
- @[agent-name] - [what they'll do]
```

---

## Skills Integration

The agent uses the **agile-product-owner skill** which provides:
- ✅ Understanding of user story formats
- ✅ Familiarity with INVEST principles
- ✅ Knowledge of agile terminology
- ✅ Understanding of backlog structures

This helps the agent interpret product documentation correctly and provide context-aware answers.

---

## Search Strategy

### Tools Used

**1. Glob** - Find files by name pattern
```
Example: Glob "**/*mobile*" finds all files with "mobile" in name
```

**2. Grep** - Search content within files
```
Example: Grep "AI.*feature" finds mentions of AI features
```

**3. Read** - Extract complete file content
```
Example: Read product_documents/product-vision.md
```

**4. Bash** - List directories, check file existence
```
Example: ls backlog/ to see what backlogs exist
```

### Search Order
1. Identify question type (feature, roadmap, user research, etc.)
2. Glob for relevant files
3. Grep for specific terms
4. Read matching files completely
5. Cross-reference multiple sources
6. Synthesize comprehensive answer

---

## Common Use Cases

### Use Case 1: Team Member Onboarding
**Scenario**: New PM joins team, needs to understand product

**Questions**:
- "What's our product vision?"
- "Who are our target users?"
- "What features are we building?"
- "What's the roadmap for Q2?"

**Benefit**: New PM gets up to speed quickly without reading every document

---

### Use Case 2: Stakeholder Updates
**Scenario**: Prepare for stakeholder meeting, need current status

**Questions**:
- "What's the status of mobile features?"
- "What user research have we done?"
- "What's our competitive positioning?"
- "What are we shipping this quarter?"

**Benefit**: Quick, accurate information with sources for credibility

---

### Use Case 3: Sprint Planning
**Scenario**: Planning next sprint, need to understand backlog

**Questions**:
- "What stories are in the backlog?"
- "What are the story point estimates for feature X?"
- "What dependencies exist for story US-001?"
- "What's the priority of feature Y?"

**Benefit**: All information in one place, faster planning

---

### Use Case 4: Decision Making
**Scenario**: Choosing between two feature approaches

**Questions**:
- "Why did we choose approach A in the past?"
- "What did user research say about this problem?"
- "What's the business impact of feature X?"
- "What technical risks were identified?"

**Benefit**: Make informed decisions based on documented context

---

### Use Case 5: Documentation Audit
**Scenario**: Verify what's actually documented

**Questions**:
- "What have we documented about pricing?"
- "Is there information about enterprise features?"
- "What decisions have been documented?"

**Benefit**: Identify documentation gaps, ensure completeness

---

## Limitations

### What It Can't Do

**1. Answer Undocumented Questions**
- If information is not in documents, agent says "I don't know"
- Cannot infer or guess missing information

**2. Provide Opinions or Recommendations**
- Only provides facts from documentation
- Cannot say "you should do X" unless documented

**3. Create New Content**
- Cannot create user stories, brainstorm ideas, or write docs
- Use other agents for creation tasks

**4. Access External Information**
- Only searches local documentation
- Cannot fetch from web, APIs, or external sources

**5. Interpret Ambiguous Documents**
- If documents conflict, agent reports the conflict
- Cannot decide which document is "correct"

---

## Best Practices

### For Users

**✅ Do**:
- Ask specific questions
- Include context in multi-part questions
- Verify sources cited by agent
- Follow up if answer is unclear

**❌ Don't**:
- Ask for opinions or recommendations
- Expect answers to undocumented questions
- Assume agent has external knowledge
- Skip reading cited sources for important decisions

---

### For Documentation

**✅ Do**:
- Keep product documentation up to date
- Document decisions and rationale
- Use consistent terminology
- Structure documents clearly (headings, sections)

**❌ Don't**:
- Leave critical information undocumented
- Spread information across too many files
- Use ambiguous language
- Create conflicting documents without resolution

---

## Troubleshooting

### Problem: Agent says "I don't know" but information exists

**Solution**:
- Check if information is in expected locations
- Ensure file naming is consistent
- Use clear, searchable terminology in documents
- Add keywords to document titles/headings

---

### Problem: Agent provides outdated information

**Solution**:
- Update or remove outdated documents
- Use consistent document naming (include dates)
- Archive old versions in separate folder
- Indicate "current" vs "historical" in document structure

---

### Problem: Agent cites conflicting sources

**Solution**:
- Review both documents
- Determine which is current
- Update or remove outdated document
- Document the resolution

---

### Problem: Agent answers are too long/short

**Solution**:
- For shorter answers: Ask more specific questions
- For longer answers: Agent provides comprehensive info by default
- Request "just the summary" if you want brevity

---

## File Structure

### Agent File
- Location: `claude/agents/product-knowledge.md`
- Size: ~700 lines
- Tools: Read, Grep, Glob, Bash
- Skills: agile-product-owner

### Documentation
- Agent documentation: `claude/agents/product-knowledge.md` (the agent file itself)
- This summary: `docs/architecture/product-knowledge-agent.md`

---

## Testing the Agent

### Test Scenario 1: Feature Question
```
@product-knowledge - What AI features are we building for mobile?

Expected: List of AI features from brainstorm/ and backlog/ with details
```

### Test Scenario 2: Timeline Question
```
@product-knowledge - When will Computer Vision Field Detection be ready?

Expected: Timeline from backlog/US-001 with breakdown and status
```

### Test Scenario 3: "I Don't Know" Response
```
@product-knowledge - What's our pricing for enterprise customers?

Expected: "I don't know" with explanation of what was searched
```

### Test Scenario 4: Multi-Part Question
```
@product-knowledge - What's our mobile strategy, who are the target 
users, and when will it launch?

Expected: Answers to all 3 parts with sources cited for each
```

---

## Comparison to Other Agents

### vs. backlog-manager
- **product-knowledge**: Reads backlog, answers questions
- **backlog-manager**: Creates/updates backlog items

### vs. feature-brainstormer
- **product-knowledge**: Reads brainstorming docs, answers questions
- **feature-brainstormer**: Creates brainstorming sessions

### vs. documentation-agent
- **product-knowledge**: Reads all docs, answers questions
- **documentation-agent**: Creates/updates documentation

**Key Difference**: product-knowledge is **read-only Q&A**, other agents **create/modify content**.

---

## Future Enhancements

### Potential Improvements
1. **Structured Query Language**: Support complex queries like "Find all HIGH priority stories in backlog"
2. **Trend Analysis**: "How has our roadmap changed over time?"
3. **Gap Detection**: "What information is missing about feature X?"
4. **Automatic Summaries**: "Summarize all user research from Q1"
5. **Natural Language Search**: More flexible question formats

---

## Success Metrics

### Process Metrics
- **Search time**: Time to find answer (target: <30 seconds)
- **Accuracy rate**: % of answers that are factually correct (target: 100%)
- **Source citation**: % of answers with sources cited (target: 100%)
- **"I don't know" rate**: % of questions where info not found (track to identify doc gaps)

### Outcome Metrics
- **Time saved**: Avg time saved per question vs manual search
- **Questions answered**: # of questions answered successfully
- **User satisfaction**: Agent provided helpful information (survey)

---

## Conclusion

The **product-knowledge agent** is your **single source of truth** for product information:
- ✅ Searches all documentation comprehensively
- ✅ Provides accurate, cited answers
- ✅ Says "I don't know" when info is missing
- ✅ Saves 80-90% of time vs manual search
- ✅ Helps onboard team members quickly

**Use it whenever you need to know**: "What's documented about X?"

---

## Quick Reference

**Agent Name**: product-knowledge  
**Invocation**: `@product-knowledge - [Your question]`  
**Best For**: Answering questions about product features, roadmap, decisions, user research  
**Not For**: Creating content, making recommendations, accessing undocumented info  
**Key Principle**: Never guess - only answer based on documented information

---

## Questions?

For questions about this agent:
- Review agent file: `claude/agents/product-knowledge.md`
- Test with sample questions
- Check documentation: `product_documents/`, `brainstorm/`, `backlog/`
