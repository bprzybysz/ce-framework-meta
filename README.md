# Context Engineering v2.0 Meta Framework

## Project Goal
Establish a robust, agentic, graph-based meta framework for programmable system patterns. Enable pattern-driven development, validation, migration, and governance, serving as the authoritative context schema for Perplexity Space orchestration and advanced coding agents.

## Core Features
- Formal graph schemas for nodes, edges, and governance
- Agentic pattern catalog (Observer, Facade, Cascade, Sequential, Validation, Composition)
- Full axiom hardening with governance (Cycle 1 complete)
- Automated validation suite covering structural, semantic, compositional, temporal logic
- PRP-driven refinement and migration cycles
- Schema-to-axiom mapping for compliance and traceability
- Temporal/migration support for scalable evolution
- Two-repo architecture (meta + orchestration workspace)

## Documentation & Artifacts
- [Axioms](patterns/axioms-v1.yaml): rigorous testable requirements
- [Schema Mapping](docs/axiom-schema-mapping.md): explicit axiom ↔️ schema linkage
- [Validation Rules](ontology/validation.yaml): automated validation suite
- [Pattern Testing](migrations/cycle-1-pattern-testing.md): full artifact coverage
- [Implementation Review](docs/IMPLEMENTATION-REVIEW-CYCLE-1.md): recommendations and next steps

## How To Use
1. Review meta framework (schemas, axioms, validation logic)
2. Serialize patterns to match meta schemas
3. Apply validation suite and governance
4. Track cycles, migrate, and evolve collaboratively

## Integration
- Authoritative meta layer for [perplexity-space-context](https://github.com/bprzybysz/perplexity-space-context)
- Enables rapid, testable, future-proof context engineering

## Recommendations: Nov 2025 Review
- Setup .gitmodules for repo integration
- Make description required in pattern-schema.json
- Expand validation implementations & coverage
- Create quick start and pattern templates
- Build CI/CD validation workflows & increase test set

**Contact**: Blazej Przybyszewski (<blazej.przybyszewski@gmail.com>)

---
**Release:** v1.0.1 (Cycle 1 complete)

See full review in [docs/IMPLEMENTATION-REVIEW-CYCLE-1.md](docs/IMPLEMENTATION-REVIEW-CYCLE-1.md)