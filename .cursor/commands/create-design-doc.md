---
name: create-design-doc
description: "Create design document with functional specifications based on PRD phase"
args:
  - name: prd_phase
    description: "PRD phase to implement (reference PRD file and phase number/name)"
    isRequired: true
  - name: feature_name
    description: "Name of the feature/component being designed"
    isRequired: true
  - name: prd_file
    description: "Path to PRD file (default: find PRD in docs/ or root)"
    isRequired: false
  - name: output_file
    description: "Output file path for design doc (default: docs/design-{feature_name}.md)"
    isRequired: false
---

# Create Design Document

Create a design document that translates a PRD phase into detailed functional specifications.

## Process

1. Read PRD and identify the specified phase
2. Extract requirements, user stories, and acceptance criteria from PRD phase
3. Define functional specifications (what to build)
4. Design technical solution (how to build it)
5. Create implementation plan with tasks
6. Create design doc following structure in `.cursor/skills/design-doc-creation-guide/SKILL.md`

## Reference

For detailed guidance, refer to the **design-doc-creation-guide** skill at `.cursor/skills/design-doc-creation-guide/SKILL.md`. It includes:
- Complete design doc structure template
- Mapping PRD phases to design docs
- Functional specification guidelines
- Technical design best practices
- Design doc to implementation handoff
- Quality checklist

## Output

Generate design doc file with:
- Link to PRD phase being implemented
- Functional specifications (requirements, user flows, edge cases)
- Technical design (architecture, components, data models, APIs)
- Implementation plan (tasks, dependencies, testing strategy)
- Success metrics aligned with PRD phase

The design doc should provide everything needed to implement the PRD phase.
