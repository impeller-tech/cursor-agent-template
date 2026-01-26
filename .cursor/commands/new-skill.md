---
name: new-skill
description: "Create a Cursor skill integrated with this project's ecosystem, automatically registered in AGENTS.md"
args:
  - name: skill_name
    description: "Name of the skill (lowercase, hyphens only, max 64 chars)"
    isRequired: true
  - name: purpose
    description: "What this skill teaches the AI to do - be specific about the task or workflow"
    isRequired: true
    isVariadic: true
  - name: location
    description: "Where to store the skill (project|personal). Project skills are in .cursor/skills/, personal in ~/.cursor/skills/"
    isRequired: false
    default: "project"
  - name: register_in_agents
    description: "Auto-register this skill in AGENTS.md (true|false)"
    isRequired: false
    default: "true"
---

# Skill Creator

Create Cursor skills integrated with this project's ecosystem.

## Process

1. Validate skill name (lowercase, hyphens only, max 64 chars, descriptive)
2. Validate purpose (specific task/workflow, clear triggers, concrete capabilities)
3. Create skill structure: `.cursor/skills/{{skill_name}}/SKILL.md` (or `~/.cursor/skills/` for personal)
4. Write SKILL.md with YAML frontmatter following Cursor's format
5. Register in AGENTS.md if `register_in_agents: true`

## Skill Structure

```
.cursor/skills/{{skill_name}}/
└── SKILL.md
```

SKILL.md format:
```markdown
---
name: {{skill_name}}
description: {{third person, includes WHAT and WHEN, trigger terms}}
---

# {{Skill Name}}

## Instructions
[Clear, step-by-step guidance]

## Examples
[Concrete examples]
```

## Best Practices

- Description: Third person, specific, includes trigger terms
- Keep SKILL.md under 500 lines
- Use progressive disclosure (link to reference.md for details)
- Reference AGENTS.md for project conventions if applicable
- File paths use forward slashes (`/` not `\`)

## Output

Create skill file and register in AGENTS.md if requested. Provide summary with location and verification checklist.
