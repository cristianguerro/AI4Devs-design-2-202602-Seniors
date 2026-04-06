---
name: create-prd
description: "Create a Product Requirements Document (PRD). Use when: writing PRD, defining product requirements, documenting product scope, creating product specification, defining non-goals, setting KPIs, product planning document."
argument-hint: "Provide product name and context or reference documents"
---

# Create PRD

## When to Use
- Starting a new product or feature initiative
- Documenting requirements for an existing product
- Formalizing product scope and goals
- The user asks to create, generate, or write a PRD

## Procedure

### Step 1: Gather Context
Before generating the PRD, collect the following from the user:
1. **Product/Feature Name**
2. **Problem Statement**: What problem does this solve?
3. **Target Users**: Who are the users/personas?
4. **Existing Documents**: Ask the user to provide or reference any designs, specs, or documents
5. **Artifact Placement**: Check if a preference was already set. If not, ask whether artifacts (roadmap, story map, user stories, backlog, tickets) should be embedded or in separate files with links.
6. **PRD Structure Approval**: Present the default PRD structure below and ask the user to approve it or request modifications before generation.

Do NOT proceed until you have sufficient context. Ask clarifying questions.

### Step 2: Generate the PRD
Use the following structure. Every section is required unless explicitly waived by the user.

````markdown
# Product Requirements Document (PRD): {Product Name}

## 1. Overview
- **Product Name**: 
- **Document Version**: 
- **Author**: 
- **Date**: 
- **Status**: [Draft | In Review | Approved]

## 2. Problem Statement
{Description of the problem being solved, supported by data or user research if available}

## 3. Goals & Objectives
{Measurable goals aligned to business outcomes. Use SMART criteria.}

## 4. Non-Goals / Out-of-Scope
| Item | Reason | Revisit Phase |
|------|--------|---------------|
| {Item} | {Why it's excluded} | {When to reconsider} |

> **Important**: This section is mandatory. Explicitly stating what is NOT in scope prevents scope creep and aligns stakeholders. Every item should include a rationale and a phase when it may be reconsidered.

## 5. Product Roadmap
{Embedded roadmap OR link to separate file}

> Create this artifact with the `create-product-roadmap` skill.
> If stored separately, link it here:
> See: [product-roadmap.md](./product-roadmap.md)

## 6. Epics
| Epic ID | Epic Name | Outcome | Dependencies | Phase |
|---------|-----------|---------|--------------|-------|
| EPIC-01 | {Epic name} | {Business/user outcome} | {Dependencies} | {Phase} |

> Epics are mandatory before user story generation. Each epic must map back to the roadmap and forward to user stories.

## 7. Target Users & Personas
| Persona | Role | Key Needs | Pain Points |
|---------|------|-----------|-------------|

## 8. Functional Requirements
> Structure requirements in sequential phases with explicit dependencies to enable modular development and improve AI agent readability.

### Phase 1: {Phase Name} — Foundation
- **Goal**: {What this phase achieves}
- **Dependencies**: None
- **Requirements**:
  - FR-1.1: {Requirement description}
  - FR-1.2: {Requirement description}
- **Deliverables**: {What is delivered at end of this phase}

### Phase 2: {Phase Name}
- **Goal**: {What this phase achieves}
- **Dependencies**: Phase 1 (FR-1.1, FR-1.2)
- **Requirements**:
  - FR-2.1: {Requirement description}
  - FR-2.2: {Requirement description}
- **Deliverables**: {What is delivered at end of this phase}

### Phase N: {Phase Name}
- **Goal**: {What this phase achieves}
- **Dependencies**: {List specific phases and requirement IDs}
- **Requirements**:
  - FR-N.1: {Requirement description}
- **Deliverables**: {What is delivered at end of this phase}

## 9. Non-Functional Requirements
- **Performance**: {Response times, throughput targets}
- **Security**: {Authentication, authorization, data protection}
- **Scalability**: {Expected growth, scaling strategy}
- **Availability**: {Uptime SLA, disaster recovery}
- **Accessibility**: {WCAG compliance level, standards}

## 10. KPIs & Success Metrics
| KPI | Description | Baseline | Target | Measurement Method | Review Frequency |
|-----|-------------|----------|--------|--------------------|------------------|
| {KPI Name} | {What it measures} | {Current value} | {Goal value} | {How it's measured} | {When reviewed} |

> **Important**: This section is mandatory. Every PRD must define measurable KPIs that link directly to the Goals & Objectives (Section 3). Include at least one KPI per goal.

## 11. User Story Map
{Embedded user story map OR link to separate file}

> Create this artifact with the `create-user-story-map` skill.
> If stored separately, link it here:
> See: [user-story-map.md](./user-story-map.md)

## 12. User Stories
{Embedded user stories OR link to separate file}
> See: [user-stories.md](./user-stories.md) *(if separate file)*

## 13. Product Backlog
{Embedded backlog OR link to separate file}
> See: [product-backlog.md](./product-backlog.md) *(if separate file)*

## 14. Technical Considerations
- **Architecture**: {High-level architecture decisions}
- **Integrations**: {Third-party services, APIs}
- **Data Model**: {Key entities and relationships}
- **Tech Stack**: {Languages, frameworks, infrastructure}

## 15. UX/UI Considerations
{Wireframes, user flows, design references, design system}

## 16. Risks & Mitigations
| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|

## 17. Dependencies & Constraints
| Dependency | Type | Owner | Status |
|------------|------|-------|--------|

## 18. Timeline & Milestones
| Phase | Milestone | Target Date | Status |
|-------|-----------|-------------|--------|

## 19. Stakeholders & Sign-off
| Name | Role | Status | Date |
|------|------|--------|------|

## Appendix
- **Glossary**: {Domain-specific terms}
- **References**: {Links to research, designs, competitor analysis}
- **Change Log**:
  | Date | Author | Version | Change Description |
  |------|--------|---------|-------------------|
````

### Step 3: Review with User
- Present the generated PRD to the user
- Explicitly confirm the roadmap structure, epic list, and whether the Mermaid visuals are clear and useful
- Ask for feedback on each section
- Iterate until the user approves

### Step 4: Next Steps
After PRD approval, suggest:
1. Validating the roadmap and epics if not already approved
2. Creating the product roadmap if it has not been created yet (use `create-product-roadmap`)
3. Creating the user story map (use `create-user-story-map`)
4. Creating user stories (use `create-user-story` skill)
5. Prioritizing the backlog (use `prioritize-backlog` skill)
6. Creating work tickets (use `create-work-ticket` skill)

## Key Rules
- **Non-Goals/Out-of-Scope** section is MANDATORY — never skip it
- **Product Roadmap** section should be generated through the `create-product-roadmap` skill when needed
- **Epics** must be defined before user stories are created
- **User Story Map** section should be generated through the `create-user-story-map` skill when needed
- **KPIs & Success Metrics** section is MANDATORY — never skip it
- Functional requirements MUST be organized in sequential phases with explicit dependencies
- Each phase must declare its dependencies on prior phases
- Requirement IDs must follow the pattern `FR-{phase}.{number}` for traceability
- Ask the user to approve the PRD structure before drafting the document
- Do NOT invent requirements — only document what the user provides or confirms
