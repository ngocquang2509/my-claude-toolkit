---
description: Draft a pull request description for the current branch (print only)
argument-hint: "[target branch]"
disable-model-invocation: true
---

Draft a pull request description for me to paste into GitHub. Print only; never create the PR or push.

1. Target branch is `$ARGUMENTS`, else `main` (ask if unclear). Find the merge-base with it.
2. Read `git log <merge-base>..HEAD` and `git diff <merge-base>`. Include any spec, plan or issue I mention.
3. Print the description in one code block with these sections:
   - **Summary**: what changed and why, in a few sentences.
   - **Evidence**: how it was verified (tests, typecheck, manual checks) and anything not verified.
   - **Merge danger**: risks, migrations, breaking changes, or "none".
4. End with the attribution line given in the session's system reminder, if one is present.
