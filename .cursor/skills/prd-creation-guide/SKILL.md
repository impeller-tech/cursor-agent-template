---
name: prd-creation-guide
description: "Comprehensive guide for creating Product Requirements Documents. Use when defining products, creating PRDs, or when detailed product planning guidance is needed."
---

# PRD Creation Guide

Complete guide for creating Product Requirements Documents that define products and establish implementation phases.

## Quick Start

Create a PRD that defines the product, its goals, and phases for implementation. The PRD serves as the foundation for design docs and implementation.

## PRD Structure

A PRD should include:

```markdown
# Product Requirements Document: {{Product Name}}

## Overview
- **Product Name**: {{name}}
- **Version**: {{version}}
- **Status**: {{draft|review|approved}}
- **Last Updated**: {{date}}
- **Owner**: {{product owner}}

## Problem Statement
{{Clear description of the problem this product solves}}

## Goals & Objectives
- Primary goal: {{main objective}}
- Success metrics: {{how success is measured}}
- Target users: {{who benefits from this}}

## Product Phases

### Phase 1: {{Phase Name}}
**Goal**: {{What this phase achieves}}
**Scope**: {{What's included}}
**Deliverables**: {{What's produced}}
**Dependencies**: {{What's needed before this phase}}
**Success Criteria**: {{How to know it's done}}

### Phase 2: {{Phase Name}}
[Same structure as Phase 1]

[Continue for all phases]

## User Stories

### Phase 1 Stories
- As a {{user type}}, I want {{action}} so that {{benefit}}
- [Additional stories]

### Phase 2 Stories
[Stories for Phase 2]

## Technical Considerations
- Platform requirements: {{platforms}}
- Performance requirements: {{performance needs}}
- Security requirements: {{security needs}}
- Integration requirements: {{external systems}}

## Constraints & Assumptions
- Constraints: {{limitations}}
- Assumptions: {{assumptions made}}
- Risks: {{potential risks}}

## Timeline
- Phase 1: {{start}} - {{end}}
- Phase 2: {{start}} - {{end}}
- Overall: {{start}} - {{end}}

## Next Steps
1. Review and approve PRD
2. Create design docs for Phase 1
3. Begin implementation planning
```

## Phase Definition Guidelines

### What Makes a Good Phase

Each phase should be:
- **Self-contained**: Can be understood independently
- **Deliverable**: Produces something tangible
- **Sequential**: Builds on previous phases logically
- **Testable**: Has clear success criteria
- **Scoped**: Not too large or too small

### Phase Relationships

Document how phases relate:
- **Sequential**: Phase 2 depends on Phase 1 completion
- **Parallel**: Phases can be done simultaneously
- **Optional**: Phase may be skipped based on feedback
- **Iterative**: Phase may be repeated with refinements

### Phase Scope Guidelines

**Too Large** (break down):
- "Build entire user authentication system"
- "Implement all payment features"

**Too Small** (combine):
- "Add button to form"
- "Change text color"

**Just Right**:
- "User registration and email verification"
- "Payment processing for single transactions"

## PRD Best Practices

### Problem Statement
- Be specific about the problem
- Include context and background
- Quantify impact when possible
- Avoid solution details (save for design docs)

### Goals & Objectives
- Use SMART criteria (Specific, Measurable, Achievable, Relevant, Time-bound)
- Prioritize goals (must-have vs nice-to-have)
- Align with business objectives
- Define success metrics upfront

### User Stories Format
```
As a [user type],
I want [action/feature],
So that [benefit/value].
```

Include acceptance criteria:
- Given [context]
- When [action]
- Then [expected outcome]

### Technical Considerations
- Don't prescribe solutions (that's for design docs)
- Do specify requirements (performance, security, etc.)
- Identify constraints (platform, budget, time)
- Note integration points

## PRD to Design Doc Handoff

The PRD should provide enough detail for design docs to be created:

1. **Clear phases** - Each phase becomes one or more design docs
2. **Functional requirements** - What needs to be built
3. **Success criteria** - How to validate completion
4. **Dependencies** - What must exist first
5. **Constraints** - Limitations to consider

## Quality Checklist

Before finalizing a PRD, ensure:
- ✅ Problem statement is clear and specific
- ✅ Goals are measurable and achievable
- ✅ Phases are well-scoped and sequential
- ✅ User stories have acceptance criteria
- ✅ Technical considerations are documented
- ✅ Constraints and assumptions are explicit
- ✅ Timeline is realistic
- ✅ Each phase can be turned into design docs

## Integration with Project

Reference AGENTS.md for:
- Project conventions and patterns
- Technical stack and architecture
- Development workflows
- Testing strategies

Link to design docs when created:
- Each phase should map to design doc(s)
- Design docs reference the PRD phase they implement
