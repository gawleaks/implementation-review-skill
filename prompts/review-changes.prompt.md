---
description: "Review uncommitted changes against codebase ground truth — find gaps, violations, and missing pieces"
agent: "agent"
argument-hint: "Optional: describe the intent of your changes"
---
Invoke the `implementation-review` skill.

**Scope:** Review the current uncommitted changes (staged + unstaged) in this workspace.

Run `git diff HEAD` to enumerate what changed. If the user provided an intent description, use it; otherwise infer intent from the diff.

Apply all review steps and lenses from the skill. Report findings grouped by severity (gap, violation, risk).
