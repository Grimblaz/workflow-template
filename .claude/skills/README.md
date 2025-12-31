# Skills Directory

Skills are **knowledge modules** that extend agent capabilities with domain-specific expertise.

## What Are Skills?

- **Agents** = WHO does the work (behavior/persona)
- **Skills** = WHAT they know (domain knowledge)

Skills are loaded on-demand, not always in context. This improves:

- **Context efficiency** - Don't bloat context with irrelevant knowledge
- **Modularity** - Separate concerns cleanly
- **Reusability** - Multiple agents can use the same skill

## Key Concept: Progressive Disclosure

Skills use a router pattern:

1. **SKILL.md is always loaded** when skill is invoked
2. **Router asks** "What do you want to do?"
3. **Routes to workflow** based on user intent
4. **Workflow specifies references** to load
5. **Only load what's needed** for the task

## Available Skills

| Skill | Purpose | Status |
|-------|---------|--------|
| `tdd-workflow` | TDD process knowledge and workflow guidance | ✅ Included |
| `brainstorming` | Structured Socratic questioning for exploring ideas | ✅ Included |
| `frontend-design` | Distinctive UI design guidance | ✅ Included |
| `ui-testing` | Resilient React component testing | ✅ Included |
| `skill-creator` | Guide for creating new skills | ✅ Included |
| `systematic-debugging` | 4-phase debugging process (Observe, Hypothesize, Test, Fix) | ✅ Included |
| `verification-before-completion` | Evidence-based verification checklist | ✅ Included |
| `software-architecture` | Clean Architecture and SOLID principles | ✅ Included |

## How to Use a Skill

1. **Load the router**: Read `.claude/skills/{skill-name}/SKILL.md`
2. **Answer the intake question**: The router asks what you need
3. **Load specific reference**: Based on response, load the targeted file
4. **Follow workflows**: Use workflow files for step-by-step procedures

### Example: Using tdd-workflow

```text
Agent: I need to write tests for a new feature
1. Read .claude/skills/tdd-workflow/SKILL.md
2. Identify phase: "Write tests" → workflows/write-tests-first.md
3. Read .claude/skills/tdd-workflow/workflows/write-tests-first.md
4. Follow the RED phase workflow
```

### VS Code 1.107+ Auto-Discovery

Skills with a `description` field in SKILL.md frontmatter are automatically discovered:

```yaml
---
name: my-skill
description: What the skill does AND when to use it. This triggers discovery.
---
```

**Supported frontmatter fields**: `name`, `description` only  
**Not supported in VS Code**: `allowed-tools` (use Claude Desktop for this)

## Skill Structure

```text
skill-name/
├── SKILL.md              # Router (always loaded when invoked)
├── workflows/            # Step-by-step procedures (FOLLOW)
├── references/           # Domain knowledge (READ)
├── templates/            # Output structures (COPY + FILL)
└── scripts/              # Executable code (EXECUTE) - future
```

## Creating New Skills

Use the `skill-creator` skill for step-by-step guidance:

```text
@skill-creator Help me create a new skill for [domain]
```

**Quick reference**:

1. Create directory: `.claude/skills/{your-skill-name}/`
2. Create `SKILL.md` with required frontmatter (`name` + `description`)
3. Add workflows, references, and templates as needed
4. Update this README with the new skill

See `skill-creator/SKILL.md` for detailed guidance and `tdd-workflow/` for a complete example.

## Customization

> **Note**: Skills like `tdd-workflow` and `ui-testing` use specific technology examples (Java/Spring Boot, React). Adapt the commands and patterns for your technology stack while keeping the conceptual structure.
