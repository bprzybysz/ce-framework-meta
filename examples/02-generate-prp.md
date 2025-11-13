# Example 2: Generating PRPs from Plans

This example shows how to quickly generate PRPs from high-level plans using the CE framework meta patterns.

## Scenario: Implement Rollback Feature

You have a high-level plan to implement a rollback feature for pattern migrations. Let's convert this to a structured PRP.

### Step 1: Write High-Level Plan

```markdown
# Plan: Implement Pattern Migration Rollback

Goal: Allow reverting pattern migrations to previous states

Requirements:
- Snapshot pattern state before migration
- Store snapshot with version metadata
- Provide rollback command
- Validate rollback preserves graph integrity

Phases:
1. Design snapshot format
2. Implement snapshot creation
3. Implement rollback logic
4. Add validation tests
5. Document usage
```

### Step 2: Use PRP Template Pattern

The CE framework meta includes a PRP template pattern:

```python
# tools/generate_prp.py
from ce_meta.patterns import load_pattern
from ce_meta.prp import PRPGenerator

def generate_prp_from_plan(plan_text, pattern_id):
    """Generate PRP from plan using template pattern."""
    
    # Load PRP template pattern
    template = load_pattern("patterns/meta/prp-template.yaml")
    
    # Parse plan
    plan = parse_plan(plan_text)
    
    # Generate PRP using pattern
    generator = PRPGenerator(template)
    prp = generator.generate(
        title=plan.title,
        overview=plan.goal,
        success_criteria=plan.requirements,
        phases=plan.phases
    )
    
    return prp

def parse_plan(text):
    """Parse high-level plan text."""
    lines = text.split("\n")
    plan = {
        "title": extract_title(lines),
        "goal": extract_goal(lines),
        "requirements": extract_requirements(lines),
        "phases": extract_phases(lines)
    }
    return plan
```

### Step 3: Generate PRP Structure

Run the generator:

```bash
# In Claude Code
python tools/generate_prp.py \
  --plan plans/rollback-feature.md \
  --output docs/prp-templates/PRP-META-003-rollback-feature.md
```

Generated PRP:

```markdown
# PRP-META-003: Pattern Migration Rollback

## Overview

Implement rollback capability for pattern migrations, allowing
reversion to previous pattern states while maintaining graph integrity.

## Success Criteria

- [ ] Snapshot format designed and documented
- [ ] Snapshot creation implemented
- [ ] Rollback logic implemented and tested
- [ ] Graph integrity validated after rollback
- [ ] Usage documentation complete

## Phases

### Phase 1: Design Snapshot Format

**Goal**: Define JSON schema for pattern state snapshots

**Estimated Hours**: 2

**Complexity**: low

**Files Modified**:
- `/schemas/snapshot-schema.json` (new)

**Implementation Steps**:
1. Define snapshot metadata fields:
   - timestamp, version, migration_id, author
2. Define pattern state capture:
   - nodes: array of pattern nodes
   - edges: array of pattern edges
   - validation_state: test results
3. Create JSON schema
4. Add schema validation tests

**Validation Gates**:
- [ ] Schema is valid JSON Schema format
- [ ] All metadata fields documented
- [ ] Validation tests pass

### Phase 2: Implement Snapshot Creation

**Goal**: Create snapshot before each migration

**Estimated Hours**: 3

**Complexity**: medium

**Files Modified**:
- `/tools/snapshot.py` (new)
- `/tools/migrate.py` (modify)

**Implementation Steps**:
1. Create SnapshotManager class
2. Implement create_snapshot(migration_id):
   - Query current graph state
   - Serialize to snapshot format
   - Save to /migrations/snapshots/
3. Integrate with migration workflow:
   - Call create_snapshot before migration
   - Store snapshot reference in migration log
4. Add snapshot tests

**Validation Gates**:
- [ ] Snapshots created successfully
- [ ] Snapshot contains complete graph state
- [ ] Tests validate snapshot integrity

### Phase 3: Implement Rollback Logic

**Goal**: Restore pattern state from snapshot

**Estimated Hours**: 4

**Complexity**: high

**Files Modified**:
- `/tools/rollback.py` (new)

**Implementation Steps**:
1. Create RollbackManager class
2. Implement rollback(snapshot_id):
   - Load snapshot from file
   - Validate snapshot integrity
   - Clear current graph state
   - Restore nodes and edges from snapshot
   - Run validation suite
3. Add rollback command to CLI:
   ```bash
   ce-meta rollback --snapshot <id>
   ```
4. Add rollback tests

**Validation Gates**:
- [ ] Rollback restores exact prior state
- [ ] Graph integrity maintained
- [ ] Validation suite passes post-rollback

### Phase 4: Add Validation Tests

**Goal**: Comprehensive testing of rollback feature

**Estimated Hours**: 2

**Complexity**: medium

**Files Modified**:
- `/validation/tests/test_rollback.py` (new)

**Implementation Steps**:
1. Test snapshot creation
2. Test rollback to previous state
3. Test rollback after failed migration
4. Test multiple consecutive rollbacks
5. Test snapshot cleanup

**Validation Gates**:
- [ ] All test scenarios pass
- [ ] Edge cases covered

### Phase 5: Document Usage

**Goal**: Complete user documentation

**Estimated Hours**: 1

**Complexity**: low

**Files Modified**:
- `/docs/rollback-guide.md` (new)
- `/README.md` (update)

**Implementation Steps**:
1. Write rollback guide with examples
2. Document snapshot format
3. Add troubleshooting section
4. Update README with rollback feature

**Validation Gates**:
- [ ] Documentation complete and clear
- [ ] Examples tested and working

---
```

### Step 4: Refine and Customize

The generated PRP provides 80% of the structure. Customize as needed:

```markdown
# Manual refinements:
- Add specific file paths
- Adjust time estimates based on complexity
- Add dependencies between phases
- Customize validation gates
- Add risk mitigation notes
```

### Step 5: Execute in Claude Code

Load and execute the PRP:

```bash
# In Claude Code
@ce-framework-meta/docs/prp-templates/PRP-META-003-rollback-feature.md

# Claude Code will:
# 1. Parse PRP structure
# 2. Execute phases sequentially
# 3. Validate success criteria
# 4. Update progress tracking
# 5. Commit changes
```

## Speed Benefits

Using PRP generation patterns:
- **Manual PRP creation**: 2-3 hours
- **Generated PRP with refinement**: 30 minutes
- **Time saved**: 75-85%

The pattern ensures:
- Consistent structure
- Complete success criteria
- Proper phase breakdown
- Built-in validation gates
- Progress tracking

## Summary

This example demonstrated:
1. Writing a high-level plan
2. Using PRP template pattern to generate structure
3. Automatic phase and validation gate creation
4. Refining generated PRP for specific needs
5. Executing PRP in Claude Code

Next: See Example 3 for pattern composition and conflict detection.
