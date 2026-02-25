---
name: po-research
description: "Product Owner research entry point. Routes to product-knowledge agent to answer questions from documented product artifacts. Searches product_documents/, brainstorm/, backlog/, sprints/, requirements/, roadmap/. Only answers from documented information with cited sources — never guesses. Use for: feature status, decisions, roadmap priorities, requirements, user research findings, stakeholder feedback."
---

# PO Research

Query: $ARGUMENTS

## Usage

Ask any product question and this skill routes it to the `product-knowledge` agent, which searches all product documentation and returns answers with source citations.

**Examples:**
- `/po-research what features are planned for mobile?`
- `/po-research what did we decide about the signature workflow?`
- `/po-research what are the requirements for onboarding?`
- `/po-research what's the status of the backlog for Q2?`
- `/po-research why did we prioritize feature X over Y?`

## Invocation

**Claude Code CLI:**
```
Task(
  subagent_type="product-knowledge",
  prompt="Question: $ARGUMENTS

IMPORTANT: You are running as a sub-agent. You do NOT have access to AskUserQuestion.
Return your answer directly without attempting to ask clarifying questions.

Search product documentation to answer this question. Check these locations:
- product_documents/ (product vision, strategy, user research)
- brainstorm/ (brainstorming sessions and feature exploration)
- backlog/ (user stories and epics)
- sprints/ (sprint plans and history)
- requirements/ (structured requirements)
- roadmap/ (roadmap and priorities)
- docs/ (workflow guides, ADRs, architecture)

Return only information found in documents. Cite exact file paths as sources. Say 'I don't know' if not documented."
)
```

**VSCode Copilot:**
Invoke the `product-knowledge` agent with: "Use the product-knowledge agent to answer: [question]"

The agent will:
- Search all product documentation directories
- Return answers with cited source file paths
- Say "I don't know" if the information is not documented
- Never guess or infer beyond what is documented

## What Next?

After the agent completes, present these next-step options to the user as plain text:

**What would you like to do next?**
- `/po-brainstorm [topic]` -- Brainstorm ideas around this research topic
- **Done** -- No further action needed
