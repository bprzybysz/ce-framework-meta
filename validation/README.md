# Validation

Validation rules and test cases for pattern graph integrity.

## Validation Types

### Structural Validation
- Graph connectivity
- Cycle detection
- Orphan node detection
- Schema compliance

### Semantic Validation  
- Dependency satisfaction
- Composition validity
- Constraint compliance
- Pattern consistency

### Quality Validation
- Cohesion metrics
- Coupling analysis
- Reusability scores
- Complexity measures

## Rule Format

```yaml
rule-id: unique-rule-id
name: Rule Name
type: structural|semantic|quality
severity: error|warning|info
description: |
  Rule description
condition:
  # Rule logic
action:
  - fail|warn|report
```

## Test Cases

Validation test fixtures in `test-cases/`:
- Valid pattern graphs (should pass)
- Invalid patterns (should fail with specific errors)
- Edge cases and boundary conditions
