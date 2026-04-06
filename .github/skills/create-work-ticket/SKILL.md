---
name: create-work-ticket
description: "Create detailed work tickets for development teams. Use when: creating tickets, writing development tasks, breaking down user stories into work items, creating Jira tickets, task breakdown, sprint work items."
argument-hint: "Provide user stories or backlog items to break into work tickets"
---

# Create Work Ticket

## When to Use
- Breaking user stories into actionable development tickets
- Creating work items for sprint planning
- Defining tasks with full context for developers
- The user asks to create, write, or generate work tickets

## Procedure

### Step 1: Gather Context
1. Read the PRD, user stories, and backlog if available
2. Identify which user stories or backlog items need to be broken into tickets
3. Check the user's artifact placement preference (embedded in PRD or separate file)

### Step 2: Generate Work Tickets
For each ticket, use the following template:

```markdown
## Ticket: {TICKET-ID}

### Title
{Concise, action-oriented title — starts with a verb (e.g., "Implement", "Create", "Fix", "Add")}

### Description
{Detailed description of the work to be done. Include:
- Business context and why this work matters
- Technical context and approach guidance
- Scope boundaries (what's included and excluded)}

### Acceptance Criteria
- [ ] **Given** {precondition} **When** {action} **Then** {expected result}
- [ ] **Given** {precondition} **When** {action} **Then** {expected result}
- [ ] {Additional non-BDD criteria if needed}

### Priority
{Must Have | Should Have | Could Have | Won't Have}

### Estimation
- **Story Points**: {points — leave blank if not yet estimated}
- **T-Shirt Size**: {XS | S | M | L | XL — leave blank if not yet estimated}
- **Estimated Hours**: {hours — leave blank if not yet estimated}

### Assignee
- **Assigned to**: {Name/Team — leave blank if not yet assigned}
- **Reviewer**: {Name — leave blank if not yet assigned}

### Tags
{Comma-separated tags: frontend, backend, database, API, bug, feature, tech-debt, infrastructure, testing, documentation, etc.}

### Comments
| Date | Author | Comment |
|------|--------|---------|
| {YYYY-MM-DD} | {Author} | {Initial ticket creation} |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | {Related US-ID} | {link or reference} |
| PRD Requirement | {FR-X.X} | {link or reference} |
| Design | {Figma/Mockup} | {link} |
| Documentation | {Technical doc} | {link} |
| Depends On | {TICKET-ID} | {link or reference} |
| Blocks | {TICKET-ID} | {link or reference} |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| {YYYY-MM-DD} | {Author} | Ticket created |
```

### Step 3: Ticket ID Convention
- Ticket IDs follow the pattern: `TK-{number}` (e.g., TK-001, TK-002)
- Group related tickets by user story for easy navigation

### Step 4: Validate Tickets
For each ticket, verify:
1. **Title** is clear and action-oriented
2. **Description** provides enough context for a developer to start work
3. **Acceptance criteria** are testable and unambiguous
4. **Links** trace back to user story and PRD requirement
5. **Tags** are appropriate for filtering and organization
6. **Dependencies** (Depends On / Blocks) are correctly identified

### Step 5: Place the Artifact
Based on the user's preference:
- **Embedded**: Add tickets under a new "Work Tickets" section in the PRD (after Section 10)
- **Separate file**: Create `work-tickets.md` in the same directory and add a link in the PRD:
  ```markdown
  ## Work Tickets
  > See: [work-tickets.md](./work-tickets.md)
  ```

### Step 6: Review with User
- Present the generated tickets
- Ask for feedback on scope, descriptions, and acceptance criteria
- Iterate until approved

## Key Rules
- Every ticket MUST link back to a user story (US-ID) and PRD requirement (FR-X.X)
- Every ticket MUST have at least one acceptance criterion
- Titles MUST be action-oriented and start with a verb
- The change log MUST be initialized with the creation entry
- Dependencies between tickets MUST be explicitly documented in Links & Resources
- Do NOT estimate tickets during creation unless the user requests it — suggest using the `estimate-ticket` skill
- If a ticket is too large (more than 2-3 days of work), recommend splitting it into smaller tickets
- Do NOT invent work — only create tickets for confirmed requirements
