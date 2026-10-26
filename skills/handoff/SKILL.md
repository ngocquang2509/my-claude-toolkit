---
name: handoff
description: Write a handoff document so a fresh session can continue this work.
disable-model-invocation: true
argument-hint: "[focus for the next session]"
---

# Handoff

Compact this conversation into a document another session can pick up cold.

## Steps

1. Write the file to `~/.claude/handoffs/HANDOFF-<yyyy-mm-dd>-<slug>.md` (create the folder if needed; `<slug>` is 2-4 words naming the work).
2. Print the full path so the user can paste it into a new session.

## Contents

- **Goal**: what we are trying to achieve.
- **State**: what is done and what is in progress.
- **Decisions**: settled choices and why, so they are not re-litigated.
- **Next**: remaining steps, in order.
- **Skills to use next**: skills the next session should reach for.
- **Pointers**: paths to the plan, branch, PR, issue and key files.

## Rules

- Do not duplicate what already lives in commits, diffs or a plan file; point to it.
- Redact secrets as `<REDACTED>`.
- If the user passed an argument, make it the focus of the "Next" section.
- Keep it short enough to read in one minute.
