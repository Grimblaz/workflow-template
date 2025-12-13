# Design: VS Code 1.107 Updates (Skills & MCP)

**Issue**: #8
**Status**: Proposed

## Context
VS Code 1.107 (November 2025) introduced several features that enhance agentic workflows:
1.  **Native Claude Skills**: VS Code can now automatically discover skills located in `.claude/skills/` or `~/.claude/skills/`.
2.  **Built-in GitHub MCP Server**: A native MCP server for GitHub is now available in Copilot Chat, removing the need for external tool configuration for basic GitHub operations.

## Decisions

### 1. Move Skills Directory
**Decision**: Move the existing `skills/` directory to `.claude/skills/`.
**Rationale**: 
- Enables "zero-setup" skill discovery for VS Code users.
- Agents can autonomously load skills like `tdd-workflow` when relevant.
- Aligns with the emerging standard for skill distribution.

**Implementation Details**:
- `git mv skills .claude/skills`
- Update references in `README.md` and `CONTRIBUTING.md` that point to the old `skills/` location.

### 2. Enable GitHub MCP Server
**Decision**: Update documentation to recommend the built-in GitHub MCP server.
**Rationale**:
- Simplifies the "Issue -> Design -> PR" workflow described in our templates.
- Reduces friction for new contributors (no need to install/configure a separate MCP server).

**Implementation Details**:
- Update `CONTRIBUTING.md`: Add a "Setup" section recommending `github.copilot.chat.githubMcpServer.enabled = true`.
- Update `README.md`: Mention the requirement for VS Code 1.107+ for best experience.

## Trade-offs
- **Backward Compatibility**: Users on older VS Code versions won't see the skills automatically. However, the files remain accessible, just in a hidden directory (`.claude`).
- **Visibility**: `.claude` is a hidden directory on Unix systems. We must ensure documentation clearly links to it.
