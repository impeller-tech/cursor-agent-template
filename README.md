# AI-Assisted Development Template

Template for AI-assisted development projects with structured commands, agents, and living documentation.

## Quick Start

1. Clone or use this template
2. Run `/init` to generate AGENTS.md
3. Create agents with `/create-agent` (optional)
4. Create skills with `/new-skill` (optional)

## Commands

- **`/init`** - Generate AGENTS.md with project context
- **`/create-agent`** - Create Cursor subagents
- **`/new-skill`** - Create Cursor skills
- **`/deslop`** - Remove AI-generated code slop

Commands reference detailed guidance in `.cursor/skills/` for comprehensive instructions.

## Structure

```
your-project/
├── .cursor/
│   ├── agents/          # Cursor AI agents
│   ├── commands/        # Custom commands
│   ├── skills/          # Detailed guidance (markdown)
│   └── rules/           # Auto-maintenance rules
├── .agents/             # Generic agent storage
├── agents/              # Project-specific agents
└── AGENTS.md            # Living context document
```

## Philosophy

- **Less is more** - Commands are concise, detailed guidance in skills
- **Less code, more markdown** - Better context through markdown documentation
- **Context is King** - AI assistants need good context
- **Documentation Must Live** - AGENTS.md auto-updates
- **Specialization > Generalization** - Purpose-built agents

## License

MIT License - see [LICENSE](LICENSE) file.

