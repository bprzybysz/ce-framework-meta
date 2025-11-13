# Context Engineering v2.0 Meta Framework

## Project Goal
Establish an agentic, graph-based context engineering framework for pattern-driven development, serialization, validation, and migration of programmable systems. Designed for integration as the meta-layer in Perplexity Space orchestration, applying principles of KISS, SOLID, and YAGNI for efficient and robust context processing.

## Key Features
- Formal pattern graph schema (nodes, edges, migration)
- Agentic pattern catalog (Observer, Facade, Cascade, Sequential, Quality Gates, Composition)
- Axiom hardening and governance (Cycle 1 complete)
- Automated validation suite (structural, semantic, compositional, temporal)
- PRP-driven refinement and migration cycles
- Comprehensive schema-axiom mapping for traceability
- Temporal and migration constraints for scalable system evolution
- Two-repository architecture: meta framework and orchestration layer

## Implementation Highlights
- [Axioms](patterns/axioms-v1.yaml): 16 refined, testable requirements
- [Schema Mapping](docs/axiom-schema-mapping.md): Explicit axiom-field linkage
- [Validation Rules](ontology/validation.yaml): Automated suite for rule enforcement
- [Pattern Testing](migrations/cycle-1-pattern-testing.md): 6 high-value patterns, validation coverage documented
- [Governance](migrations/): Entry/exit criteria, rollback, migration versioning

## Workflow
1. Review meta framework (schemas, axioms, validation)
2. Serialize patterns and relationships using formal schema
3. Apply validation suite and governance checks
4. Track progress by cycle and artifact
5. Bump version, tag release, and prepare for next refinement

## Recommendations (from Nov 2025 Review)
- Add .gitmodules for submodule integration in orchestration repo
- Update pattern-schema.json: make description required
- Expand validation coverage and implementation
- Create quick start and pattern templates
- Automate progress tracking and CI validation
- Document known limitations and troubleshooting

## Integration
- Acts as authoritative source in [perplexity-space-context](https://github.com/bprzybysz/perplexity-space-context)
- Designed for rapid, testable context engineering evolution in collaborative, agentic environments

---
**For full implementation review, see [Project Evaluation Report](migrations/cycle-1-pattern-testing.md)**

**Latest Release:** v1.0.1 (Cycle 1 complete)

**Maintainer:** Blazej Przybyszewski (<blazej.przybyszewski@gmail.com>)
