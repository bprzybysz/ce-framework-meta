# Example 1: Defining a New Pattern

This example shows how to define a new pattern using the CE framework meta axioms and schemas.

## Pattern: Observer (Behavioral)

The Observer pattern is a behavioral design pattern that defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

### Step 1: Define Pattern Metadata

Using the pattern schema from `/schemas/pattern-schema.json`:

```yaml
# patterns/behavioral/observer.yaml
id: "pattern:behavioral:observer"
name: "Observer Pattern"
description: |
  Behavioral pattern for event-driven state propagation.
  Defines subscription-based notification system where
  observers register with subject and receive updates.
  
axioms:
  - "Every pattern must have a unique ID, name, description"
  - "Patterns explicitly define relationships"
  - "Patterns can be versioned and reflexively migrated"
  - "Relationships and constraints are validated on each refinement cycle"
  
version: "1.0.0"

relationships:
  - "EXTENDS:pattern:behavioral:base"
  - "DEPENDS_ON:pattern:structural:interface"
  - "CONFLICTS_WITH:pattern:behavioral:mediator"
  
constraints:
  - "Observers must implement update() method"
  - "Subject maintains list of observers"
  - "Notification is one-way (subject → observers)"
  - "Observers are loosely coupled to subject"

meta:
  category: behavioral
  complexity: medium
  use_cases:
    - "Event-driven systems"
    - "Agentic state propagation"
    - "Pub-sub messaging"
  tags:
    - event-driven
    - decoupling
    - notification
```

### Step 2: Validate Against Axioms

Check that the pattern complies with all axioms:

```python
# validation/tests/test_observer_pattern.py
import pytest
from ce_meta.validation import validate_pattern
from ce_meta.patterns import load_pattern

def test_observer_pattern_axioms():
    pattern = load_pattern("patterns/behavioral/observer.yaml")
    
    # Axiom: Every pattern must have unique ID, name, description
    assert pattern.id == "pattern:behavioral:observer"
    assert pattern.name == "Observer Pattern"
    assert pattern.description is not None
    
    # Axiom: Patterns explicitly define relationships
    assert len(pattern.relationships) > 0
    assert any("EXTENDS" in r for r in pattern.relationships)
    
    # Axiom: Patterns can be versioned
    assert pattern.version == "1.0.0"
    
    # Axiom: Relationships validated
    errors = validate_pattern(pattern)
    assert len(errors) == 0
```

### Step 3: Serialize to Graph

Generate graph nodes and edges:

```python
# tools/serialize_pattern.py
from ce_meta.patterns import load_pattern
from ce_meta.graph import PatternNode, PatternEdge
import json

def serialize_pattern(pattern_path, output_dir):
    """Serialize pattern to graph format."""
    pattern = load_pattern(pattern_path)
    
    # Create node
    node = PatternNode(
        id=pattern.id,
        name=pattern.name,
        description=pattern.description,
        axioms=pattern.axioms,
        version=pattern.version,
        constraints=pattern.constraints,
        meta=pattern.meta
    )
    
    # Create edges
    edges = []
    for rel in pattern.relationships:
        rel_type, target = rel.split(":" 1)
        edge = PatternEdge(
            source=pattern.id,
            target=target,
            type=rel_type,
            meta={"version": pattern.version}
        )
        edges.append(edge)
    
    # Save to JSON
    with open(f"{output_dir}/nodes/{pattern.id}.json", "w") as f:
        json.dump(node.to_dict(), f, indent=2)
    
    for i, edge in enumerate(edges):
        with open(f"{output_dir}/edges/{pattern.id}_edge_{i}.json", "w") as f:
            json.dump(edge.to_dict(), f, indent=2)

# Usage
serialize_pattern(
    "patterns/behavioral/observer.yaml",
    "migrations/generated-nodes"
)
```

### Step 4: Import to Neo4j

```cypher
// Load observer pattern node
CALL apoc.load.json('file:///migrations/generated-nodes/nodes/pattern:behavioral:observer.json')
YIELD value
CREATE (p:Pattern:Behavioral)
SET p = value

// Load observer pattern edges
CALL apoc.load.json('file:///migrations/generated-nodes/edges/pattern:behavioral:observer_edge_0.json')
YIELD value
MATCH (s:Pattern {id: value.source})
MATCH (t:Pattern {id: value.target})
CREATE (s)-[r:EXTENDS]->(t)
SET r.meta = value.meta

// Verify
MATCH (p:Pattern {id: "pattern:behavioral:observer"})-[r]->(t)
RETURN p.name, type(r), t.name
```

### Step 5: Validate in Graph

Query to validate pattern relationships:

```cypher
// Check all constraints satisfied
MATCH (p:Pattern {id: "pattern:behavioral:observer"})
WHERE size(p.constraints) > 0
RETURN p.name, p.constraints

// Check no conflicting patterns used together
MATCH (p1:Pattern {id: "pattern:behavioral:observer"})
     -[:CONFLICTS_WITH]->
     (p2:Pattern)
WHERE exists((p1)<-[:USES]-(:Implementation)-[:USES]->(p2))
RETURN "Conflict detected", p1.name, p2.name

// Should return no rows if valid
```

## Summary

This example demonstrated:
1. Defining a pattern using YAML and axioms
2. Validating pattern against axiom rules
3. Serializing pattern to graph format (JSON)
4. Importing to Neo4j graph database
5. Validating pattern relationships in graph

Next: See Example 2 for pattern migration workflow.
