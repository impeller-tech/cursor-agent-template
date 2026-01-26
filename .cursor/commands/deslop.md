---
name: deslop
description: "Remove AI-generated code slop from branch by analyzing diff against main. Identifies and removes unnecessary comments, defensive code, type casts, and style inconsistencies introduced by AI assistants."
args:
  - name: base_branch
    description: "Base branch to compare against (default: main)"
    isRequired: false
    default: "main"
  - name: scope
    description: "Scope of analysis (all|staged|modified). 'all' checks all changes, 'staged' only staged files, 'modified' only modified files"
    isRequired: false
    default: "all"
  - name: report_level
    description: "Detail level of report (summary|detailed). 'summary' provides 1-3 sentence overview, 'detailed' lists all changes"
    isRequired: false
    default: "summary"
---

# Remove AI Code Slop

Analyze diff against base branch and remove AI-generated slop patterns while preserving intentional changes.

## Process

1. Get diff: `git diff {{base_branch}}...HEAD` (or `--cached`/`HEAD` based on `scope`)
2. Analyze each changed file for slop patterns
3. Remove slop while preserving intentional changes
4. Verify changes maintain consistency
5. Generate report based on `report_level`

## Reference

For detailed guidance, refer to the **code-slop-removal** skill at `.cursor/skills/code-slop-removal/SKILL.md`. It includes:
- Complete slop pattern identification guide
- Step-by-step removal process
- Common patterns and anti-patterns
- Integration with project conventions
- Quality checklist

## Slop Patterns to Identify

- Comment slop: Over-commenting, inconsistent commenting, redundant comments
- Defensive code slop: Unnecessary null checks, excessive try/catch, redundant validation
- Type safety slop: Casts to `any`, type assertions without proper types
- Style inconsistencies: Verbose variable names, inconsistent formatting, unnecessary abstractions

See `.cursor/skills/code-slop-removal/SKILL.md` for detailed examples and patterns.

## Output

Provide report based on `report_level`:
- **Summary**: 1-3 sentence overview of changes
- **Detailed**: File-by-file breakdown with explanations
