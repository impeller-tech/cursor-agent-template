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

# Skill Creator with Template Integration

Create Cursor skills that integrate with this project's ecosystem, following Cursor's best practices and automatically registering in AGENTS.md.

## Skill Creation Process

### Step 1: Validate Inputs

Validate skill name:
- Lowercase letters, numbers, and hyphens only
- Max 64 characters
- Descriptive and specific (not generic like "helper" or "utils")
- No spaces, underscores, or special characters

Validate purpose:
- Specific task or workflow (not vague like "be helpful")
- Clear trigger scenarios
- Concrete capabilities

### Step 2: Determine Skill Location

Project skills (`.cursor/skills/`): Shared with team, version controlled, project-specific workflows.

Personal skills (`~/.cursor/skills/`): Individual use, cross-project reusable. May still be documented in AGENTS.md if `register_in_agents: true`.

### Step 3: Create Skill Structure

```
.cursor/skills/{{skill_name}}/
├── SKILL.md
├── reference.md
├── examples.md
└── scripts/
```

### Step 4: Write SKILL.md

Follow Cursor's SKILL.md format with YAML frontmatter:

```markdown
---
name: {{skill_name}}
description: {{concise description with trigger terms}}
---

# {{Skill Name}}

## Instructions
[Clear, step-by-step guidance]

## Examples
[Concrete examples]
```

Description requirements:
- Write in third person (injected into system prompt)
- Include WHAT (specific capabilities) and WHEN (trigger scenarios)
- Include key search terms

Good: "Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction."

Bad: "Helps with documents"

### Step 5: Apply Best Practices

Keep SKILL.md under 500 lines. Use progressive disclosure (link to reference.md for details). Keep examples concrete.

Set appropriate freedom level:
- High freedom (text instructions): Multiple valid approaches
- Medium freedom (templates): Preferred pattern with variation
- Low freedom (specific scripts): Fragile operations requiring consistency

### Step 6: Template Integration

If project skill or `register_in_agents: true`, reference AGENTS.md for conventions, link to existing agents, and use project-specific patterns.

### Step 7: Register in AGENTS.md

If `register_in_agents: true`, add to AGENTS.md's "Agent Ecosystem" section:

```markdown
#### Skill: {{skill_name}}

**Purpose**: {{one-line description}}  
**Location**: `{{path/to/skill}}`  
**Type**: {{task-specific instruction|workflow|pattern}}

**What It Does**
{{List specific capabilities}}

**When to Use**
{{Describe trigger scenarios}}
- Use case 1: {{description}}
- Use case 2: {{description}}

**Integration Points**
{{How this skill relates to the project}}
- References: {{AGENTS.md sections, other agents, etc.}}
- Used by: {{which agents or workflows}}

**Example Usage**
\`\`\`
{{Show example command or prompt}}
\`\`\`
```

Update table of contents and "Last Updated" timestamp if present.

### Step 8: Set Up Auto-Maintenance

If AGENTS.md has auto-maintenance rules, add `.cursor/skills/**/*` to watch patterns.

## Skill Content Guidelines

Description best practices:
- Write in third person: "Processes Excel files and generates reports"
- Be specific: "Extract text and tables from PDF files, fill forms, merge documents"
- Include triggers: "Use when working with PDF files or when the user mentions PDFs"
- Include both WHAT and WHEN

Avoid:
- First person: "I can help you process Excel files"
- Vague: "Helps with documents"
- Missing triggers: "Processes files" (when?)

Essential sections: Quick Start (required), Examples (recommended), Additional Resources (if using progressive disclosure).

Optional: Workflow patterns, common pitfalls, integration with other tools, troubleshooting.

Anti-patterns to avoid:
- Windows-style paths (use `/` not `\`)
- Too many options (provide default with escape hatch)
- Time-sensitive info
- Inconsistent terminology
- Vague skill names (use `processing-pdfs` not `helper`)

## Template-Specific Enhancements

### Reference AGENTS.md

If the skill relates to project conventions:

```markdown
## Project Conventions

This skill follows conventions documented in AGENTS.md:
- Code style: See AGENTS.md > Development Conventions
- Architecture: See AGENTS.md > Architectural Patterns
- Testing: See AGENTS.md > Testing Strategy
```

### Link to Related Agents

If the skill works with existing agents:

```markdown
## Related Agents

This skill complements:
- **{{agent_name}}**: {{how they work together}}
- See AGENTS.md > Agent Ecosystem for full agent list
```

### Use Project Patterns

Reference project-specific patterns from AGENTS.md:

```markdown
## Following Project Patterns

When implementing, follow patterns from AGENTS.md:
- {{Pattern 1}}: {{how to apply}}
- {{Pattern 2}}: {{how to apply}}
```

## Output Requirements

After creating the skill, provide summary with location and AGENTS.md registration status. Include verification checklist: SKILL.md under 500 lines, description includes trigger terms and is in third person, examples are concrete, file paths use forward slashes, AGENTS.md updated if requested, no time-sensitive information, consistent terminology.

## Error Handling

If validation fails:
- Invalid skill name: Suggest corrections (e.g., "code_review" → "code-review")
- Vague purpose: Ask for more specific details
- AGENTS.md not found: Create it or ask user to run `/init` first
- Permission issues: Suggest checking file permissions or using personal location

## Special Cases

Skill for maintaining AGENTS.md: Reference template's AGENTS.md structure, include sections from `/init` output, link to auto-maintenance rules.

Skill for creating agents: Reference `/create-agent` patterns, use template's agent YAML structure, link to existing agents in AGENTS.md.

Cross-project skills: Avoid project-specific references, use generic patterns, document when to customize.
