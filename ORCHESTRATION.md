# Orchestration Layer

This repository (`ce-framework-meta`) provides the **meta framework** for Context Engineering v2.0.

For **active work execution and pattern implementations**, see:

## 🔗 [perplexity-space-context](https://github.com/bprzybysz/perplexity-space-context)

The orchestration repository provides:

- **Work Tracking**: Active refinement cycles and progress
- **Pattern Implementations**: Serialized patterns following this framework
- **Quick Reference**: Framework schemas and axiom summaries
- **Execution Context**: PRP execution tracking and artifacts

## Repository Relationship

```
perplexity-space-context/     ← Orchestration & Execution
├── meta/ → references ce-framework-meta
├── patterns/                   ← Pattern implementations
└── work/                       ← Active cycles

ce-framework-meta/            ← Framework Definition (THIS REPO)
├── schemas/                    ← Authoritative schemas
├── patterns/                   ← Framework patterns & axioms
├── prps/                       ← Product Requirements Prompts
└── docs/                       ← Framework documentation
```

## Current Work

**Cycle 1: Axiom Hardening** - IN PROGRESS  
See: [perplexity-space-context/work/cycle-1](https://github.com/bprzybysz/perplexity-space-context/tree/main/work/cycle-1)

**Task 1**: ✅ Complete - [Axiom Review](migrations/cycle-1-axiom-review.md)  
**Task 2**: 🔄 In Progress - Update axioms-v1.yaml

## Integration with Perplexity Space

The orchestration repository aligns with the **Context Engineering v2.0** Space instructions:

```
SOURCE: GitHub perplexity-space-context repo (meta/, patterns/, work/)
PRINCIPLES: KISS, SOLID, YAGNI
PROCESS: Review repo state → Apply validation → Generate next steps
```

## Usage

1. **Framework Changes**: Update this repo (ce-framework-meta)
2. **Pattern Work**: Update orchestration repo (perplexity-space-context)
3. **Cross-Reference**: Both repos link to each other

---

**Last Updated**: 2025-11-13