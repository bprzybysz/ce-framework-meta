# Patterns

Pattern definitions organized by category.

## Categories

### Structural Patterns
Patterns defining system structure and organization.
- Component patterns
- Architecture patterns
- Module patterns

### Behavioral Patterns  
Patterns defining system behavior and interactions.
- Workflow patterns
- State patterns
- Event patterns

### Integration Patterns
Patterns for system integration and communication.
- API patterns
- Data flow patterns
- Protocol patterns

### Meta Patterns
Higher-order patterns and compositions.
- Pattern compositions
- Pattern transformations
- Pattern generators

## Pattern Format

Each pattern is defined in YAML with the following structure:

```yaml
id: pattern-unique-id
name: Pattern Name
category: structural|behavioral|integration|meta
version: 1.0.0
description: |
  Detailed pattern description
metadata:
  author: name
  created: 2025-11-13
  tags: [tag1, tag2]
structure:
  nodes:
    - id: node1
      type: component
  edges:
    - from: node1
      to: node2
      type: DEPENDS_ON
validation:
  rules:
    - rule-id-1
    - rule-id-2
examples:
  - path: examples/example1.md
```

## Migration Status

- ⬜ Not started
- 🟡 In progress  
- ✅ Migrated
- ✔️ Validated
