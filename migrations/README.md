# Migrations

Migration stage definitions and utilities.

## Migration Stages

See [migration-stages.yaml](migration-stages.yaml) for complete stage definitions.

### Stage 1: Foundation (v1.0.0)
- Coverage: 20-30%
- Focus: Schema design, initial patterns, validation framework
- Duration: 4 weeks

### Stage 2: Expansion (v1.1.0)  
- Coverage: 60-70%
- Focus: Refinement, extended patterns, quality metrics
- Duration: 6 weeks

### Stage 3: Complete (v2.0.0)
- Coverage: 95-100%
- Focus: Full migration, production hardening, meta-governance
- Duration: 6 weeks

## Migration Scripts

Utility scripts in `scripts/`:
- Pattern converters (legacy → graph)
- Validation runners
- Report generators
- Rollback utilities

## Migration Tracking

Each implementation tracks its migration progress:
```yaml
current_stage: stage-1-foundation
coverage: 25%
last_sync: 2025-11-13
validation_status: passing
```
