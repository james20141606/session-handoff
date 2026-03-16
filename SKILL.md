---
name: session-handoff
description: Generate a structured handoff document for the next AI agent when ending a long session. Use when the user says "handoff", "交接", "session handoff", "工作交接", "写交接文档", "context too long", "开新会话", "new session", or wants to transfer work context to a fresh conversation. Also use when the user mentions hallucinations increasing, conversation getting too long, or wants to start over without losing progress.
---

Generate a handoff document at `./{YYMMDD}-handoff.md` (use today's date) for the next AI agent to continue work.

The document is written **for another AI agent**, not for the user. Assume the reader has zero prior context and can only see this file.

## Output Structure

```markdown
# Session Handoff - {YYYY-MM-DD}

## 1. Current Task Objective
What problem is being solved, expected output, and completion criteria.

## 2. Current Progress
What analysis, changes, fixes, discussions, or outputs have been completed.

## 3. Key Context
- Important background information
- User's explicit requirements
- Known constraints
- Key decisions already made
- Important assumptions

## 4. Key Findings
Most important conclusions, patterns, anomalies, root causes, design judgments, or noteworthy information discovered so far.

## 5. Unfinished Items
Remaining work, sorted by priority.

## 6. Recommended Handoff Path
- Which files, modules, data, logs, commands, pages, or leads to check first
- What to verify first
- Recommended next actions

## 7. Risks and Caveats
- What is easy to misjudge or get wrong
- What directions have been tried and should not be repeated
- What could cause wasted effort

## First Step for the Next Agent
One concrete, actionable first move.
```

## After Writing the Handoff File

Print a ready-to-paste prompt block for the user to start the new session with:

```
📋 Copy the following into your new session:
─────────────────────────────────────────
Read ./{YYMMDD}-handoff.md — this is a handoff document from a previous session. Follow the "First Step for the Next Agent" section and continue the work described in it.
─────────────────────────────────────────
```

## Rules

- Be specific: use exact file paths, class names, module names, API names, commands, error messages, and decision points.
- Prioritize actionable information over summaries.
- Include code snippets or command examples where they save the next agent significant ramp-up time.
- If there are modified but uncommitted files, list them explicitly.
- If there are running processes, background jobs, or temporary state, mention them.
- Keep it concise but complete. No filler, no pleasantries.
