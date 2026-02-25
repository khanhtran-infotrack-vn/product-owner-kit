# User Interaction Patterns for Agents and Skills

**Created**: 2026-02-25
**ADR**: `docs/adrs/260225-askuserquestion-subagent-constraint.md`

---

## The Constraint

`AskUserQuestion` is a Claude Code tool available ONLY in the main conversation
context. Sub-agents spawned via `Task()` do NOT have access. Any sub-agent that
calls `AskUserQuestion` will silently fail or hang.

---

## Three Approved Patterns

### Pattern 1: Parent-Skill Pre-Discovery
- **Context**: Main conversation (skill loaded as context)
- **Tool available**: YES -- AskUserQuestion works here
- **When**: Before spawning a sub-agent, when essential context is missing
- **How**: Ask 1-3 targeted questions using AskUserQuestion. Pass answers into
  the Task() prompt as a "User context" block.
- **Example**: `po-brainstorm` asks target persona and constraints before
  spawning `feature-brainstormer`.

### Pattern 2: Agent Output-Text Questions
- **Context**: Sub-agent (inside Task())
- **Tool available**: NO -- AskUserQuestion NOT available
- **When**: During execution, when follow-up information would improve output
- **How**: Write questions in output text under a standardized heading.
  Proceed with best judgment for non-blocking questions.
- **Heading**: `## FOLLOW-UP QUESTIONS FOR USER` (placed at END of output)
- **Example**: Feature-brainstormer writes follow-up questions and continues
  generating ideas.

### Pattern 3: Post-Agent Plain-Text Follow-Up
- **Context**: Main conversation (after sub-agent returns)
- **Tool available**: Depends -- use plain text to be safe
- **When**: After sub-agent completes, to present next-step options
- **How**: Present options as formatted markdown text, NOT as
  `AskUserQuestion([{...}])` function-call syntax.
- **Example**: po-brainstorm's "What Next?" section lists options as plain text.

---

## Checklist for New Skills and Agents

When creating a skill that delegates to an agent via Task():

1. [ ] Add a **Pre-Discovery** section to the skill (Pattern 1)
2. [ ] Include this line in the Task() prompt:
       `IMPORTANT: You are running as a sub-agent. You do NOT have access to AskUserQuestion.`
3. [ ] Add a **Sub-Agent Mode** section to the agent file (Pattern 2)
4. [ ] Use plain text for "What Next?" sections in the skill (Pattern 3)
5. [ ] Never use `AskUserQuestion([{...}])` syntax in skill files

---

## Anti-Patterns (Do NOT Do These)

| Anti-Pattern | Why It Breaks | Fix |
|---|---|---|
| `AskUserQuestion([{...}])` in a skill file | Ambiguous -- sometimes interpreted as a call, sometimes as inert text | Use plain-text options (Pattern 3) |
| "ALWAYS ask the user" in an agent file | Blocks the entire workflow in sub-agent mode | Make context-aware: ask in interactive mode, default in sub-agent mode |
| "Present to user for confirmation" without fallback | Agent stalls waiting for response that never comes | Add parenthetical: "(in sub-agent mode: present and proceed)" |
| Agent assumes it can ask probing questions mid-workflow | Questions go unanswered in sub-agent context | Pattern 2: write questions in output, proceed with best judgment |

