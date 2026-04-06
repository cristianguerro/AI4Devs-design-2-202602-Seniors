---
name: create-user-story
description: "Create user stories following best practices. Use when: writing user stories, defining acceptance criteria, BDD scenarios, applying INVEST principle, 3 C's methodology, Given/When/Then criteria, breaking down requirements into stories."
argument-hint: "Provide requirements, features, or PRD reference to generate user stories from"
---

# Create User Story

## When to Use
- Translating PRD requirements into user stories
- Writing new user stories for a feature
- Refining existing user stories
- The user asks to create, write, or generate user stories

## Procedure

### Step 1: Gather Context
1. Read the PRD or requirements document if available
2. Verify that epics are already defined and approved in the PRD or a related artifact
3. Verify that a user story map already exists and has been approved
4. Identify the personas/roles from the PRD
5. Identify functional requirements to translate into stories
6. Check the user's artifact placement preference (embedded in PRD or separate file)

Do NOT generate user stories until epics and the user story map have been defined and approved.

### Step 2: Generate User Stories
For each approved epic and mapped requirement, generate a user story using the template below. Apply the **3 C's** (Card, Conversation, Confirmation) and validate against the **INVEST** principle.

```markdown
## User Story: {US-ID}

### Card
**As a** {persona/role}
**I want** {goal/desire}
**So that** {benefit/value}

### Conversation
- **Context**: {Background and business context}
- **Assumptions**: {Any assumptions made}
- **Dependencies**: {Related stories, prerequisite US-IDs, or PRD requirement IDs (FR-X.X)}
- **Notes**: {Discussion points, decisions made, edge cases}

### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: {Scenario title}
- **Given** {initial context/precondition}
- **When** {action/event}
- **Then** {expected outcome}

**Scenario 2**: {Scenario title}
- **Given** {initial context/precondition}
- **When** {action/event}
- **Then** {expected outcome}

### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ☐ | {Can be developed independently of other stories?} |
| **N**egotiable | ☐ | {Details can be discussed and refined?} |
| **V**aluable | ☐ | {Delivers clear value to user or business?} |
| **E**stimable | ☐ | {Team can estimate the effort?} |
| **S**mall | ☐ | {Fits within a single sprint?} |
| **T**estable | ☐ | {Has clear pass/fail acceptance criteria?} |

### Metadata
- **Priority**: {Must Have | Should Have | Could Have | Won't Have}
- **Story Points**: {Estimate — leave blank if not yet estimated}
- **Sprint**: {Sprint number — leave blank if not yet assigned}
- **Epic/Feature**: {Parent epic or feature name}
- **Epic ID**: {EPIC-XX reference}
- **PRD Requirement**: {FR-X.X reference}
- **Labels/Tags**: {Relevant tags}
```

### Step 3: Validate Each Story

For every story, verify:
1. **3 C's Compliance**:
   - **Card**: The "As a / I want / So that" is clear and specific
   - **Conversation**: Context and assumptions are documented
   - **Confirmation**: At least 2 BDD acceptance criteria scenarios exist
2. **INVEST Compliance**: All 6 criteria are checked and justified
3. **BDD Scenarios**: Each scenario follows strict Given/When/Then format
4. **Traceability**: Story links back to an approved epic and a PRD functional requirement (FR-X.X)

### Step 4: Place the Artifact
Based on the user's preference:
- **Embedded**: Add the stories under the PRD user stories section
- **Separate file**: Create `user-stories.md` in the same directory and add a link in the PRD:
  ```markdown
  ## 12. User Stories
  > See: [user-stories.md](./user-stories.md)
  ```

### Step 5: Review with User
- Present the generated stories
- Ask for feedback and iterate
- Confirm each story is complete before moving on

## Key Rules
- Never generate user stories before epics are defined and approved
- Never generate user stories before the `create-user-story-map` skill has been used and approved
- Every acceptance criterion MUST use Given/When/Then format — no exceptions
- Every story MUST have at least 2 BDD scenarios
- Every story MUST be validated against all 6 INVEST criteria
- User story IDs follow the pattern `US-{number}` (e.g., US-001, US-002)
- Epic IDs follow the pattern `EPIC-{number}` (e.g., EPIC-01, EPIC-02)
- Always link stories to PRD requirement IDs for traceability
- Do NOT invent user needs — derive stories only from documented or confirmed requirements
- If a story is too large (fails the "Small" INVEST check), recommend splitting it
