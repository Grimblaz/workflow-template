# Design: Agent Improvements (Post v1.2.0)

**Issue**: #13
**Created**: 2026-01-07
**Status**: Design Phase

## Overview

Port incremental agent improvements discovered during production usage since the v1.2.0 release (January 1, 2026).

## Changes to Port

### 1. Code-Conductor - Refactoring Guidelines Clarification ✅

**Source**: Commit `c06b99b9` (Jan 7)

**Decision**: Add explicit guidance distinguishing proportionate refactoring from broad rewrites.

**Key Concepts**:
- "Proportionate refactoring" = improving touched code and immediate neighbors without expanding PR scope
- "Broad rewrite" = changes that expand the PR's shape/intent, requiring separate approval or tech-debt issue
- Decision rule guardrail for when refactoring expands beyond PR intent

### 2. Code-Critic - Enhanced Adjudication ✅

**Source**: Commit `ac814f0c` (Jan 6)

**Decision**: Update adjudication process for clarity and improved functionality.

### 3. Code-Review-Response - Improved Workflow ✅

**Source**: Commit `ac814f0c` (Jan 6)

**Decision**: Clarify categorization and adjudication workflow.

### 4. Janitor - Knowledge Capture Process ✅

**Source**: Commit `2b0b8f0a` (Jan 7)

**Decision**: Specify where different types of knowledge should be captured.

**Key Concepts**:
- Durable knowledge (design decisions, architectural trade-offs) → `Documents/Decisions/` (git-tracked, permanent)
- Working notes (issue-specific context, debugging insights) → `.copilot-tracking/` (transient, archived after completion)

## Implementation Notes

- Changes are small and targeted
- Remove any project-specific references when porting
- Maintain technology-agnostic language

---

Ready for implementation.
