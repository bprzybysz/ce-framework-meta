# Changelog

All notable changes to the CE Framework Meta repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2025-11-13

### Added
- Enhanced pattern axioms (v1.1) with detailed core axioms and derived principles
- Comprehensive pattern and edge schemas (v1.1) with metadata and validation support
- Structural validation rules (STR-001 to STR-006)
- Semantic validation rules (SEM-001 to SEM-006)
- Quality validation rules (QL-001 to QL-005)
- Relationship ontology with all five edge types and derived queries
- Global and pattern-specific constraints
- Initial pattern catalog: repository-pattern and observer-pattern
- Pattern catalog documentation with serialization format and validation info
- Version tracking and changelog

### Changed
- Refined axioms from simple list to structured categories with rationale
- Enhanced schemas with metadata, lifecycle, and migration fields
- Improved pattern serialization format with comprehensive metadata

### Migration Notes
- This is the first refinement cycle (Cycle 1)
- Patterns now require compliance with axioms v1.1
- All new patterns must validate against schemas v1.1

## [1.0.0] - 2025-11-13

### Added
- Initial repository structure
- Basic pattern axioms (v1.0)
- Simple pattern and edge schemas
- Migration stage 1 instructions
- README and .gitignore

[1.1.0]: https://github.com/bprzybysz/ce-framework-meta/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/bprzybysz/ce-framework-meta/releases/tag/v1.0.0
