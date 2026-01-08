# Design: Agent System Enhancements

**Issue**: #13
**Created**: 2026-01-07
**Status**: Design Phase

## Overview

This document captures design decisions for enhancing the workflow template's agent system based on patterns observed in production usage.

## Key Design Decisions

### 1. Agent Transparency Rules ✅

**Decision**: Add explicit transparency requirements to Code-Conductor

**Rationale**: When orchestrating work, users need visibility into what's happening. Announcing subagent calls before making them improves trust and debuggability.

**Key Concepts**:
- Always announce which agent is being called and why
- Never perform expert tasks directly
- State the expert's role before delegation

### 2. Skill Awareness Integration ✅

**Decision**: Add skill awareness and mapping to Code-Conductor

**Rationale**: Skills provide domain knowledge that specialists need. The orchestrator should identify relevant skills and instruct subagents to use them.

**Approach**:
- Check `.claude/skills/` at start of every task
- Maintain skill-to-context mapping table
- Include skill instructions in delegation prompts

### 3. Mandatory Refactoring Phase ✅

**Decision**: Refactoring is MANDATORY, not optional

**Rationale**: Code quality improves when refactoring is an explicit step, not an afterthought. Refactor-Specialist decides what needs improvement, not the plan.

**Key Concepts**:
- "Proportionate refactoring" = improving touched code and immediate neighbors
- "Broad rewrite" = expanding PR scope, requiring separate approval
- Flow: Code-Smith → Refactor-Specialist → Code-Critic

### 4. Proactive Hunting Stance for Refactor-Specialist ✅

**Decision**: Refactor-Specialist should actively hunt for improvements

**Rationale**: Passive "looks fine" reviews miss opportunities. Presume every file is improvable until verified otherwise.

**Checklist Categories**:
- Size & Structure (file limits, function length)
- DRY (duplicate code detection)
- SOLID (design principle violations)
- Readability (naming, magic numbers, complexity)
- Testability (private methods, tight coupling)

### 5. Knowledge Capture Workflow ✅

**Decision**: Add optional knowledge capture to Janitor for non-trivial problems

**Rationale**: Complex debugging insights are often lost. Capturing them in solution documents improves future productivity.

**Key Concepts**:
- Trigger: complex debugging, novel solutions, architectural decisions
- Categories: Architecture, Testing, Performance, Integration, Workflow
- Optional but encouraged after non-trivial work

### 6. Plan Execution Prompt ✅

**Decision**: Create reusable prompt for enforcing plan-tracking discipline

**Rationale**: Plan drift is common. A pre-flight checklist ensures agents read plans, verify roles, and stay in boundaries.

**Key Steps**:
1. Load plan (mandatory)
2. Verify role (chatmode boundary)
3. Find next task (execution)
4. Mark complete (immediate)
5. Check boundary (phase complete?)

### 7. webapp-testing Skill ✅

**Decision**: Add Playwright-based E2E testing skill

**Rationale**: E2E testing is a common need. A skill provides patterns, setup guidance, and best practices without bloating agent instructions.

**Structure**:
- `SKILL.md` - Router
- `patterns.md` - Common patterns (locators, assertions, waits)
- `playwright-setup.md` - Configuration and setup

### 8. Skills README ✅

**Decision**: Create comprehensive README explaining skills system

**Rationale**: The skills concept (knowledge modules vs agent behavior) needs clear documentation for users to leverage effectively.

**Key Sections**:
- What are skills
- Progressive disclosure concept
- Available skills table
- How to use a skill
- Skill structure conventions

## Trade-offs Considered

### Archive vs Delete for Tracking Files

**Options**:
1. Archive to `.copilot-tracking-archive/` (preserves history)
2. Delete entirely (cleaner workspace)

**Decision**: Support both approaches, default to delete for template simplicity. Projects with compliance needs can customize to archive.

### Model Recommendations

**Options**:
1. Prescriptive (specify exact models)
2. Descriptive (describe task complexity, let user decide)

**Decision**: Descriptive approach with suggestions. Model availability varies by environment, and users may have cost constraints.

### Agent Frontmatter Consistency

**Decision**: Standardize on:
- `name`: Required
- `description`: Required (brief)
- `argument-hint`: Required (what to pass)
- `tools`: Required (array)
- `handoffs`: Optional (array of label/agent/prompt)

## Implementation Notes

### Removing Source References

When adapting content, ensure removal of:
- Project-specific references (game mechanics, domain terms)
- Organization/repository names
- Specific file paths that don't apply to template
- Custom CI workflow references

### Maintaining Technology Agnosticism

The template should work for:
- Any programming language
- Any framework
- Any test runner
- Any CI platform

Skill examples can be more specific (e.g., Playwright) but should note they're examples.

## Next Steps

1. Create research document with detailed analysis
2. Create implementation plan with phases
3. Execute plan via Code-Conductor

---

Ready for handoff to Plan-Architect.
