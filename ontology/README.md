# Ontology

Formal ontology definitions for the CE Framework.

## Files

### pattern-ontology.ttl
RDF/OWL ontology defining:
- Pattern classes and hierarchies
- Properties and relationships  
- Constraints and axioms

### relationships.yaml
Edge type definitions:
```yaml
DEPENDS_ON:
  description: "Pattern A depends on pattern B"
  transitive: true
  properties:
    - strength: [weak, moderate, strong]
```

### constraints.yaml  
Global constraints:
- Cycle detection rules
- Composition limits
- Validation thresholds

## Ontology Version

Ontology evolves with schema versions but maintains backward compatibility where possible.
