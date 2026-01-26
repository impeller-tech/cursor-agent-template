---
name: design-doc-creation-guide
description: "Comprehensive guide for creating design documents from PRD phases. Use when creating design docs, defining functional specifications, or translating PRD phases into implementation plans."
---

# Design Document Creation Guide

Complete guide for creating design documents that define functional specifications based on PRD phases.

## Quick Start

Create design docs that translate PRD phases into detailed functional specifications. Design docs bridge the gap between product requirements and implementation.

## Design Doc Structure

A design doc should include:

```markdown
# Design Document: {{Feature/Component Name}}

## Metadata
- **Related PRD**: {{PRD name and phase}}
- **Phase**: {{Phase number and name}}
- **Status**: {{draft|review|approved|implemented}}
- **Last Updated**: {{date}}
- **Author**: {{designer/engineer}}
- **Reviewers**: {{reviewers}}

## Overview
{{Brief description of what this design doc covers}}

## Context
- **Problem**: {{What problem this solves (from PRD)}}
- **Goals**: {{What this design achieves (from PRD phase)}}
- **Scope**: {{What's in scope and out of scope}}

## Functional Specifications

### Feature: {{Feature Name}}
**Description**: {{What this feature does}}
**User Story**: {{From PRD}}
**Acceptance Criteria**: {{From PRD}}

**Functional Requirements**:
- FR-1: {{Requirement}}
- FR-2: {{Requirement}}

**User Flows**:
1. {{Step 1}}
2. {{Step 2}}
3. {{Step 3}}

**Edge Cases**:
- {{Edge case 1}}: {{How to handle}}
- {{Edge case 2}}: {{How to handle}}

### Feature: {{Feature Name}}
[Same structure for each feature]

## Technical Design

### Architecture
{{High-level architecture diagram or description}}

### Components
- **Component 1**: {{Purpose and responsibility}}
- **Component 2**: {{Purpose and responsibility}}

### Data Models
```typescript
// Example data structures
interface {{ModelName}} {
  // Fields
}
```

### APIs/Interfaces
- **API Endpoint**: {{Method}} {{Path}}
  - Request: {{Structure}}
  - Response: {{Structure}}
  - Errors: {{Error cases}}

### Algorithms/Logic
{{Key algorithms or business logic}}

## Implementation Plan

### Tasks
1. [ ] {{Task 1}}
2. [ ] {{Task 2}}
3. [ ] {{Task 3}}

### Dependencies
- Requires: {{What must be done first}}
- Blocks: {{What this unblocks}}

### Testing Strategy
- Unit tests: {{What to test}}
- Integration tests: {{What to test}}
- E2E tests: {{What to test}}

## Non-Functional Requirements

### Performance
- Response time: {{target}}
- Throughput: {{target}}
- Scalability: {{requirements}}

### Security
- Authentication: {{requirements}}
- Authorization: {{requirements}}
- Data protection: {{requirements}}

### Reliability
- Uptime: {{target}}
- Error handling: {{approach}}
- Monitoring: {{what to monitor}}

## Design Decisions

### Decision 1: {{Decision}}
**Context**: {{Why this decision was needed}}
**Options Considered**: {{Alternatives}}
**Chosen Solution**: {{What was chosen}}
**Rationale**: {{Why this was chosen}}
**Trade-offs**: {{What was given up}}

### Decision 2: {{Decision}}
[Same structure]

## Open Questions
- [ ] {{Question 1}}
- [ ] {{Question 2}}

## Risks & Mitigations
- **Risk 1**: {{Description}}
  - Mitigation: {{How to address}}
- **Risk 2**: {{Description}}
  - Mitigation: {{How to address}}

## Success Metrics
- {{Metric 1}}: {{How to measure}}
- {{Metric 2}}: {{How to measure}}

## References
- PRD: {{Link to PRD and phase}}
- Related Design Docs: {{Links to related docs}}
- Technical Docs: {{Links to relevant technical docs}}
- AGENTS.md: {{Relevant sections}}
```

## From PRD Phase to Design Doc

### Mapping PRD to Design

1. **Identify Phase Scope**
   - Review PRD phase goals and deliverables
   - Break down into features/components
   - Each major feature may need its own design doc

2. **Extract Requirements**
   - User stories from PRD
   - Acceptance criteria
   - Success metrics
   - Constraints and assumptions

3. **Define Functional Specs**
   - Translate user stories into functional requirements
   - Define user flows
   - Identify edge cases
   - Specify data needs

4. **Design Technical Solution**
   - Architecture and components
   - Data models
   - APIs and interfaces
   - Algorithms and logic

5. **Plan Implementation**
   - Break into tasks
   - Identify dependencies
   - Define testing approach

## Functional Specification Guidelines

### Writing Good Functional Requirements

**Format**: "The system SHALL [action] [condition]"

Examples:
- ✅ "The system SHALL validate email format before submission"
- ✅ "The system SHALL display error message when validation fails"
- ❌ "The system should be user-friendly"
- ❌ "The system needs to work well"

### User Flows

Document complete user journeys:
1. Start with user goal
2. Include all steps (happy path)
3. Document alternative paths
4. Include error handling
5. Show end states

### Edge Cases

Consider:
- Empty/null inputs
- Invalid inputs
- Boundary conditions
- Concurrent operations
- Failure scenarios
- Data inconsistencies

## Technical Design Guidelines

### Architecture Decisions

Document:
- Why this architecture was chosen
- What alternatives were considered
- What trade-offs were made
- How it fits with existing system (reference AGENTS.md)

### Component Design

For each component:
- Single responsibility
- Clear interfaces
- Dependencies documented
- Integration points identified

### Data Models

Define:
- Required fields
- Optional fields
- Validation rules
- Relationships
- Indexes (if applicable)

## Design Doc Best Practices

### Clarity
- Use diagrams for complex flows
- Include examples
- Define terminology
- Reference existing patterns from AGENTS.md

### Completeness
- Cover all features from PRD phase
- Address all acceptance criteria
- Include error handling
- Document edge cases

### Actionability
- Tasks are specific and clear
- Dependencies are explicit
- Testing strategy is defined
- Success metrics are measurable

## Design Doc to Implementation Handoff

The design doc should provide:
1. **Clear functional specs** - What to build
2. **Technical design** - How to build it
3. **Implementation plan** - Tasks and order
4. **Testing strategy** - How to validate
5. **Success criteria** - How to know it's done

## Quality Checklist

Before finalizing a design doc, ensure:
- ✅ All PRD phase requirements are addressed
- ✅ Functional specs are clear and testable
- ✅ Technical design follows project patterns (AGENTS.md)
- ✅ Implementation plan is actionable
- ✅ Testing strategy is defined
- ✅ Dependencies are documented
- ✅ Open questions are identified
- ✅ Success metrics align with PRD

## Integration with Project

Reference AGENTS.md for:
- Architectural patterns
- Development conventions
- Code style guidelines
- Testing strategies
- Deployment processes

Link to:
- PRD phase this implements
- Related design docs
- Implementation tasks/issues
