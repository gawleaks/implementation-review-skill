Invoke the `implementation-review` skill.

**Scope:** Completeness audit — probe exclusively for what's absent, not what's wrong in existing code.

$ARGUMENTS

Systematically check:

- Tests — unit tests for every public method and branch; integration tests if adjacent modules have them
- Types — interfaces and types exported, updated, consistent with shared type definitions
- Error paths — every failure mode handled; error types matching the module's conventions
- Edge cases — nulls, empty collections, boundary values, concurrent access where applicable
- Observability — logging, metrics, or tracing if adjacent modules include them
- Migrations — database or schema changes needed but not present
- Documentation — README, JSDoc, or API docs if the module's pattern includes them

Report each missing item as a Gap with its location and the ground truth that demands it.
