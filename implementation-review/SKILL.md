---
name: implementation-review
description: >
  Probe changes against codebase ground truth — finds gaps, pattern violations, and
  missing pieces in implemented features. Use when the user asks to review changes,
  check an implementation, find what's missing, or validate a feature is complete.
  Use when another skill needs a post-implementation quality gate.
---

# Implementation Review

Probe implemented changes against the codebase's **ground truth** — the established patterns, domain model, conventions, and architectural decisions. The goal is not style nitpicks but structural gaps: what's missing, what breaks contracts, what violates the system's own rules.

## Steps

### 1. Build ground truth

Read the system before judging the change. Load, in order:

- `CONTEXT.md` and `docs/adr/` — domain language and architectural decisions (proceed silently if absent)
- The module or domain area the change touches — its existing patterns, types, tests, and interfaces
- Adjacent modules that interact with the changed code — their contracts and expectations

Explore the unchanged code until you can name the conventions it follows. Look for: directory structure patterns, naming conventions, dependency injection style, test structure, error handling idiom, and type definitions. These are the rules the change must obey.

**Completion criterion:** you can describe how the affected subsystem works, what patterns it follows, and what contracts it maintains with its neighbours — without referencing the change itself.

### 2. Scope the change

Identify what changed and why:

- Run `git diff --stat` and `git diff` (or read the user's description) to enumerate every changed and added file
- Articulate the intent in domain language: what behaviour is being added, changed, or fixed?
- Map each changed file to the ground truth area it touches

When reviewing a feature rather than a diff, use the boundary provided by the invoking context. If no boundary is provided and no invoking context supplies one, ask the user. Do not guess the boundary.

**Completion criterion:** every changed file listed, intent articulated in domain vocabulary, and each change mapped to the subsystem it affects.

### 3. Probe

Examine each change through every applicable **lens** below. Probe for what's absent, not just what's wrong — the most damaging gaps are things that should exist but don't.

#### Lenses

- **Pattern conformance** — does the change follow the patterns established in the same module? Check: naming conventions, file structure, dependency direction, error handling style, test patterns. A deviation is a finding even when the new way is arguably better — the codebase chose, and unilateral divergence is a cost.
- **Domain fidelity** — does the change use the domain's vocabulary correctly? Are new concepts named consistently with `CONTEXT.md`? Does the behaviour match the domain model's rules?
- **Completeness** — what's missing? Systematically check: tests (unit and integration), types and interfaces updated, error paths handled, edge cases covered, migrations needed, documentation updated, logging and observability added. Compare the test coverage pattern in adjacent modules — if they test X, this change should test X too.
- **Contract integrity** — does the change maintain contracts with adjacent code? Check: interface changes propagated to all callers, event schemas honoured, API contracts preserved, database constraints respected, shared types updated.
- **Regression surface** — could this break existing behaviour? Look for: changed function signatures, altered default values, removed or renamed exports, changed error types, modified query patterns, implicit assumptions in callers.

**Completion criterion:** every changed file examined against every applicable lens. Every finding documented with its location, the problem, and the ground truth it violates.

### 4. Report

Deliver findings grouped by severity:

- **Gap** — something missing that the ground truth demands (a test the pattern requires, an error path the convention handles, a type the interface needs)
- **Violation** — something present that contradicts the ground truth (a pattern broken, a contract breached, a domain term misused)
- **Risk** — something that works now but creates future problems (a regression surface, an implicit coupling, a missing migration)

Each finding states: **where** (file and location), **what** (the problem), and **against what** (the ground truth that makes it a problem).

**Completion criterion:** every finding from step 3 classified, reported, and traceable to a specific ground truth. No finding left unclassified. No lens left unapplied.

## Boundaries

This skill probes — it does not fix. Output is findings, not patches. If the user wants fixes applied, that is a separate pass.

Does not replace linters, type checkers, or CI. Assumes automated checks pass. Probes for what automated tools cannot catch: structural gaps, missing pieces, and pattern violations that require system understanding.
