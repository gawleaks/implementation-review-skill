---
description: "Review a module's design — interfaces, depth, seams, and architectural fit"
agent: "agent"
argument-hint: "Path to the module or area to review, e.g. src/domain/voyages"
---
Invoke the `implementation-review` skill. If the `codebase-design` skill is available, invoke it for the interface-depth and seam-placement lenses; otherwise apply those lenses using ground truth from `implementation-review`.

**Scope:** Architectural review of the specified module or area. This is not a line-by-line code review — focus on structural qualities.

Build ground truth first, then probe through these design lenses:

- **Interface depth** — is the module deep (lots of behaviour behind a small interface) or shallow (pass-through)?
- **Seam placement** — are seams at the right boundaries? Are dependencies injected or hard-wired?
- **Contract integrity** — does the module honour contracts with its neighbours? Are shared types and interfaces consistent?
- **Domain fidelity** — does the structure reflect domain concepts? Are aggregates, entities, and value objects correctly bounded?
- **ADR conformance** — does the design align with existing architectural decisions in `docs/adr/`?

Report findings as gaps, violations, or risks with concrete locations.
