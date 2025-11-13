# PRP-1: Axiom Hardening Cycle

## Product Requirements Prompt

### Context
You are working on the CE Framework Meta Repository refinement cycle 1. The goal is to finalize all pattern axioms that govern serializing existing CE patterns into graph representation.

### Objective
Complete axiom hardening with 100% review coverage, validated schemas, and passing validation suite.

### Tasks

#### 1. Review & Triage Draft Axioms
- [ ] Read `/patterns/axioms-v1.yaml`
- [ ] Mark each axiom: KEEP / REVISE / DROP
- [ ] Document reasoning in `/migrations/cycle-1-axiom-review.md`

#### 2. Add Missing Edge-Case Axioms
- [ ] Add versioning semantics axiom
- [ ] Add temporal edge handling axiom
- [ ] Add rollback/migration-stage axiom
- [ ] Add composition validation axiom
- [ ] Document in `/patterns/axioms-v1.yaml`

#### 3. Schema Validation
- [ ] Ensure every axiom maps to schema fields in `/schemas/pattern-schema.json`
- [ ] Ensure every axiom maps to schema fields in `/schemas/edge-schema.json`
- [ ] Create mapping document: `/docs/axiom-schema-mapping.md`

#### 4. Validation Rules
- [ ] Create validation test for each axiom in `/ontology/validation.yaml`
- [ ] Implement structural validation rules
- [ ] Implement semantic validation rules
- [ ] Document test coverage in `/migrations/cycle-1-validation-coverage.md`

#### 5. Sample Pattern Testing
- [ ] Select 5-10 high-value patterns from existing framework
- [ ] Serialize to graph format using axioms
- [ ] Run validation suite
- [ ] Document gaps and fixes in `/migrations/cycle-1-pattern-testing.md`

### Acceptance Criteria
- 100% of axioms reviewed and marked
- All missing axioms added and documented
- Complete axiom-to-schema mapping exists
- Validation suite passes on all sample patterns
- All tasks checked off in `/migrations/refinement-cycle-1-progress.md`

### Output Artifacts
- Updated `/patterns/axioms-v1.yaml`
- Updated `/schemas/pattern-schema.json`
- Updated `/schemas/edge-schema.json`
- New `/ontology/validation.yaml`
- New `/docs/axiom-schema-mapping.md`
- New `/migrations/cycle-1-axiom-review.md`
- New `/migrations/cycle-1-validation-coverage.md`
- New `/migrations/cycle-1-pattern-testing.md`
- Updated `/migrations/refinement-cycle-1-progress.md`

### Version Bump
After completion, bump version to `v1.0.1` in `/VERSION` and update `/CHANGELOG.md`
