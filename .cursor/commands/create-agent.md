---
name: create-agent
description: "Generate a complete Cursor subagent from natural language description with validation and best practices. Creates .md files in .cursor/agents/ format compatible with Cursor's native subagent system."
args:
  - name: input
    description: "Agent description including: role, domain, expertise level, communication preferences, constraints, and required capabilities"
    isRequired: true
    isVariadic: true
  - name: location
    description: "Where to store the agent (project|personal). Project agents are in .cursor/agents/, personal in ~/.cursor/agents/"
    isRequired: false
    default: "project"
---

# Agent Creator

Transform freeform agent descriptions into complete, production-ready Cursor subagents.

## Process

1. Analyze the agent description from `{{input}}`
2. Extract core identity, operational characteristics, communication style, and constraints
3. Generate YAML frontmatter with `name` and `description` fields
4. Create system prompt body following the structure in `.cursor/skills/agent-creation-guide/SKILL.md`
5. Write agent file to `.cursor/agents/{slug}.md` (project) or `~/.cursor/agents/{slug}.md` (personal)

## Reference

For detailed guidance on agent creation, refer to the **agent-creation-guide** skill at `.cursor/skills/agent-creation-guide/SKILL.md`. It includes:
- Complete input processing guidelines
- System prompt structure templates
- Description field best practices
- Validation checklists
- Anti-patterns to avoid
- Optimization targets

## Output

Generate a single markdown file with:
- Valid YAML frontmatter (`name`, `description`)
- Complete system prompt as markdown body
- All information synthesized (no separate metadata sections)

Verify the file was created and provide usage instructions.