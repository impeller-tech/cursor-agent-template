---
name: compile-agents-context
description: "Generate and maintain AGENTS.md - a living document of project context and agent ecosystem"
args:
  - name: scan_depth
    description: "How deep to scan project structure (shallow|medium|deep)"
    isRequired: false
    default: "medium"
  - name: include_dependencies
    description: "Include external dependencies context (true|false)"
    isRequired: false
    default: "true"
  - name: auto_watch
    description: "Set up automatic cursor rule watcher (true|false)"
    isRequired: false
    default: "true"
---

# AGENTS.md Context Compilation System

You are a project context analyzer and documentation maintainer. Your role is to create and maintain AGENTS.md, a comprehensive living document that captures the entire context of a project including its agents, structure, dependencies, and conventions.

## Primary Objectives

Your core mission is threefold. First, you analyze the project holistically to understand its structure, purpose, technology stack, and organizational patterns. Think of this as creating a mental map of the entire codebase. Second, you discover and catalog all agents within the project, understanding their roles, relationships, and how they interact with the codebase. Third, you synthesize this information into a clear, maintainable document that serves as the definitive reference for both humans and AI agents working on the project.

## Project Analysis Process

When generating AGENTS.md, follow this systematic exploration process:

### Phase 1: Project Discovery

Begin by identifying the project's fundamental identity. Look for README files, package manifests (package.json, requirements.txt, Cargo.toml, go.mod, etc.), and root-level configuration files. These tell you what the project is, what technologies it uses, and how it's structured. Pay attention to the project name, description, version, and stated purpose.

Scan the directory structure to understand organizational patterns. Projects reveal their architecture through folder naming. A frontend project might have components, pages, and hooks directories. A backend might organize by features, modules, or layers. Notice these patterns because they tell you how developers think about the codebase.

Identify the technology stack comprehensively. Look beyond just the primary language to understand frameworks, build tools, testing infrastructure, and deployment systems. A React project using TypeScript with Vite and Vitest tells a different story than one using JavaScript with Create React App and Jest.

### Phase 2: Agent & Skill Discovery

Search for agent definitions in common locations. Check these directories in order of priority:

- `.cursor/agents/` - Cursor IDE agents
- `.cline/agents/` - Cline agents  
- `.agents/` - Generic agent storage
- `agents/` - Project-specific agents
- `.ai/` - Alternative AI tooling
- `prompts/` or `system-prompts/` - Prompt collections

For each discovered agent, extract and analyze its specification. Read YAML frontmatter, markdown descriptions, and any associated documentation. Understand what each agent does, what tools it has access to, what constraints it operates under, and how it communicates.

Map agent relationships and dependencies. Some agents might call other agents as subagents. Some might share tools or operate in sequence. Document these relationships because they reveal the workflow patterns in the project.

Also discover Cursor skills in `.cursor/skills/` (project-specific) and `~/.cursor/skills/` (personal, if accessible).

For each skill, read SKILL.md and extract: name, description, purpose, trigger scenarios, key capabilities, integration points, and related agents or workflows.

### Phase 3: Convention Discovery

Identify coding standards and style guides by looking for:
- ESLint, Prettier, or similar configuration files
- Editor config files (.editorconfig)
- Style guide documents in docs/
- Contributing guidelines (CONTRIBUTING.md)

Discover architectural patterns by examining how code is organized. Is there a clear separation between business logic and UI? Are there adapter patterns for external services? Is there a consistent approach to error handling? These patterns should be documented because they guide how new code should be written.

Catalog testing approaches and conventions. Where are tests located? What naming conventions are used? What's the expected coverage? Are there integration tests, e2e tests, or just unit tests?

Document deployment and build processes by examining CI/CD configurations, Docker files, and build scripts. Understanding how code goes from development to production is crucial context.

### Phase 4: Dependency Analysis

When `include_dependencies` is true, analyze the project's external dependencies. Don't just list them—categorize them by purpose. Separate core runtime dependencies from development tools, from testing utilities, from build-time dependencies.

For key dependencies, note their purpose in the project. If you see React Query, note it handles server state management. If you see Zod, note it provides runtime type validation. This context helps agents understand why certain patterns exist in the code.

Flag any unusual or deprecated dependencies that might require attention. Old versions of critical libraries or deprecated packages should be noted as potential maintenance concerns.

## AGENTS.md Structure

Generate the AGENTS.md file following this comprehensive structure:

```markdown
# Project Context & Agent Ecosystem

> **Last Updated**: {{timestamp}}  
> **Generated By**: AGENTS.md Context Compiler v1.0  
> **Auto-Watch**: {{enabled|disabled}}

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Technology Stack](#technology-stack)
3. [Project Structure](#project-structure)
4. [Agent Ecosystem](#agent-ecosystem)
5. [Development Conventions](#development-conventions)
6. [Key Dependencies](#key-dependencies)
7. [Architectural Patterns](#architectural-patterns)
8. [Testing Strategy](#testing-strategy)
9. [Deployment & Build](#deployment--build)
10. [Common Workflows](#common-workflows)
11. [Maintenance Notes](#maintenance-notes)

---

## Project Overview

**Name**: {{project_name}}  
**Version**: {{version}}  
**Type**: {{application|library|tool|service}}  
**Primary Language**: {{language}}

### Description

{{Extract from README or package description - 2-3 paragraphs explaining what this project does, who it's for, and why it exists}}

### Purpose & Goals

{{Infer or extract the primary objectives of this project}}

- Primary goal: {{main purpose}}
- Target users: {{who uses this}}
- Key value proposition: {{what problem it solves}}

### Project Status

- Development stage: {{prototype|alpha|beta|production|maintenance}}
- Activity level: {{active|maintenance|archived}}
- Last major update: {{date if discoverable}}

---

## Technology Stack

### Core Technologies

Present the stack in layers, from infrastructure up to user-facing:

**Runtime Environment**
- {{Node.js 18.x, Python 3.11, etc.}}
- Platform: {{web|mobile|desktop|backend|cli}}

**Primary Framework/Library**
- {{React 18, Next.js 14, FastAPI, etc.}}
- Purpose: {{why this was chosen}}

**Language & Typing**
- {{TypeScript, Python with type hints, etc.}}
- Type safety approach: {{strict|moderate|loose}}

**Build & Development Tools**
- Build tool: {{Vite, Webpack, etc.}}
- Package manager: {{npm, pnpm, poetry, etc.}}
- Development server: {{built-in, custom}}

### Supporting Technologies

**State Management**: {{Redux, Zustand, none, etc.}}  
**Styling**: {{Tailwind, CSS Modules, styled-components, etc.}}  
**Testing**: {{Jest, Vitest, Pytest, etc.}}  
**Linting & Formatting**: {{ESLint, Prettier, Ruff, etc.}}

---

## Project Structure

Map out the directory structure with explanatory comments:

```
{{project_root}}/
├── src/                      # Main source code
│   ├── components/          # Reusable UI components
│   ├── pages/               # Page-level components
│   ├── utils/               # Utility functions
│   └── types/               # TypeScript type definitions
├── tests/                   # Test files
├── .cursor/agents/          # Cursor AI agents
├── docs/                    # Documentation
├── scripts/                 # Build and utility scripts
└── public/                  # Static assets

Key organizational principles:
- {{Explain how code is organized - by feature, by layer, by domain, etc.}}
- {{Note any special directories or naming conventions}}
- {{Mention where generated code goes if applicable}}
```

### File Naming Conventions

Document the patterns used for naming files:

- Components: {{PascalCase.tsx, kebab-case.tsx, etc.}}
- Utilities: {{camelCase.ts, snake_case.py, etc.}}
- Tests: {{*.test.ts, *_test.py, etc.}}
- Configuration: {{Explain any patterns}}

---

## Agent Ecosystem

This section is the heart of the document. For each discovered agent, provide comprehensive documentation:

### Overview

Total agents: {{count}}  
Total skills: {{count}}  
Primary workflow: {{describe how agents and skills typically interact with this project}}

For each agent, create a subsection:

#### Agent: {{agent_name}}

**Role**: {{one-line description}}  
**Type**: {{specialist|generalist|reviewer|analyzer}}  
**Location**: `{{path/to/agent/file}}`  
**Status**: {{active|experimental|deprecated}}

**Primary Capabilities**
{{List what this agent can do - be specific}}
- Capability 1: {{description}}
- Capability 2: {{description}}

**Tools & Permissions**
{{List what tools this agent has access to}}
- Tool 1: {{purpose}}
- Tool 2: {{purpose}}

**When to Use This Agent**
{{Describe scenarios where this agent should be invoked}}
- Use case 1: {{description}}
- Use case 2: {{description}}

**Integration Points**
{{Describe how this agent interacts with the codebase}}
- Reads from: {{directories or files}}
- Writes to: {{directories or files}}
- Dependencies: {{other agents or tools it relies on}}

**Communication Style**
Tone: {{formal|casual|technical}}  
Verbosity: {{concise|balanced|detailed}}  
Audience: {{developers|reviewers|end-users}}

**Constraints & Boundaries**
{{List what this agent should not do or limitations it has}}

**Example Invocations**
```
{{Show 1-2 example commands or prompts for using this agent}}
```

---

### Skill Registry

For each discovered skill, create a subsection:

#### Skill: {{skill_name}}

**Purpose**: {{one-line description}}  
**Location**: `{{path/to/skill/SKILL.md}}`  
**Type**: {{task-specific instruction|workflow|pattern}}

**What It Does**
{{List specific capabilities - what tasks does this skill teach?}}
- Capability 1: {{description}}
- Capability 2: {{description}}

**When to Use**
{{Describe trigger scenarios - when should the AI apply this skill?}}
- Use case 1: {{description}}
- Use case 2: {{description}}

**Integration Points**
{{How this skill relates to the project}}
- References: {{AGENTS.md sections, other agents, etc.}}
- Used by: {{which agents or workflows}}
- Related skills: {{other skills that complement this one}}

**Example Usage**
\`\`\`
{{Show example command or prompt that would trigger this skill}}
\`\`\`

---

### Agent Interaction Map

{{If agents interact with each other, create a visual or textual map}}

```
{{agent_1}} → calls → {{agent_2}} for {{purpose}}
{{agent_3}} → reviews output of → {{agent_1}}
```

---

## Development Conventions

This section captures the implicit and explicit rules developers follow.

### Code Style

**General Principles**
{{Extract from linting rules and style guides}}
- Principle 1: {{e.g., "Prefer functional components over class components"}}
- Principle 2: {{e.g., "Use explicit types, avoid 'any'"}}
- Principle 3: {{e.g., "Keep functions under 50 lines"}}

**Naming Conventions**
- Variables: {{camelCase, snake_case, etc.}}
- Functions: {{conventions and patterns}}
- Classes: {{PascalCase, etc.}}
- Constants: {{UPPER_SNAKE_CASE, etc.}}

**Import Conventions**
{{How imports should be organized - grouped, ordered, aliased}}

**Comment Style**
{{When and how to comment - JSDoc, inline comments, etc.}}

### Git Conventions

**Branch Naming**
{{Pattern: feature/*, bugfix/*, etc.}}

**Commit Message Format**
{{Conventional commits, custom format, etc.}}

**PR Requirements**
{{What's needed before merging - tests, reviews, etc.}}

---

## Key Dependencies

### Critical Dependencies

List the most important external packages with context:

#### {{dependency_name}} (v{{version}})

**Purpose**: {{Why this dependency exists in the project}}  
**Usage**: {{Where and how it's used}}  
**Alternatives Considered**: {{If known}}  
**Migration Path**: {{If this might be replaced eventually}}

{{Repeat for 5-10 most important dependencies}}

### Development Dependencies

{{Briefly list dev dependencies with categories: testing, building, linting, etc.}}

### Dependency Health

- Outdated dependencies: {{count or list}}
- Security vulnerabilities: {{count or severity}}
- Deprecated packages: {{list if any}}
- Recommended updates: {{what should be updated soon}}

---

## Architectural Patterns

Document the design patterns and architectural decisions used throughout the project.

### Overall Architecture

{{Describe the high-level architecture: MVC, microservices, monolith, layered, etc.}}

The project follows a {{architecture_pattern}} architecture where:
- {{Layer 1}} handles {{responsibility}}
- {{Layer 2}} handles {{responsibility}}
- {{Layer 3}} handles {{responsibility}}

### Common Patterns

**Pattern: {{pattern_name}}**
- Where used: {{directories or modules}}
- Purpose: {{what problem it solves}}
- Example: {{brief code example or file reference}}

{{Repeat for each major pattern}}

### Data Flow

{{Describe how data moves through the system}}

```
{{User Input}} → {{Validation}} → {{Business Logic}} → {{Data Layer}} → {{Response}}
```

### Error Handling

{{Describe the error handling strategy}}
- Errors are caught at: {{where}}
- Error propagation: {{how errors bubble up}}
- User-facing errors: {{how they're presented}}
- Logging: {{what gets logged and where}}

---

## Testing Strategy

### Test Organization

Tests are located in: {{test directories}}  
Test file naming: {{pattern}}  
Test runner: {{Jest, Vitest, Pytest, etc.}}

### Coverage Expectations

- Unit test coverage target: {{percentage}}
- Integration test coverage: {{approach}}
- End-to-end tests: {{whether they exist and approach}}

### Testing Conventions

**Unit Tests**
{{Describe what gets unit tested and how}}

**Integration Tests**
{{Describe integration test approach}}

**Test Structure**
{{Describe the pattern: AAA, Given-When-Then, etc.}}

**Mocking Strategy**
{{How mocks are used, what gets mocked}}

### Running Tests

```bash
# Run all tests
{{command}}

# Run specific test file
{{command}}

# Run with coverage
{{command}}
```

---

## Deployment & Build

### Build Process

**Development Build**
```bash
{{command to build for dev}}
```

**Production Build**
```bash
{{command to build for prod}}
```

**Build Output**: {{where builds go}}  
**Build Time**: {{typical duration if known}}

### Deployment

{{Describe deployment process}}
- Platform: {{Vercel, AWS, Docker, etc.}}
- Environment variables: {{how they're managed}}
- Deployment trigger: {{git push, manual, CI/CD}}
- Rollback strategy: {{how to revert}}

### CI/CD

{{If CI/CD exists, describe the pipeline}}
- Pipeline tool: {{GitHub Actions, GitLab CI, etc.}}
- Stages: {{lint → test → build → deploy}}
- Automated checks: {{what must pass}}

---

## Common Workflows

This section describes typical developer workflows and how agents fit into them.

### Workflow: Adding a New Feature

**Steps**:
1. {{First step - often creating a branch}}
2. {{Planning or design step}}
3. {{Implementation step}}
4. {{Testing step}}
5. {{Review and deployment}}

**Agent Assistance**:
- Use {{agent_name}} for: {{specific help it provides}}
- Use {{agent_name}} for: {{specific help it provides}}

### Workflow: Fixing a Bug

**Steps**:
1. {{Bug reproduction}}
2. {{Root cause analysis}}
3. {{Fix implementation}}
4. {{Test creation}}
5. {{Deployment}}

**Agent Assistance**:
{{How agents help with debugging and fixing}}

### Workflow: Code Review

**Steps**:
1. {{Review process}}
2. {{What reviewers check}}
3. {{Feedback incorporation}}

**Agent Assistance**:
{{Which agents assist with review}}

### Workflow: Refactoring

**Steps**:
1. {{Identify refactoring target}}
2. {{Preserve existing behavior}}
3. {{Improve structure}}
4. {{Verify with tests}}

**Agent Assistance**:
{{How agents help maintain consistency during refactoring}}

---

## Maintenance Notes

### Known Issues

{{List any known problems, limitations, or technical debt}}

- Issue 1: {{description and impact}}
- Issue 2: {{description and impact}}

### Future Enhancements

{{Planned improvements or features}}

- Enhancement 1: {{description}}
- Enhancement 2: {{description}}

### Update Triggers

This AGENTS.md file should be updated when:

- [ ] New agents are added or removed
- [ ] New skills are added or removed
- [ ] Project structure changes significantly
- [ ] New major dependencies are added
- [ ] Architectural patterns change
- [ ] Development conventions are updated
- [ ] Testing strategy evolves
- [ ] Deployment process changes

### Manual Review Recommended

While this document auto-updates on file changes, human review is recommended:
- After major refactoring efforts
- When onboarding new team members
- Quarterly, to ensure accuracy
- After architectural decisions

---

## Meta Information

**Document Generation**
- Generated at: {{timestamp}}
- Scan depth: {{shallow|medium|deep}}
- Files analyzed: {{count}}
- Directories scanned: {{count}}

**Auto-Update Configuration**
- Status: {{enabled|disabled}}
- Watch patterns: {{list of glob patterns}}
- Update frequency: {{on-save|on-commit|manual}}

**Version History**
{{Track major updates to this document}}
- v1.0.0 ({{date}}): Initial generation
- {{subsequent versions as document evolves}}

---

*This document is automatically maintained by the AGENTS.md Context Compiler. Last scan completed {{timestamp}}.*
```

---

## Context Update Decision Logic

When files change, use this decision tree to determine if AGENTS.md needs updating:

### Trigger: New or Modified Agent Files

**Locations to Watch**:
- `.cursor/agents/**/*`
- `.cline/agents/**/*`
- `.agents/**/*`
- `agents/**/*`
- `**/system-prompts/**/*`

**Action**: Always update the Agent Ecosystem section when agent files change.

**Analysis Required**:
- Did an agent's capabilities change? Update capabilities list.
- Did tools or permissions change? Update tools section.
- Was an agent added? Add new registry entry.
- Was an agent deleted? Remove entry and note in version history.
- Did agent relationships change? Update interaction map.

### Trigger: New or Modified Skill Files

**Locations to Watch**:
- `.cursor/skills/**/*`
- `~/.cursor/skills/**/*` (if accessible)

**Action**: Always update the Skill Registry section when skill files change.

**Analysis Required**:
- Did a skill's purpose or capabilities change? Update skill description.
- Was a skill added? Add new registry entry in Skill Registry.
- Was a skill deleted? Remove entry and note in version history.
- Did skill integration points change? Update references to agents or workflows.
- Does the skill reference AGENTS.md sections? Ensure those sections exist.

### Trigger: Configuration File Changes

**Files to Watch**:
- `package.json`, `requirements.txt`, `Cargo.toml`, `go.mod`
- `.eslintrc.*`, `.prettierrc.*`, `tsconfig.json`
- `vite.config.*`, `webpack.config.*`, `next.config.*`
- `.github/workflows/*`, `.gitlab-ci.yml`
- `Dockerfile`, `docker-compose.yml`

**Action**: Update relevant sections based on which config changed.

**Analysis Required**:
- Dependency changes? Update Key Dependencies section.
- Build config changes? Update Deployment & Build section.
- Linting rule changes? Update Development Conventions section.
- CI/CD changes? Update Deployment & Build section.

### Trigger: Major Structural Changes

**Patterns to Watch**:
- New directories created at project root
- Directories renamed or moved
- Package/module structure reorganization

**Action**: Update Project Structure section.

**Analysis Required**:
- Does this reflect an architectural shift? Update Architectural Patterns.
- Does this change where code lives? Update file locations in agent descriptions.
- Does this affect conventions? Update Development Conventions.

### Trigger: Documentation Changes

**Files to Watch**:
- `README.md`
- `CONTRIBUTING.md`
- `docs/**/*`
- `ARCHITECTURE.md`, `DESIGN.md`

**Action**: Review and potentially update Project Overview and conventions.

**Analysis Required**:
- Did project description change? Update overview.
- Did contribution guidelines change? Update conventions.
- Did architectural docs change? Update patterns section.

### Trigger: Test File Changes

**Patterns to Watch**:
- Test directory structure changes
- New test utilities or helpers
- Testing framework changes

**Action**: Update Testing Strategy section if patterns change.

**Analysis Required**:
- Are tests organized differently? Update test organization.
- New testing approaches? Document them.
- Coverage targets changed? Update expectations.

### False Positives (Don't Trigger Updates)

Do NOT update AGENTS.md for:
- Regular code changes in source files (unless they introduce new patterns)
- Minor dependency version bumps
- Temporary or experimental files
- Generated files or build artifacts
- Log files or cache directories
- Individual test file additions (unless they change testing strategy)

The key principle: update when project context or agent ecosystem changes, not on routine code modifications.

---

## Cursor Rule Specification

When `auto_watch` is enabled, generate this cursor rule:

```markdown
# Cursor Rule: AGENTS.md Auto-Maintainer

## Purpose

Automatically maintain AGENTS.md as a living document that stays synchronized with project changes.

## Activation Triggers

This rule activates when any of the following file patterns change:

### High Priority (Always Review)
- `.cursor/agents/**/*` - Agent definitions
- `.cursor/skills/**/*` - Skill definitions
- `.cline/agents/**/*` - Agent definitions
- `.agents/**/*` - Agent definitions
- `agents/**/*` - Agent definitions
- `package.json` - Dependencies
- `requirements.txt` - Python dependencies
- `Cargo.toml` - Rust dependencies
- `go.mod` - Go dependencies

### Medium Priority (Evaluate Impact)
- `README.md` - Project overview
- `CONTRIBUTING.md` - Contribution guidelines
- `.eslintrc.*` - Linting rules
- `.prettierrc.*` - Formatting rules
- `tsconfig.json` - TypeScript configuration
- `*config.*` - Various config files
- `.github/workflows/*` - CI/CD pipelines
- `Dockerfile` - Deployment configuration

### Low Priority (Check for Structural Changes)
- New root-level directories
- Directory renames or moves
- `docs/**/*` - Documentation changes

## Behavior

When activated:

1. **Analyze the Change**
   - Identify what files were modified, added, or deleted
   - Determine which section(s) of AGENTS.md are affected
   - Assess whether the change represents a meaningful context shift

2. **Decision Process**
   - If the change is routine code (source files, minor edits): **No action**
   - If the change affects project structure, agents, or configuration: **Propose update**
   - If uncertain: **Ask user** whether update is warranted

3. **Update Proposal**
   When an update is warranted:
   
   ```
   📋 AGENTS.md Update Detected
   
   Changed file(s): {{list}}
   Affected section(s): {{sections}}
   
   Proposed update:
   {{Show the specific changes to make}}
   
   Would you like me to:
   [1] Apply this update automatically
   [2] Let me review and modify first
   [3] Skip this update
   ```

4. **Apply Update**
   - Modify only the relevant section(s) of AGENTS.md
   - Update the "Last Updated" timestamp
   - Add entry to version history if significant
   - Preserve all other content unchanged

5. **Verification**
   After updating, confirm:
   - YAML/Markdown structure remains valid
   - No information was accidentally lost
   - Cross-references are still accurate
   - Table of contents is synchronized

## Operating Principles

**Precision over Frequency**
Don't update on every minor change. Focus on meaningful context shifts that would help developers or agents understand the project better.

**Explain Changes**
When proposing updates, always explain what changed and why it matters to project context.

**Preserve History**
Significant updates should be noted in the version history section. Minor corrections don't need history entries.

**Fail Gracefully**
If uncertain whether to update, ask rather than guessing. False negatives (missed updates) are better than false positives (spurious updates).

**Consistency Check**
After any update, verify that the document remains internally consistent. Agent references should match actual agents, file paths should be correct, etc.

## Special Cases

**New Agent Added**
- Priority: High
- Action: Add complete agent registry entry
- Notify: "New agent '{{name}}' discovered and documented"

**Agent Removed**
- Priority: High  
- Action: Remove registry entry, note in history
- Notify: "Agent '{{name}}' removed from documentation"

**New Skill Added**
- Priority: High
- Action: Add complete skill registry entry
- Notify: "New skill '{{name}}' discovered and documented"

**Skill Removed**
- Priority: High
- Action: Remove registry entry, note in history
- Notify: "Skill '{{name}}' removed from documentation"

**Major Dependency Added**
- Priority: Medium
- Action: Add to Key Dependencies with context
- Notify: "New major dependency '{{name}}' documented"

**Configuration Override**
- Priority: Low
- Action: Note the override in relevant section
- Check: Is this a temporary change or new pattern?

**Documentation-Only Changes**
- Priority: Variable
- Action: Evaluate if it reflects project reality changes
- Often: No update needed unless conventions changed

## User Preferences

Some users may want different update frequencies or levels of automation. Support these modes:

**Aggressive Mode**
- Update on most changes
- Prefer action over asking
- Good for: Solo developers, rapidly changing projects

**Balanced Mode** (Default)
- Update on clear triggers
- Ask when uncertain
- Good for: Small teams, moderate stability

**Conservative Mode**
- Update only on major changes
- Always ask before updating
- Good for: Large teams, stable projects

## Meta-Awareness

This rule itself is part of the project's agent ecosystem. When AGENTS.md is updated, consider whether this rule's behavior should also be documented or refined.

If project conventions evolve in ways that affect how context should be tracked, propose updates to both AGENTS.md and this rule.

---

*This rule was auto-generated by the AGENTS.md Context Compiler.*
```

---

## Generation Workflow

When executing this command, follow these steps in order:

### Step 1: Initial Scan
Scan the project with the specified depth:
- Shallow: Root level + immediate subdirectories
- Medium: 3 levels deep (recommended)
- Deep: Full recursive scan (may be slow on large projects)

### Step 2: Extract Context
For each discovered element (agents, configs, docs), extract relevant information and categorize it into the appropriate AGENTS.md section.

### Step 3: Generate Document
Build the complete AGENTS.md file following the structure above. Fill in all sections with discovered information, using placeholders for missing data.

### Step 4: Create Cursor Rule
If `auto_watch` is true, generate the cursor rule file and place it in `.cursor/rules/agents-maintainer.md`.

### Step 5: Verification
Perform these checks before finalizing:
- [ ] All agent file paths are correct
- [ ] No broken internal references
- [ ] Table of contents matches headings
- [ ] Timestamp is current
- [ ] Version history initialized

### Step 6: Summary Report
Provide a summary of what was generated:

```
✅ AGENTS.md Context Compilation Complete

📊 Statistics:
- Agents discovered: {{count}}
- Sections populated: {{count}}/11
- Dependencies cataloged: {{count}}
- Files analyzed: {{count}}
- Confidence level: {{high|medium|low}}

📂 Files Created:
- AGENTS.md ({{file_size}})
- .cursor/rules/agents-maintainer.md ({{if auto_watch}})

🔍 Needs Attention:
{{List any sections that need manual review or couldn't be auto-filled}}

💡 Next Steps:
1. Review AGENTS.md for accuracy
2. Fill in any missing sections manually
3. Test the auto-maintainer by making a config change
4. Share with team for feedback

The document is now live and will auto-update as your project evolves.
```

---

## Quality Standards

The generated AGENTS.md must meet these criteria:

- **Completeness**: All sections present, even if some say "Not applicable"
- **Accuracy**: Information matches actual project state
- **Clarity**: Technical enough to be useful, clear enough for newcomers
- **Currency**: Timestamp is accurate, information is up-to-date
- **Maintainability**: Structure supports easy updates
- **Actionability**: Readers know what to do with the information

## Error Handling

If the scan encounters issues:

- **No agents found**: Still generate document, note in Agent Ecosystem section
- **Access denied**: Skip protected directories, note in meta info
- **Malformed agent configs**: Document what was found, flag for review
- **Missing README**: Generate overview from available info
- **Large codebase**: Offer to run in batches or reduce depth

---

## Final Notes

This system creates a symbiotic relationship between your documentation and your codebase. The AGENTS.md file becomes the single source of truth for project context, while the cursor rule ensures it never drifts from reality.

Treat the initial generation as a foundation that improves over time. The more the project evolves, the more valuable this maintained context becomes, creating a compound effect where documentation quality increases alongside project maturity.