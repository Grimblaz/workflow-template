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

| Skill          | Purpose                                       | Status    |
| -------------- | --------------------------------------------- | --------- |
| `tdd-workflow` | Test-Driven Development process and standards | ✅ Example |

## How to Use a Skill

1. **Load the router**: Read `skills/{skill-name}/SKILL.md`
2. **Answer the intake question**: The router asks what you need
3. **Load specific reference**: Based on response, load the targeted file
4. **Follow workflows**: Use workflow files for step-by-step procedures

### Example: Using tdd-workflow

```text
Agent: I need to write tests for a new feature
1. Read skills/tdd-workflow/SKILL.md
2. Identify phase: "Write tests" → workflows/write-tests-first.md
3. Read skills/tdd-workflow/workflows/write-tests-first.md
4. Follow the RED phase workflow
```

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

To add a domain-specific skill:

1. Create directory: `skills/{your-skill-name}/`
2. Create `SKILL.md` with:
   - Overview of the skill domain
   - Intake questions (what does the user need?)
   - Routing table (which file for which need)
   - File index (what's available)
3. Add workflows, references, and templates as needed
4. Update this README with the new skill

See `tdd-workflow/` for a complete example.

## Customization

> **Note**: The `tdd-workflow` skill uses Java/Spring Boot examples (JUnit, Maven/Gradle commands). Adapt the commands and patterns for your technology stack while keeping the conceptual structure.
