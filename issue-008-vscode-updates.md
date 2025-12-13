---
status: pending
priority: p2
issue_id: "008"
tags: [feature, vscode, documentation]
created: 2025-12-10
updated: 2025-12-10
---

# Issue #8: Implement VS Code 1.107 Updates

## Summary

Implement changes to leverage new features in VS Code 1.107, specifically Native Claude Skills and the Built-in GitHub MCP Server.

## Context

VS Code 1.107 (November 2025) introduced features that enhance agentic workflows.
See design document: `Documents/Design/issue-8-vscode-updates.md`.

## Progress

- [ ] Move `skills/` directory to `.claude/skills/`
- [ ] Update documentation to recommend Built-in GitHub MCP Server

## Next Steps

1. Execute `git mv skills .claude/skills`
2. Update `README.md` and `CONTRIBUTING.md` to reflect the new skills location.
3. Update `CONTRIBUTING.md` to add setup instructions for GitHub MCP Server.
4. Update `README.md` to mention VS Code 1.107+ requirement.

## Notes

- Ensure backward compatibility or clear documentation for users on older versions.
- Verify `.claude` directory visibility in documentation.
