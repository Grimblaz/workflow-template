# Design Document: Issue #11 — VS Code 1.107+ Skills Discovery + Agent/Skill Integration

**Status**: Complete ✅
**Date**: 2025-12-31
**Version**: v1.2.0

## Problem Statement

The template advertised VS Code 1.107+ skill discovery, but the existing `tdd-workflow` skill did not follow the required frontmatter format (YAML must start on line 1). Additionally, the template lacked a set of universal skills that are commonly needed across different projects.

## Design Decisions

### 1. Skill Frontmatter Normalization
All skills in `.claude/skills/` must follow the VS Code 1.107+ and Claude Code compatible format:
- YAML frontmatter starts on line 1 with `---`.
- Includes `name` and `description` fields.
- `description` is optimized for semantic discovery.
- `allowed-tools` is omitted as it is not supported by VS Code.

### 2. Universal Skill Library
Added 7 new template-generic skills to provide a solid foundation for any project:
- `brainstorming`: Structured Socratic questioning.
- `frontend-design`: Purposeful UI design guidance.
- `ui-testing`: Resilient React component testing.
- `skill-creator`: Meta-guide for creating new skills.
- `systematic-debugging`: 4-phase evidence-based debugging.
- `verification-before-completion`: Pre-completion validation checklist.
- `software-architecture`: Clean Architecture and SOLID principles.

### 3. Agent-Skill Integration
Updated orchestration agents to be "skill-aware":
- Removed legacy `runSubagent` terminology in favor of "agent tool".
- Added explicit instructions for agents to check `.claude/skills/` for relevant guidance.
- Improved delegation logic to leverage specialist skills.

### 4. Repository Hygiene
- Ensured `.copilot-tracking/` directory is preserved in git clones via `.gitkeep`.
- Updated `.gitignore` to allow `.gitkeep` while ignoring transient tracking files.

## Implementation Details

- **Skills Directory**: `.claude/skills/`
- **Agents Updated**: `Plan-General`, `Plan-Architect`, `Code-Conductor`, `Test-Writer`.
- **Version**: Bumped to `v1.2.0` to reflect the significant expansion of the skills framework.

## Alternatives Considered

- **Renaming `tdd-workflow`**: Considered renaming to `test-driven-development`, but decided to keep the existing name to maintain compatibility with existing documentation.
- **Including `allowed-tools`**: Decided against it to avoid confusion in VS Code, which explicitly does not support this field.
