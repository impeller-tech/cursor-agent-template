---
name: create-prd
description: "Create Product Requirements Document that defines a product and establishes implementation phases"
args:
  - name: product_name
    description: "Name of the product"
    isRequired: true
  - name: output_file
    description: "Output file path for PRD (default: docs/prd-{product_name}.md)"
    isRequired: false
---

# Create PRD

Create a Product Requirements Document that defines a product and establishes phases for implementation.

## Process

1. Gather product requirements and user needs
2. Define problem statement and goals
3. Break down into implementation phases
4. Document user stories and acceptance criteria
5. Create PRD following structure in `.cursor/skills/prd-creation-guide/SKILL.md`

## Reference

For detailed guidance, refer to the **prd-creation-guide** skill at `.cursor/skills/prd-creation-guide/SKILL.md`. It includes:
- Complete PRD structure template
- Phase definition guidelines
- User story format
- Technical considerations
- PRD to design doc handoff process
- Quality checklist

## Output

Generate PRD file with:
- Problem statement and goals
- Product phases (each phase will become design doc(s))
- User stories with acceptance criteria
- Technical considerations
- Timeline and next steps

Each phase in the PRD should be scoped to become one or more design documents.
