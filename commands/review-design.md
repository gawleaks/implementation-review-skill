Invoke the `implementation-review` skill.

**Scope:** Architectural review of the specified module or area. Focus on structural qualities, not line-by-line code.

$ARGUMENTS

Probe through design lenses:

- Interface depth — is the module deep (lots of behaviour behind a small interface) or shallow (pass-through)?
- Seam placement — are seams at the right boundaries? Are dependencies injected or hard-wired?
- Contract integrity — does the module honour contracts with its neighbours? Are shared types and interfaces consistent?
- Domain fidelity — does the structure reflect domain concepts? Are aggregates, entities, and value objects correctly bounded?
- ADR conformance — does the design align with existing architectural decisions?

Report findings as Gap, Violation, or Risk with concrete file locations and the ground truth each violates.
