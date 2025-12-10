# Post-PR Review Instructions

## Purpose

This document provides a standardized checklist for agents to follow after a Pull Request has been reviewed, approved, and merged. These steps ensure proper cleanup, documentation, and project maintenance.

## When to Use

Execute this workflow **after**:

- Pull Request has been reviewed
- All feedback has been addressed
- PR has been merged to the main branch
- CI/CD pipeline has completed successfully

## Standard Post-Merge Checklist

### 1. Archive Tracking Files

**Action**: Move completed tracking files to archive.

```bash
# Move tracking file to archived directory
mv .copilot-tracking/issue-{ID}-{description}.md .copilot-tracking/archived/

# Update status in archived file
# Change status to: complete
# Add completed: YYYY-MM-DD field
```

**Verify**:

- File moved to `.copilot-tracking/archived/`
- YAML frontmatter updated with `status: complete`
- Completion date recorded

### 2. Update Documentation

**Action**: Ensure all relevant documentation reflects the changes.

**Common Documentation to Review**:

- [ ] README.md - Updated if features/setup changed
- [ ] CHANGELOG.md - Entry added for this change
- [ ] API documentation - Updated if interfaces changed
- [ ] Architecture docs - Updated if structure changed
- [ ] User guides - Updated if user-facing changes
- [ ] Configuration examples - Updated if settings changed

**Guidelines**:

- Be specific about what changed
- Include version numbers where applicable
- Link to related issues or PRs
- Update any diagrams or visual documentation

### 3. Tag Releases (If Applicable)

**Action**: Create version tags for significant releases.

**When to Tag**:

- Feature releases (minor version bump)
- Bug fix collections (patch version bump)
- Breaking changes (major version bump)
- Milestone completions

**Semantic Versioning**:

- `MAJOR.MINOR.PATCH` (e.g., `v1.2.3`)
- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes (backward compatible)

**Process**:

```bash
# Example commands (adapt to your project)
git tag -a v1.2.0 -m "Release version 1.2.0: Added feature X"
git push origin v1.2.0
```

**Release Notes**:

- Summarize changes from CHANGELOG
- Highlight breaking changes
- Include upgrade instructions if needed

### 4. Clean Up Branches

**Action**: Remove merged feature branches.

```bash
# Delete local branch
git branch -d feature/issue-{ID}-description

# Delete remote branch (if not auto-deleted by PR merge)
git push origin --delete feature/issue-{ID}-description
```

**Note**: Some projects auto-delete branches on PR merge. Verify your project settings.

### 5. Update Project Tracking

**Action**: Update external project management tools if used.

**Common Tools**:

- GitHub Projects - Move cards to "Done"
- Issue trackers - Close related issues
- Sprint boards - Update sprint progress
- Team dashboards - Reflect completion

**Verification**:

- [ ] Related issues closed or updated
- [ ] Project board reflects current state
- [ ] No orphaned or stale references

### 6. Notify Stakeholders (If Applicable)

**Action**: Communicate completion to relevant parties.

**Notification Scenarios**:

- Feature releases → Announce to users/team
- Breaking changes → Alert dependent teams
- Bug fixes → Notify affected users
- Security patches → Follow security disclosure process

**Communication Channels** (adapt to your project):

- GitHub issue comments
- Team chat channels
- Email notifications
- Release announcements
- Documentation updates

## Validation Checklist

Before considering work fully complete, verify:

- [ ] All tests passing in main branch
- [ ] No merge conflicts or issues
- [ ] Tracking files archived properly
- [ ] Documentation is current and accurate
- [ ] Release tagged (if applicable)
- [ ] Branches cleaned up
- [ ] Project tracking updated
- [ ] Stakeholders notified (if needed)

## Common Pitfalls to Avoid

1. **Forgetting to archive tracking files**

   - Leads to cluttered tracking directory
   - Makes it hard to see active work

2. **Incomplete documentation updates**

   - Causes confusion for future contributors
   - Creates technical debt

3. **Skipping release tags**

   - Makes version history unclear
   - Complicates rollback procedures

4. **Leaving stale branches**

   - Clutters repository
   - May cause confusion about active work

5. **Not closing related issues**
   - Leaves project tracking inaccurate
   - May cause duplicate work

## Project-Specific Customization

**[CUSTOMIZE]** Add project-specific steps:

- Deployment procedures
- Database migration verification
- Cache invalidation
- CDN purging
- Monitoring setup
- Alert configuration
- Dependency updates
- Security scans
- Performance benchmarks

## Emergency Rollback

If critical issues are discovered post-merge:

1. **Immediate**: Revert the merge commit
2. **Communication**: Alert team and stakeholders
3. **Investigation**: Identify root cause
4. **Resolution**: Create hotfix PR
5. **Documentation**: Record incident and resolution

```bash
# Revert merge commit
git revert -m 1 <merge-commit-hash>
git push origin main
```

## Completion

Once all checklist items are verified:

- Mark the original issue as closed
- Remove any temporary resources
- Archive any temporary documentation
- Update team status boards

The work is now fully complete and properly documented.
