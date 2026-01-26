---
name: implement
description: "Implement design document following project conventions and patterns"
args:
  - name: design_doc
    description: "Path to design document to implement"
    isRequired: true
  - name: start_task
    description: "Task number to start from (default: 1, implement all)"
    isRequired: false
  - name: end_task
    description: "Task number to end at (default: all tasks)"
    isRequired: false
---

# Implement

Implement a design document following project conventions and patterns.

## Process

1. Read design doc and understand functional specifications
2. Review technical design and architecture
3. Follow implementation plan tasks in order
4. Implement following patterns from AGENTS.md
5. Write tests according to design doc testing strategy
6. Verify against acceptance criteria and success metrics
7. Update documentation as needed

## Implementation Flow

**PRD → Design Doc → Implementation**

1. **PRD** defines product and phases
2. **Design Doc** defines functional specs for a PRD phase
3. **Implementation** builds the design doc

## Reference

For detailed guidance, refer to:
- **Design Doc**: Contains functional specs, technical design, and implementation plan
- **AGENTS.md**: Project conventions, architectural patterns, testing strategy, code style
- **Related Design Docs**: For dependencies and integration points

## Output

Implement all tasks from design doc (or specified range), ensuring:
- ✅ All functional requirements are met
- ✅ Technical design is followed
- ✅ Tests are written per testing strategy
- ✅ Code follows project conventions (AGENTS.md)
- ✅ Acceptance criteria are satisfied
- ✅ Success metrics are met
