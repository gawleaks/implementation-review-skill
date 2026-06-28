---
description: "Review the last commit(s) against codebase ground truth"
agent: "agent"
argument-hint: "Optional: commit range like HEAD~3..HEAD or a commit SHA"
---
Invoke the `implementation-review` skill.

**Scope:** Review committed changes. Use the user-provided range, or default to `HEAD~1..HEAD` (last commit).

Run `git diff <range>` and `git log --oneline <range>` to enumerate what changed and why.

Apply all review steps and lenses from the skill. Report findings grouped by severity (gap, violation, risk).
