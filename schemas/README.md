# Schemas

Versioned schema definitions for the CE Framework graph representation.

## Schema Versioning

Each major/minor version has its own directory:
- `v1.0/` - Initial graph schema (Cycle 1)
- `v1.1/` - Refined schema (Cycle 2)  
- `v2.0/` - Production schema (Cycle 3)

## Schema Types

### Pattern Schema
Defines the structure of pattern nodes in the graph.

### Edge Schema  
Defines relationship types and their properties.

### Meta-Pattern Schema
Defines composition patterns and meta-level constructs.

### Validation Schema
Defines validation rule structure and constraints.

## Schema Evolution

**Breaking Changes:** Require new major version  
**Additive Changes:** Can be minor version bump  
**Bug Fixes:** Patch version only

See [schema-evolution.md](../docs/schema-evolution.md) for details.
