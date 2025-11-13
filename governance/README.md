# Governance

Governance model for the CE Framework Meta repository.

## Pattern Lifecycle

Patterns progress through defined states:

1. **Draft** - Initial pattern definition, work in progress
2. **Review** - Submitted for community review
3. **Approved** - Accepted into framework, ready for use
4. **Deprecated** - Marked for removal, use discouraged

## Change Process

### Minor Changes (Patches, Documentation)
- Direct PR to main branch
- Single reviewer approval required
- Automated tests must pass

### Schema Changes (Minor Version)
- RFC (Request for Comments) issue required
- 3 business days for community feedback
- Two reviewer approvals required
- Backward compatibility maintained

### Breaking Changes (Major Version)
- Formal RFC with migration plan
- 2 weeks for community feedback
- Consensus from 3+ maintainers
- Deprecation timeline (2 versions minimum)
- Migration tooling provided

## Approval Workflow

```yaml
workflow:
  pattern_proposal:
    - create_issue: "Pattern Proposal"
    - community_discussion: 5 days
    - prototype: optional
    - vote: maintainers
    - merge: if approved
  
  schema_change:
    - create_rfc: "RFC: Schema Change"
    - impact_analysis: required
    - migration_plan: required
    - community_review: 2 weeks
    - implementation: after approval
```

## Deprecation Policy

### Timeline
1. **Announcement** - Mark as deprecated, document replacement
2. **Version N** - Deprecation warnings in validation
3. **Version N+1** - Still available, warnings increase
4. **Version N+2** - Removed from framework

### Requirements
- Clear migration path documented
- Automated migration tooling if possible
- Advance notice in CHANGELOG
- Backward compatibility maintained through N+1

## Maintainer Responsibilities

- Review PRs within 3 business days
- Maintain CHANGELOG and VERSION
- Run validation suite before releases
- Respond to issues within 5 business days
- Facilitate community discussions
- Ensure documentation quality

## Community Guidelines

- Be respectful and constructive
- Provide clear rationale for proposals
- Test changes thoroughly
- Document patterns comprehensively
- Help others understand the framework

## Release Process

1. Update VERSION file
2. Update CHANGELOG.md
3. Run full validation suite
4. Create git tag `vX.Y.Z`
5. Generate release notes
6. Publish to package registry (if applicable)
7. Notify implementation repositories
