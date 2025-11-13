# Axiom-Schema Mapping

**Date:** 2025-11-13
**Status:** Initial mapping

This document connects each refined axiom (from `patterns/axioms-v1.yaml`) to explicit schema fields in:
- [`schemas/pattern-schema.json`](https://github.com/bprzybysz/ce-framework-meta/blob/main/schemas/pattern-schema.json)
- [`schemas/edge-schema.json`](https://github.com/bprzybysz/ce-framework-meta/blob/main/schemas/edge-schema.json)

---

## Mapping Table

| Axiom | Maps to Pattern Schema | Maps to Edge Schema | Notes |
|-------|------------------------|---------------------|-------|
| Unique ID, name, description | `id`, `name`, `description` | — | Make `description` required |
| Node serialization, axiom/constraint metadata | `axioms`, `constraints` | — | Complete |
| Explicit edge relationships (DEPENDS_ON, ...) | `relationships` | `type` | Enum in edge schema covers all |
| KISS, DRY, SOLID principles | `name`, `constraints`, `relationships` | `meta` | Implementation best practices |
| Meta info isolation | `axioms`, `constraints` | — | Docs + governance |
| Serialization matches schemas | N/A (implicit) | N/A | Validation prerequisite |
| Semantic versioning | `version` | — | Schema required field |
| Migration reflexivity, stage governance | `version` | — | Documented in migrations |
| Temporal edge constraints | — | `meta` (`valid_from`, `valid_until`) | Add examples in edge schema |
| Acyclic COMPOSES, EXTENDS, etc. | `relationships` | `type`/`meta` | Validation rules |
| Validation before commit | All fields | All fields | Validation logic in YAML |

---

### Required Schema Adjustments
1. **Make `description` required** in `pattern-schema.json`
2. **Add temporal fields (`valid_from`, `valid_until`)** to `edge-schema.json` examples and docs

---

## Next Steps
- Update schemas as documented
- Proceed to create validation rules
- Document artifacts in progress log

**Review:** All axioms map to explicit schema elements or validation practices; two identified for schema enhancement.