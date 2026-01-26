---
name: agent-creation-guide
description: "Comprehensive guide for creating Cursor subagents. Use when creating agents, designing agent architectures, or when detailed agent creation guidance is needed."
---

# Agent Creation Guide

Complete guide for transforming freeform agent descriptions into production-ready Cursor subagents.

## Quick Start

Transform agent descriptions into complete subagents following Cursor's native format. Reference this skill when creating agents.

## Input Processing

Analyze agent descriptions to extract:

### Core Identity
- **Role and Title**: Primary function
- **Domain Expertise**: Field or specialty
- **Seniority/Capability Level**: Junior, mid-level, senior, expert, or specialized
- **Scope**: Narrow specialist or broad generalist

### Operational Characteristics
- **Primary Goals**: Outcomes to achieve
- **Key Capabilities**: Specific skills or knowledge areas
- **Tool Requirements**: External tools, APIs, or resources needed
- **Collaboration Model**: Solo operator, pair programming, review assistant

### Communication & Style
- **Tone**: Formal, casual, technical, friendly, direct, empathetic
- **Verbosity**: Concise, balanced, or detailed explanations
- **Audience Awareness**: Primary user

### Constraints & Boundaries
- **Hard Limits**: What agent must never do
- **Soft Boundaries**: What to avoid or approach cautiously
- **Quality Standards**: Level of rigor expected

## Output Format

Generate a single markdown file with YAML frontmatter:

```markdown
---
name: <agent-slug>
description: <actionable description with trigger terms>
---

# <Agent Name> - <Role>

<Complete system prompt as markdown body>
```

### Step 1: Determine Agent Location

- **Project-level** (`.cursor/agents/`): Codebase-specific, shared with team, version controlled
- **User-level** (`~/.cursor/agents/`): Personal, available across all projects

### Step 2: Generate YAML Frontmatter

**Required Fields:**
- `name`: Lowercase slug (letters, numbers, hyphens only)
- `description`: How Cursor decides when to delegate. Must be:
  - Written in third person
  - Include WHAT (capabilities) and WHEN (trigger scenarios)
  - Include key trigger terms
  - Be specific and actionable
  - Optionally include "Use proactively" for automatic delegation

**Example descriptions:**
```yaml
# ❌ Too vague
description: Helps with code

# ✅ Specific and actionable
description: Expert code review specialist. Proactively reviews code for quality, security, and maintainability. Use immediately after writing or modifying code. Focuses on critical issues, warnings, and suggestions with specific examples.

# ✅ With trigger terms
description: Data analysis expert for SQL queries, BigQuery operations, and data insights. Use proactively for data analysis tasks, SQL queries, database operations, or when user mentions data analysis, BigQuery, or SQL.
```

### Step 3: Generate System Prompt Body

Structure the markdown body as:

```markdown
# <Agent Name> - <Role>

## Identity & Role

You are <agent_name>, a <role> specializing in <domain>. Your primary purpose is to <primary_goal>.

<2-3 paragraph detailed description>

## Core Capabilities

You excel at:
- <capability 1 with specifics>
- <capability 2 with specifics>

Your expertise includes:
- <technical skill 1>
- <technical skill 2>
- <knowledge domain 1>

## Communication Style

<Describe tone, style, verbosity, technical depth>

When responding:
- <guideline 1>
- <guideline 2>
- <guideline 3>

## Operating Principles

### You Always:
- <positive behavior 1 with context>
- <positive behavior 2 with context>

### You Never:
- <negative behavior 1 with reasons>
- <negative behavior 2 with reasons>

### When Uncertain:
<Describe how to handle ambiguity>

## Tools & Resources

You have access to:
- <tool 1>: <purpose>
- <tool 2>: <purpose>

## Decision-Making Framework

When faced with <situation type 1>:
- <decision rule or approach>

When faced with <situation type 2>:
- <decision rule or approach>

## Quality Standards

Your outputs should:
- <quality criterion 1>
- <quality criterion 2>

Before responding, verify:
- <validation check 1>
- <validation check 2>

## Constraints & Boundaries

Hard limits you must respect:
- <absolute constraint 1>
- <absolute constraint 2>

Areas requiring caution:
- <soft boundary 1>
- <soft boundary 2>

## Example Workflows

### Scenario: <use case 1>
<How agent handles this scenario>

### Scenario: <use case 2>
<How agent handles this scenario>

---

Remember: <key reminder that captures the agent's essence>
```

## Generation Guidelines

### Inferencing Rules
- If seniority isn't specified, infer from complexity of described tasks
- If tools are vague, suggest realistic options with TODO markers
- If communication style is unclear, match it to the domain (technical → precise, creative → expressive)
- If constraints are missing, add sensible defaults for the role
- If trigger scenarios aren't specified, infer from the agent's role and capabilities
- Always include "Use proactively" in description if the agent should be automatically invoked

### Quality Standards
- Goals must be specific and verifiable, not vague aspirations
- Capabilities should be concrete actions, not abstract qualities
- Tools must have realistic access methods, not handwaved "integrations"
- Examples should demonstrate actual use patterns, not trivial cases
- Constraints should be enforceable through prompt engineering

### Anti-Patterns to Avoid
- ❌ Overly broad roles ("expert in everything")
- ❌ Vague goals ("be helpful")
- ❌ Unenforceable constraints ("always be perfect")
- ❌ Contradictory requirements ("concise but comprehensive")
- ❌ Missing decision guidance (no heuristics for ambiguity)
- ❌ Vague descriptions without trigger terms ("Helps with code")
- ❌ First-person descriptions ("I can help you...")
- ❌ Missing "when to use" information in description

### Optimization Targets
- System prompt should be 1500-3000 tokens for most agents
- Specialist agents can be more concise (800-1500 tokens)
- Complex multi-capability agents may reach 3000-5000 tokens
- Prioritize clarity over brevity, but eliminate redundancy
- Description field should be 50-200 words with clear trigger terms
- Description should enable Cursor to automatically delegate when appropriate

## File Naming and Location

- **File name**: `{slug}.md` where slug is lowercase-hyphenated version of agent name
- **Project location**: `.cursor/agents/{slug}.md`
- **User location**: `~/.cursor/agents/{slug}.md`

## Validation Checklist

Before creating the file, ensure:
- ✅ YAML frontmatter is valid and properly formatted
- ✅ `name` field uses only lowercase letters, numbers, and hyphens
- ✅ `description` is specific, includes trigger terms, and written in third person
- ✅ System prompt is complete and immediately usable
- ✅ All placeholders are replaced with actual values
- ✅ Markdown is properly formatted
- ✅ File path matches the `location` parameter (project vs personal)
- ✅ Directory exists (create `.cursor/agents/` or `~/.cursor/agents/` if needed)

## Description Field Best Practices

### ✅ Good Descriptions

```yaml
# Code Reviewer
description: Expert code review specialist. Proactively reviews code for quality, security, and maintainability. Use immediately after writing or modifying code. Focuses on critical issues, warnings, and suggestions with specific examples.

# Debugger
description: Debugging specialist for errors, test failures, and unexpected behavior. Use proactively when encountering any issues, errors, exceptions, or test failures. Performs root cause analysis and provides specific fixes.

# Data Scientist
description: Data analysis expert for SQL queries, BigQuery operations, and data insights. Use proactively for data analysis tasks, SQL queries, database operations, or when user mentions data analysis, BigQuery, or SQL.

# Documentation Agent
description: Documentation specialist for maintaining code comments, README files, and technical documentation. Use proactively when code is written or modified, or when user requests documentation updates.
```

### ❌ Bad Descriptions

```yaml
# Too vague - no trigger terms
description: Helps with code

# First person - wrong voice
description: I can help you review code and find bugs

# Missing "when to use" information
description: Reviews code for quality

# No proactive delegation hint
description: Code reviewer that checks for issues
```

### Description Template

Use this structure:
```
[Role/Expertise] [Primary Capability]. [Secondary capabilities]. Use [when/trigger scenarios]. [Additional context about approach or focus].
```

Include:
- **WHAT**: Specific capabilities and expertise
- **WHEN**: Clear trigger scenarios and keywords
- **HOW**: Approach or focus (optional but helpful)
- **Proactive hint**: "Use proactively" if agent should auto-invoke
