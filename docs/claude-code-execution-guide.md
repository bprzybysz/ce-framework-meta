# Claude Code Execution Guide

## Overview
This guide provides step-by-step instructions for executing the CE Framework Meta refinement cycles in Claude Code.

## Prerequisites
- Claude Code with GitHub MCP configured
- Access to repository: `bprzybysz/ce-framework-meta`
- Serena MCP installed (optional but recommended)
- Context7 MCP installed (optional for documentation)

## Execution Workflow

### Phase 1: Setup & Context Loading

1. **Clone/Open Repository**
   ```bash
   git clone https://github.com/bprzybysz/ce-framework-meta.git
   cd ce-framework-meta
   ```

2. **Load Context in Claude Code**
   - Open the repository in Claude Code
   - Run: `/context` to load repository context
   - Review: `README.md`, `migrations/refinement-cycle-1-definition.md`

3. **Set Up Serena MCP (if available)**
   ```bash
   # Serena will auto-index the codebase
   # Use: mcp__serena__think_about_collected_information
   ```

### Phase 2: Execute Refinement Cycle 1

1. **Load PRP-1**
   - Read: `prps/PRP-1-axiom-hardening.md`
   - Understand all tasks and acceptance criteria

2. **Execute Tasks Sequentially**
   ```
   For each task in PRP-1:
     1. Read task requirements
     2. Execute task (review, create, update files)
     3. Commit changes with descriptive message
     4. Update progress in refinement-cycle-1-progress.md
     5. Move to next task
   ```

3. **Example Task Execution (Task 1: Review Axioms)**
   ```
   Prompt to Claude Code:
   "Review /patterns/axioms-v1.yaml and triage each axiom as KEEP/REVISE/DROP.
   Document your reasoning in /migrations/cycle-1-axiom-review.md.
   Update the progress tracker when complete."
   ```

4. **Validation Checkpoint**
   - After completing all tasks, run validation
   - Ensure all acceptance criteria met
   - Update `refinement-cycle-1-progress.md` to 100%

5. **Version Bump & Commit**
   ```bash
   # Update VERSION file to v1.0.1
   # Update CHANGELOG.md with cycle 1 summary
   git add .
   git commit -m "Complete Refinement Cycle 1: Axiom Hardening"
   git tag v1.0.1
   git push origin main --tags
   ```

### Phase 3: Execute Refinement Cycle 2

1. **Verify Cycle 1 Complete**
   - Check: Version = `v1.0.1`
   - Check: All Cycle 1 tasks complete

2. **Load PRP-2**
   - Read: `prps/PRP-2-pattern-serialization.md`
   - Create progress tracker: `refinement-cycle-2-progress.md`

3. **Execute Tasks Sequentially**
   - Follow same pattern as Cycle 1
   - Pay special attention to automation tasks
   - Run validation after each batch of patterns

4. **Version Bump & Commit**
   ```bash
   # Update VERSION file to v1.1.0
   # Update CHANGELOG.md with cycle 2 summary
   git add .
   git commit -m "Complete Refinement Cycle 2: Pattern Serialization Sprint"
   git tag v1.1.0
   git push origin main --tags
   ```

### Phase 4: Reporting & Handoff

1. **Create Summary Report**
   - Compile metrics from both cycles
   - Document lessons learned
   - Identify items for future cycles

2. **Prepare for Implementation Teams**
   - Create integration guide
   - Document how to consume meta-framework
   - Provide examples

## Best Practices for Claude Code

### Context Management
- Use `/clear` to reset context between major tasks
- Use `/context` to reload repository state
- Reference specific files explicitly when needed

### Commit Strategy
- Commit after each major task completion
- Use conventional commit messages
- Tag versions at cycle completion

### Validation Gates
- Run validation after each batch of changes
- Don't proceed if validation fails
- Document all validation failures

### Error Handling
- Log all errors in migration documents
- Don't skip errors - fix or ticket them
- Update error rate metrics

## MCP Tool Usage

### GitHub MCP
```
# Create/update files
mcp__github__create_or_update_file

# List files in directory
mcp__github__get_file_contents

# Commit changes
mcp__github__push_files
```

### Serena MCP (if available)
```
# Extract pattern semantics
mcp__serena__think_about_collected_information

# Query codebase structure
mcp__serena__query_codebase
```

### Context7 MCP (if available)
```
# Fetch documentation
mcp__context7__fetch_docs
```

## Troubleshooting

### Issue: Can't find pattern definitions
- Solution: Check if ctx-eng-plus repo exists and is accessible
- Fallback: Create sample patterns manually for testing

### Issue: Validation fails
- Solution: Review validation rules in `/ontology/validation.yaml`
- Check: Schema matches axiom requirements
- Fix: Update schemas or axioms as needed

### Issue: Serialization errors
- Solution: Check `/migrations/cycle-2-serialization-errors.md`
- Debug: Run serialization on single pattern first
- Fix: Update serialization logic in `/tools/serialize-patterns.py`

## Next Steps After Completion
- Execute PRP-3 (if defined) for Cycle 3
- Integrate with concrete implementation repos
- Deploy graph database for production use
- Create API for pattern querying
