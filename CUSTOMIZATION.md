# Customization Guide

This guide walks you through adapting the workflow template for your specific project.

## Before You Start

Ensure you have:

- A clear understanding of your project's architecture
- Identified your team's development workflow
- Decided on coding standards and conventions

## Step-by-Step Customization

### 1. Project Context (`copilot-instructions.md`)

Create `.github/copilot-instructions.md` with your project-specific context:

```markdown
# Project: [Your Project Name]

## Overview
Brief description of what your project does.

## Technology Stack
- Language: [e.g., Java 21]
- Framework: [e.g., Spring Boot 3.x]
- Database: [e.g., PostgreSQL]
- Build Tool: [e.g., Gradle]

## Architecture
Describe your project's architecture pattern.

## Key Conventions
List your team's coding conventions.
```

### 2. Architecture Rules (`architecture-rules.md`)

Create `.github/architecture-rules.md` defining your structure:

```markdown
# Architecture Rules

## Layer Structure
Define your layers (e.g., Controller → Service → Repository)

## Package Organization
Describe how code should be organized.

## Dependency Rules
- What can depend on what
- What should remain independent
```

### 3. Customize Agents

Review each agent in `.github/agents/` and consider:

- **Do the responsibilities fit your workflow?**
- **Are the interaction patterns appropriate?**
- **Do you need additional specialized agents?**

Common customizations:

- Adjust code standards references
- Update architecture terminology
- Add domain-specific knowledge

### 4. Add Project Skills

Create skills in `.claude/skills/` for domain-specific knowledge:

```text
.claude/skills/
├── your-domain/
│   ├── README.md          # Skill description
│   ├── patterns.md        # Common patterns
│   └── examples/          # Code examples
```

### 5. Configure Templates

Update templates in `.github/templates/`:

- Implementation plan template
- PR description template
- Issue templates

### 6. Set Up CI/CD

Adapt workflows in `.github/workflows/`:

- Build and test pipeline
- Code quality checks
- Deployment automation

## Example: Spring Boot Microservice

Here's a complete example for a Spring Boot microservice:

### copilot-instructions.md

```markdown
# Project: Order Service

## Overview
Microservice handling order processing for e-commerce platform.

## Technology Stack
- Java 21
- Spring Boot 3.2
- PostgreSQL 15
- Gradle 8.x

## Architecture
Layered architecture:
- Controller (REST API)
- Service (Business Logic)
- Repository (Data Access)

## Conventions
- Use constructor injection
- DTOs for API boundaries
- Entities for persistence
```

### architecture-rules.md

```markdown
# Architecture Rules

## Layers
1. Controller - HTTP handling only
2. Service - All business logic
3. Repository - Database operations

## Dependencies
- Controllers → Services
- Services → Repositories
- Services → External Clients

## Prohibited
- Controllers accessing Repositories directly
- Circular dependencies between services
```

## Maintaining Your Customizations

### Version Tracking

Keep track of which template version you started from:

```markdown
<!-- In your README or a TEMPLATE-VERSION file -->
Based on workflow-template v1.0.0
```

### Upgrading

When a new template version is released:

1. Review the [release notes](../../releases)
2. Identify relevant changes
3. Manually merge desired updates
4. Test your workflow

### Contributing Back

If you develop improvements:

1. Generalize the solution
2. Submit a PR to this template
3. Help the community benefit

## Troubleshooting

### Agents Not Following Instructions

- Ensure `copilot-instructions.md` is in `.github/`
- Check that agent definitions are properly formatted
- Verify instructions aren't conflicting

### Skills Not Being Used

- Confirm skill is in the `.claude/skills/` directory
- Check skill README is properly structured
- Ensure skill is referenced in relevant prompts

### CI/CD Failures

- Verify workflow syntax
- Check required secrets are configured
- Review workflow permissions

## Getting Help

- Check [Issues](../../issues) for known problems
- Review [Discussions](../../discussions) for tips
- Open a new issue if stuck
