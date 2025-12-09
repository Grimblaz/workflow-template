# Copilot Workflow Template

A multi-agent workflow system for GitHub Copilot, designed to orchestrate AI-assisted software development through specialized agents.

## Overview

This template provides a proven framework for working with AI coding agents, featuring:

| Agent | Role |
|-------|------|
| **Issue Designer** | Picks up issues, prepares environment, creates design docs |
| **Research Agent** | Performs deep research on proposed changes |
| **Code Conductor** | Orchestrates implementation via sub-agents |
| **Code-Smith** | Writes production code |
| **Test-Writer** | Creates comprehensive tests |
| **Refactor-Specialist** | Improves code quality and structure |
| *...and more* | Additional specialized agents for various tasks |

## Quick Start

### Option 1: Use as GitHub Template

1. Click **"Use this template"** → **"Create a new repository"**
2. Clone your new repository
3. Follow the [Customization Guide](CUSTOMIZATION.md)

### Option 2: Manual Setup

1. Clone this repository
2. Copy contents to your project
3. Customize the agents and instructions for your domain

## Repository Structure

```
.github/
├── agents/              # Agent definitions (15+ specialized agents)
├── instructions/        # Tracking format, PR review guidelines
├── templates/           # Implementation plan templates
├── prompts/             # Execution prompts for agents
├── scripts/             # Validation scripts
└── workflows/           # CI/CD workflow templates

skills/                  # Reusable skill definitions
├── README.md            # Skills framework documentation
└── tdd-workflow/        # Example: Test-Driven Development skill

Documents/
└── Development/         # Project documentation templates
    ├── NEXT-STEPS.md    # Roadmap template
    └── TechnicalArchitecture.md
```

## Key Concepts

### Agents

Agents are specialized AI personas defined in `.github/agents/`. Each agent has:
- A specific role and expertise
- Defined responsibilities
- Interaction patterns with other agents

### Skills

Skills are domain-specific knowledge packages in `skills/`. They provide:
- Contextual information for agents
- Best practices for specific workflows
- Examples and patterns to follow

### Instructions

Instructions in `.github/instructions/` guide agent behavior:
- Output formats (tracking, documentation)
- Review processes
- Quality standards

## Customization

See [CUSTOMIZATION.md](CUSTOMIZATION.md) for detailed guidance on adapting this template for your project.

Key customization points:
- **`copilot-instructions.md`** - Project-specific context
- **`architecture-rules.md`** - Your architecture patterns
- **`skills/`** - Domain-specific knowledge

Note: `copilot-instructions.md` and `architecture-rules.md` ship with the Phase 5 example deliverables and are not present earlier.

## Design Philosophy

### Standalone Template with Manual Sync

This template follows a **copy-and-adapt** model:
- No automatic updates to consumer repositories
- Versioned releases (tags) for upgrade reference points
- Each project maintains ownership of customizations
- Improvements flow back via PRs to this template

### Why This Approach?

1. **Independence** - Your project isn't blocked by template changes
2. **Flexibility** - Adapt freely to your specific needs
3. **Stability** - Upgrade on your schedule
4. **Control** - You decide what changes to incorporate

## Example Projects

This template includes example configurations for:
- **Spring Boot Microservice** - Layered architecture (Controller → Service → Repository)

> **Note**: All concrete examples throughout this template (test commands, quality gates, code patterns) use **Java/Spring Boot** conventions. When adapting for other stacks (Node.js, Python, etc.), replace these with your framework's equivalents while keeping the same conceptual structure.

The examples demonstrate how agents and skills work in practice, serving as a reference for adaptation to your specific technology stack.

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Ways to contribute:
- Report issues with agent definitions
- Share improvements to prompts
- Add new skill definitions
- Improve documentation

## Versioning

This project uses semantic versioning:
- **Major** - Breaking changes to agent interfaces
- **Minor** - New agents, skills, or features
- **Patch** - Bug fixes and documentation

Check [Releases](../../releases) for version history.

## License

This project is available for use under the terms specified in the LICENSE file.

## Related

- Originally extracted from [Organizations-of-Elos](https://github.com/Grimblaz-and-Friends/Organizations-of-Elos)
- Tracking issue: [#77](https://github.com/Grimblaz-and-Friends/Organizations-of-Elos/issues/77)