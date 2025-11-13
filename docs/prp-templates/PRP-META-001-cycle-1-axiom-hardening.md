# PRP-META-001: Cycle 1 - Axiom Hardening

## Overview

Harden pattern axioms to establish a complete foundation for graph-based pattern serialization. This includes tri-aging existing axioms, adding missing edge cases, validating against real patterns using Serena MCP, and building a comprehensive validation test suite.

## Success Criteria

- [ ] 100% axioms reviewed (keep/revise/drop decisions documented)
- [ ] All schema fields mapped to at least one axiom
- [ ] Edge-case axioms added (versioning, rollback, composition)
- [ ] Serena MCP extraction validates axiom coverage
- [ ] Validation suite passes against sample patterns
- [ ] Progress checklist 100% complete
- [ ] Version bumped to v0.2.0, tagged and released

## Context

This is the first refinement cycle for the CE framework meta-repository. The goal is to establish a solid axiom foundation before attempting pattern serialization in Cycle 2.

**Related Files**:
- `/patterns/axioms-v1.yaml` - Current draft axioms
- `/schemas/pattern-schema.json` - Pattern node schema
- `/schemas/edge-schema.json` - Edge relationship schema
- `/migrations/refinement-cycle-1-progress.md` - Progress tracking

---

## Phases

### Phase 1: Tri-age Draft Axioms

**Goal**: Review and categorize each existing axiom as keep/revise/drop

**Estimated Hours**: 2

**Complexity**: low

**Files Modified**:
- `/patterns/axioms-v1.yaml` → `/patterns/axioms-v2.yaml`

**Dependencies**: None

**Implementation Steps**:
1. Read `/patterns/axioms-v1.yaml`
2. For each axiom:
   - Evaluate necessity for graph serialization
   - Check for redundancy or conflicts
   - Mark decision: `# KEEP`, `# REVISE: reason`, `# DROP: reason`
3. Document rationale in comments
4. Create `/patterns/axioms-v2.yaml` with kept/revised axioms
5. Update progress checklist

**Validation Gates**:
- [ ] Every axiom has a decision marker
- [ ] Dropped axioms have documented rationale
- [ ] Revised axioms include improvement notes
- [ ] No duplicate or conflicting axioms remain

**Conflict Notes**: None - single file transformation

---

### Phase 2: Add Missing Edge-Case Axioms

**Goal**: Extend axiom set to cover versioning, rollback, and composition edge cases

**Estimated Hours**: 3

**Complexity**: medium

**Files Modified**:
- `/patterns/axioms-v2.yaml`

**Dependencies**: Phase 1

**Implementation Steps**:
1. Add versioning axioms:
   - Pattern versions use semantic versioning
   - Temporal edges track pattern evolution
   - Version compatibility rules for composition
2. Add rollback/migration axioms:
   - Migration stages are reversible
   - Rollback preserves graph integrity
   - Snapshot semantics for stage checkpoints
3. Add edge validation axioms:
   - Edge types must match source/target constraints
   - Circular dependencies detected and prevented
   - Edge weight/priority semantics
4. Add composition/conflict axioms:
   - Pattern composition rules (AND/OR/XOR)
   - Conflict detection between patterns
   - Resolution strategies documented
5. Update progress checklist

**Validation Gates**:
- [ ] At least 4 new axiom categories added
- [ ] Each new axiom includes usage example
- [ ] Axioms are testable and non-ambiguous
- [ ] Cross-references to related axioms documented

**Conflict Notes**: None - additive changes only

---

### Phase 3: Serena MCP Semantic Extraction

**Goal**: Validate axiom coverage by extracting real patterns from ctx-eng-plus

**Estimated Hours**: 2

**Complexity**: medium

**Files Modified**:
- `/migrations/cycle-1-serena-analysis.md` (new)
- `/patterns/axioms-v2.yaml` (if gaps found)

**Dependencies**: Phase 2, Serena MCP configured

**Implementation Steps**:
1. Identify 5-10 high-value patterns in ctx-eng-plus:
   - PRP execution pattern
   - Blend/merge pattern
   - Validation gate pattern
   - Migration strategy pattern
   - Progress tracking pattern
2. Use Serena MCP to extract semantic structure:
   ```bash
   # In Claude Code with Serena
   @ctx-eng-plus analyze patterns in tools/ce/
   ```
3. Map extracted structure to axioms:
   - Which axioms are used?
   - Which axioms are missing?
   - Are axioms sufficient for serialization?
4. Document gaps in `/migrations/cycle-1-serena-analysis.md`
5. Add missing axioms to `/patterns/axioms-v2.yaml`
6. Update progress checklist

**Validation Gates**:
- [ ] 5-10 real patterns analyzed
- [ ] Gaps documented with specific examples
- [ ] Missing axioms added and justified
- [ ] Serena analysis report complete

**Conflict Notes**: Requires Serena MCP access to ctx-eng-plus repo

---

### Phase 4: Build Validation Test Suite

**Goal**: Create comprehensive validation tests for every axiom

**Estimated Hours**: 3

**Complexity**: medium

**Files Modified**:
- `/validation/tests/test_axioms.py` (new)
- `/validation/tests/test_structural.py` (new)
- `/validation/tests/test_semantic.py` (new)
- `/validation/fixtures/sample-patterns.yaml` (new)

**Dependencies**: Phase 3

**Implementation Steps**:
1. Create test framework structure:
   ```
   /validation/
   ├── tests/
   │   ├── test_axioms.py       # Axiom compliance tests
   │   ├── test_structural.py   # Graph structure tests
   │   └── test_semantic.py     # Pattern semantics tests
   └── fixtures/
       └── sample-patterns.yaml # Test data
   ```
2. For each axiom, create validation test:
   - Positive case (valid pattern)
   - Negative case (violates axiom)
   - Edge case (boundary condition)
3. Implement structural validation:
   - Graph connectivity tests
   - Cycle detection tests
   - Orphan node detection
   - Schema compliance tests
4. Implement semantic validation:
   - Pattern consistency tests
   - Dependency satisfaction tests
   - Composition validity tests
   - Conflict detection tests
5. Create sample patterns for testing
6. Run full test suite, ensure all pass
7. Update progress checklist

**Validation Gates**:
- [ ] Every axiom has at least one test
- [ ] Structural validation covers all graph properties
- [ ] Semantic validation covers all pattern properties
- [ ] All tests pass with 100% success rate
- [ ] Test coverage documented in report

**Conflict Notes**: None - new test infrastructure

---

### Phase 5: Finalize Cycle 1

**Goal**: Complete documentation, update version, tag release

**Estimated Hours**: 1

**Complexity**: low

**Files Modified**:
- `/migrations/refinement-cycle-1-progress.md`
- `/CHANGELOG.md`
- `/VERSION`
- `/docs/pattern-catalog.md`

**Dependencies**: Phase 4

**Implementation Steps**:
1. Mark all tasks complete in progress checklist
2. Document key decisions and learnings
3. Update `/CHANGELOG.md` with Cycle 1 summary:
   - Axioms: X kept, Y revised, Z added
   - Validation: N tests, 100% pass rate
   - Gaps found and resolved
4. Bump `/VERSION` from 0.1.0 → 0.2.0
5. Update `/docs/pattern-catalog.md` with axiom references
6. Commit all changes
7. Tag release: `git tag v0.2.0 -m "Cycle 1: Axiom Hardening Complete"`
8. Push tag: `git push origin v0.2.0`

**Validation Gates**:
- [ ] Progress checklist shows 100% completion
- [ ] CHANGELOG accurately reflects changes
- [ ] VERSION file updated
- [ ] Git tag created and pushed
- [ ] All files committed

**Conflict Notes**: None - documentation and release tasks

---

## Execution Notes

### Prerequisites
- Serena MCP configured and accessible
- Access to ctx-eng-plus repository
- Python environment for validation tests

### Execution in Claude Code

```bash
# Load this PRP in Claude Code
@ce-framework-meta/docs/prp-templates/PRP-META-001-cycle-1-axiom-hardening.md

# Claude will execute phases sequentially
# Monitor progress in /migrations/refinement-cycle-1-progress.md
```

### Time Budget
Total: 11 hours over 3-5 days

### Risk Mitigation
- **Risk**: Serena extraction fails
  - **Mitigation**: Manual pattern analysis fallback
- **Risk**: Validation tests fail
  - **Mitigation**: Revise axioms, not tests
- **Risk**: Scope creep (too many axioms)
  - **Mitigation**: Time-box to 11 hours, defer extras to Cycle 3

---
