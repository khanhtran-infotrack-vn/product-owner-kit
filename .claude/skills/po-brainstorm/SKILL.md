---
name: po-brainstorm
description: "Product Owner brainstorming entry point. Routes to feature-brainstormer agent for structured ideation with SCAMPER, anti-bias rotation, idea clustering, Challenge & Critique phase (pre-mortem, devil's advocate, constraint inversion), and optional user story generation. Modes: --quick (skip ideation/clustering), --challenge (challenge-only on existing ideas), --idea (ideation only)."
---

# PO Brainstorm

Topic: $ARGUMENTS

## Mode Detection

Parse `$ARGUMENTS` for mode flags before delegating:
- Default (no flag): Full workflow — context gathering, ideation, clustering, evaluation, challenge & critique, documentation
- `--quick`: Skip ideation + clustering, go straight to evaluation and challenge
- `--challenge`: Challenge-only mode — stress-test existing ideas without generating new ones
- `--idea`: Ideation-only — stop after idea clustering (skip challenge and deep evaluation)

Strip mode flags from topic string before delegation.

## Pre-Discovery (before delegation)

Before spawning the feature-brainstormer agent, gather essential context that the
agent cannot ask for interactively. If the user has NOT provided this information
in their topic description, ask ONE AT A TIME using AskUserQuestion:

1. **Target persona**: "Who is the primary user you're brainstorming for?" (skip if obvious from topic)
2. **Scope constraint**: "Any specific constraints? (budget, timeline, technical)" (skip if mentioned)
3. **Session goal**: "New feature brainstorm, improvement to existing, or problem-solving?" (skip if clear)

Only ask where the answer is genuinely unclear. Pass all gathered context into the
Task() prompt as the `User context` block below.

**Why here and not in the agent**: The agent runs as a sub-agent via Task() and does
NOT have access to AskUserQuestion. This pre-discovery step runs in the main
conversation context where the tool IS available.

## Invocation

**Claude Code CLI:**
```
Task(
  subagent_type="feature-brainstormer",
  prompt="Topic: [topic with flags stripped]
Mode: [full|quick|challenge|idea]

User context (gathered during pre-discovery):
- Target persona: [answer or 'not specified -- use your best judgment']
- Constraints: [answer or 'none specified']
- Session type: [answer or 'inferred from topic']

IMPORTANT: You are running as a sub-agent. You do NOT have access to AskUserQuestion.
- Do NOT attempt to call AskUserQuestion or block waiting for user input.
- When you would normally ask a probing question, write it in your output and proceed
  with your best professional judgment.
- For user story creation: create draft stories by default (the user requested a full
  brainstorming session). Note they are drafts pending review.
- For cluster confirmation and ranking consensus: present your analysis and proceed.
- Place any follow-up questions at the END of your output under a
  '## FOLLOW-UP QUESTIONS FOR USER' heading.

Read product context from product_documents/ and existing brainstorm sessions from brainstorm/.

Run the appropriate mode:
- full: all phases (context → ideation → clustering → evaluation → challenge & critique → documentation)
- quick: skip ideation + clustering, go straight to evaluation + challenge
- challenge: challenge-only on existing ideas (read brainstorm/[topic]/SUMMARY.md first)
- idea: ideation + clustering only (stop before challenge)"
)
```

**VSCode Copilot:**
Invoke the `feature-brainstormer` agent with: "Use the feature-brainstormer agent to brainstorm [topic]" (add "in quick mode", "challenge-only", or "ideation only" as needed)

The agent will:
- Read product context from `product_documents/`
- Facilitate ideation using SCAMPER + "How Might We" + anti-bias domain rotation
- Cluster ideas into themes with scoring
- Evaluate each idea (User Value / Business Impact / Technical Feasibility, 1-5)
- Run Challenge & Critique phase (pre-mortem, assumption stress-test, devil's advocate, constraint inversion)
- Reconcile rankings after challenge
- Document in `brainstorm/[topic]/SUMMARY.md` and `IDEAS.md`
- Optionally generate draft user stories with story point estimates

## What Next?

After the agent completes, present these next-step options to the user as plain text:

**What would you like to do next?**
- `/po-brainstorm [topic] --challenge` -- Re-challenge the ideas from this session
- `/po-research [topic]` -- Look up existing research or decisions related to this topic
- **Done** -- No further action needed
