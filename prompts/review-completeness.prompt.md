---
description: "Check what's missing from a feature implementation — tests, types, error paths, edge cases"
agent: "agent"
argument-hint: "Describe the feature or point to the files that implement it"
---
Invoke the `implementation-review` skill.

**Scope:** Completeness audit. The user describes a feature or points to files — probe exclusively for what's **absent**, not what's wrong in existing code.

Build ground truth by reading adjacent modules that follow the same patterns. Then systematically check:

- **Tests** — unit tests for every public method and branch; integration tests if adjacent modules have them; test patterns matching the module's neighbours
- **Types** — interfaces and types exported, updated, and consistent with shared type definitions
- **Error paths** — every failure mode handled; error types matching the module's conventions
- **Edge cases** — nulls, empty collections, boundary values, concurrent access where applicable
- **Observability** — logging, metrics, or tracing if adjacent modules include them
- **Migrations** — database or schema changes needed but not present
- **Documentation** — README, JSDoc, or API docs if the module's pattern includes them

Report each missing item as a gap with its location and the ground truth that demands it.
