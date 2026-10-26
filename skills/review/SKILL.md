---
name: review
description: Review all pending changes before reporting work done. Use after finishing code changes and before handing over commit commands.
---

# Review

Review everything pending, committed or not. Run it once at the end of a unit of work, not after every edit. Skip it when the diff contains no code (docs or config text only).

## Gather

- **Fixed point**: the merge-base of the current branch with the branch it will merge into (usually `main`; ask if unclear).
- **Diff**: `git diff <merge-base>` (working tree vs merge-base, so uncommitted work is included).
- **New files**: `git status --porcelain`; read untracked files directly.
- **Spec**: the plan, issue or ADR the work came from. If none exists, skip the Spec axis. Do not block on asking.
- **Standards**: conventions written in the repo (CLAUDE.md, CONTRIBUTING, lint and format config).

## Axes

| Axis | Question |
|---|---|
| Spec | Does the code do what was asked, fully, and nothing less? |
| Correctness | Bugs, edge cases, error handling, races, off-by-one? |
| Standards | Does it follow the repo's written conventions? Also common smells (unclear names, duplication, needless abstraction) as judgement only. |
| Tests | Is new behavior tested? Do tests check behavior, not implementation? |
| Security | Secrets, untrusted input, injection, access control (light check; use `/security-review` for depth). |
| Scope | Anything outside the request: drive-by cleanup, reformatting, unrelated files? |

## Levels

- **Block**: Spec, Correctness or Security problems. Must be fixed.
- **Should fix**: Standards and Tests problems.
- **Nit**: smells and style. List only.

## Depth

Small diff (under about 80 changed lines): review inline. Larger: run two sub-agents in parallel (Standards + Correctness; Spec + Scope), giving each the diff command and the untracked file list.

## After the review

Fix Block and Should fix items, then re-run typecheck and tests. Report:

1. One-line verdict: clean, or has Block items.
2. Findings by level, each with `file:line`, the problem, the fix, and whether it is "fixed" or "needs your decision".

No praise filler, no restating the diff. Never run `git commit` or `git push`; the user runs commits.
