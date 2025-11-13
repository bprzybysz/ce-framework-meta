# Quick Start: Execute in Claude Code

## Ready to Execute

Everything needed for Claude Code execution is now in place. Follow these steps:

### 1. Open in Claude Code

```bash
git clone https://github.com/bprzybysz/ce-framework-meta.git
cd ce-framework-meta
# Open in Claude Code
```

### 2. Execute Cycle 1 (Axiom Hardening)

**Prompt to Claude Code:**
```
Read and execute PRP-1: Axiom Hardening

File: /prps/PRP-1-axiom-hardening.md

Follow all tasks sequentially:
1. Review axioms in /patterns/axioms-v1.yaml
2. Add missing edge-case axioms
3. Validate schemas
4. Create validation rules
5. Test with sample patterns

Update progress in /migrations/refinement-cycle-1-progress.md after each task.
Commit changes incrementally.

When complete:
- Bump VERSION to v1.0.1
- Update CHANGELOG.md
- Tag release
```

### 3. Execute Cycle 2 (Pattern Serialization)

**After Cycle 1 is complete, prompt:**
```
Read and execute PRP-2: Pattern Serialization Sprint

File: /prps/PRP-2-pattern-serialization.md

Prerequisite: Verify Cycle 1 complete (VERSION = v1.0.1)

Follow all tasks sequentially:
1. Create pattern inventory
2. Build serialization tooling
3. Serialize 60-70% of patterns
4. Run validation suite
5. Calculate and document metrics

Update progress in /migrations/refinement-cycle-2-progress.md after each task.
Commit changes incrementally.

When complete:
- Bump VERSION to v1.1.0
- Update CHANGELOG.md
- Tag release
```

## What's Included

✅ **PRPs (Product Requirements Prompts)**
- `/prps/PRP-1-axiom-hardening.md` - Detailed cycle 1 tasks
- `/prps/PRP-2-pattern-serialization.md` - Detailed cycle 2 tasks

✅ **Execution Guides**
- `/docs/claude-code-execution-guide.md` - Complete execution workflow
- `/docs/framework-usage-examples.md` - Code examples and patterns

✅ **Foundation**
- `/patterns/axioms-v1.yaml` - Initial axioms (ready for refinement)
- `/schemas/pattern-schema.json` - Pattern node schema
- `/schemas/edge-schema.json` - Relationship edge schema
- `/patterns/catalog-draft.md` - Agentic patterns catalog

✅ **Progress Tracking**
- `/migrations/refinement-cycle-1-progress.md` - Cycle 1 checklist
- `/migrations/refinement-cycle-1-definition.md` - Cycle 1 boundaries
- `/migrations/stage-1-instructions.md` - Overall stage instructions

✅ **Version Control**
- `/VERSION` - Current version (0.1.0)
- `/CHANGELOG.md` - All changes documented

## MCP Tools to Use

### GitHub MCP (Required)
```
mcp__github__get_file_contents - Read files
mcp__github__create_or_update_file - Update files
mcp__github__push_files - Commit multiple files
```

### Serena MCP (Recommended)
```
mcp__serena__think_about_collected_information - Extract pattern semantics
mcp__serena__query_codebase - Analyze structure
```

### Context7 MCP (Optional)
```
mcp__context7__fetch_docs - Get external documentation
```

## Expected Outcomes

### After Cycle 1 (v1.0.1)
- ✅ All axioms reviewed and finalized
- ✅ Schemas validated and complete
- ✅ Validation rules implemented
- ✅ Sample patterns tested
- ✅ Documentation updated

### After Cycle 2 (v1.1.0)
- ✅ 60-70% patterns serialized
- ✅ <3% validation error rate
- ✅ Serialization tooling ready
- ✅ Metrics documented
- ✅ Ready for Cycle 3

## Time Estimates

- **Cycle 1**: 2-4 hours (with Claude Code)
- **Cycle 2**: 3-5 hours (with automation)
- **Total**: 5-9 hours for foundation

Compare to manual: 20-30 hours
**Time saved: 60-70%**

## Support

Refer to:
- `/docs/claude-code-execution-guide.md` - Detailed execution steps
- `/docs/framework-usage-examples.md` - Code examples
- `/migrations/` - All migration documentation

## Ready?

**Start now with:**
```
Claude Code, execute PRP-1 from /prps/PRP-1-axiom-hardening.md
```
