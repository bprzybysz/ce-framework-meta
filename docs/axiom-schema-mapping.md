# Axiom-Schema Mapping

**Date:** 2025-11-13
**Purpose:** Explicit mapping of refined axioms to schema fields in pattern-schema.json and edge-schema.json

## Mapping Table

| Axiom                                                                                                                                                                                    | Pattern Node Field                  | Edge Field / Meta               | Validation Note                        |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|----------------------------------|-----------------------------------------|
| Every pattern must have a unique ID, name, description.                                                                                           | id, name, description               |                                  | Required, uniqueness enforced           |
| Patterns are serializable as nodes with axiom and constraint metadata.                                                                            | axioms, constraints                 |                                  | Lists in node metadata                  |
| Patterns explicitly define relationships: DEPENDS_ON, COMPOSES, EXTENDS, VALIDATES, CONFLICTS_WITH.                                               | relationships                       | type (enum)                      | Edge schema enforces relationship types |
| Patterns must use semantic versioning (MAJOR.MINOR.PATCH).                                                 | version                             |                                  | Required format, validated              |
| Pattern migrations must be reversible (forward/rollback).                                                   | version, migration                  |                                  | History documented by version           |
| Meta information (not implementation) must be isolated in this repo.                                         | description, meta                   | meta (object)                    | Repo governance                         |
| Serialization of patterns follows schemas in /schemas/.                                                     | all fields                          | all fields                       | Schema validation required              |
| Patterns must follow KISS principle.                                                                        | id, name, axioms, constraints       |                                  | Minimal viable serialization            |
| Patterns must respect DRY principle.                                                                        | constraints (references)            | meta (references)                | Duplicate data flagged                  |
| Patterns must embody SOLID principles.                                                                      | name, constraints, relationships    | type, meta                       | Field design mapped to principles       |
| Relationships can have temporal constraints (valid_from, valid_until).                                      |                                     | meta.valid_from, meta.valid_until| Temporal metadata required              |
| COMPOSES relationships must form acyclic directed graph (no circular composition).                          | relationships                       | type: COMPOSES                   | Graph traversal for cycle check         |
| EXTENDS relationships must preserve base pattern constraints.                                               | constraints, relationships          | type: EXTENDS                    | Constraint inheritance validated        |
| CONFLICTS_WITH relationships must be symmetric (bidirectional).                                             | relationships                       | type: CONFLICTS_WITH              | Validator for symmetry                  |
| DEPENDS_ON relationships must resolve to existing pattern nodes.                                            | relationships                       | type: DEPENDS_ON                  | Existential check enforced              |
| Migration stages must define: scope, entry criteria, exit criteria, success metrics.                        | migration, version                  |                                  | Tracked in /migrations/                 |
| Stage transitions require validation suite pass (zero critical errors).                                      |                                     |                                  | Exit criteria enforced                  |
| Rollback procedures must be documented for each stage.                                                      | migration, version                  |                                  | Tracked in /migrations/                 |
| Stage progress tracked in /migrations/ with version-tagged artifacts.                                       | migration, version                  |                                  | Artifacts linked to version             |
