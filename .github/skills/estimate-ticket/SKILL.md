---
name: estimate-ticket
description: "Estimate effort for work tickets using story points, T-shirt sizing, and hour estimates. Use when: estimating tickets, effort estimation, story point assignment, planning poker, capacity planning, sprint planning estimation, updating ticket estimates."
argument-hint: "Provide work tickets or ticket IDs to estimate"
---

# Estimate Ticket

## When to Use
- Estimating effort for newly created work tickets
- Re-estimating tickets after scope changes
- Creating an estimation report for sprint or release planning
- Updating existing ticket estimates
- The user asks to estimate, size, or assign story points to tickets

## Procedure

### Step 1: Gather Context
1. Read the work tickets to be estimated (from PRD, work-tickets.md, or user input)
2. Understand the technical complexity and scope of each ticket
3. Review any existing estimates or velocity data if available
4. Ask the user which estimation method to use if not already established:
   - **Planning Poker (Fibonacci)**: 1, 2, 3, 5, 8, 13, 21
   - **T-Shirt Sizing**: XS, S, M, L, XL, XXL
   - **Both with hour mapping**

### Step 2: Define the Estimation Scale
Present the scale to the user for confirmation:

```markdown
## Estimation Criteria
| Story Points | T-Shirt Size | Complexity | Typical Scope | Approx. Hours |
|-------------|-------------|------------|---------------|---------------|
| 1 | XS | Trivial | Config change, copy update, minor CSS fix | 1-2h |
| 2 | S | Low | Simple feature, minor bug fix, small refactor | 2-4h |
| 3 | S-M | Low-Medium | Well-understood task, single component | 4-8h |
| 5 | M | Medium | Standard feature, moderate complexity | 8-16h |
| 8 | L | Medium-High | Complex feature, multiple components, integration work | 16-24h |
| 13 | XL | High | Major feature, significant unknowns, cross-team coordination | 24-40h |
| 21 | XXL | Very High | Epic-level work — recommend decomposition | 40h+ |
```

> If the user has a custom scale, use that instead.

### Step 3: Estimate Each Ticket
For each ticket, evaluate:
1. **Complexity**: How technically complex is the work?
2. **Uncertainty**: How much is unknown or ambiguous?
3. **Effort**: How much raw work is involved?
4. **Risk**: What could go wrong or cause rework?

Provide a brief rationale for each estimate.

### Step 4: Generate Estimation Report

```markdown
# Effort Estimation Report: {Product/Sprint Name}

**Date**: {Date}
**Estimator(s)**: {Names}
**Method**: {Planning Poker | T-Shirt Sizing | Combined}

## Estimation Scale
| Story Points | T-Shirt Size | Complexity | Typical Scope | Approx. Hours |
|-------------|-------------|------------|---------------|---------------|
| 1 | XS | Trivial | Config change, copy update | 1-2h |
| 2 | S | Low | Simple feature, minor fix | 2-4h |
| 3 | S-M | Low-Medium | Well-understood task | 4-8h |
| 5 | M | Medium | Standard feature | 8-16h |
| 8 | L | Medium-High | Complex feature, multiple components | 16-24h |
| 13 | XL | High | Major feature, significant unknowns | 24-40h |
| 21 | XXL | Very High | Epic-level, needs decomposition | 40h+ |

## Ticket Estimates
| Ticket ID | Title | Complexity | Uncertainty | Story Points | T-Shirt Size | Est. Hours | Rationale |
|-----------|-------|------------|-------------|--------------|--------------|------------|-----------|
| TK-001 | {Title} | {Low/Med/High} | {Low/Med/High} | {SP} | {Size} | {Hours} | {Brief justification} |
| TK-002 | {Title} | {Low/Med/High} | {Low/Med/High} | {SP} | {Size} | {Hours} | {Brief justification} |

## Risks & Assumptions
| Ticket ID | Risk / Assumption | Impact on Estimate |
|-----------|------------------|-------------------|
| {TK-ID} | {Description} | {How it could change the estimate} |

## Velocity Reference (if available)
- **Team Velocity (avg)**: {SP per sprint}
- **Sprint Duration**: {weeks}
- **Capacity This Sprint**: {SP}

## Summary
| Metric | Value |
|--------|-------|
| Total Tickets Estimated | {n} |
| Total Story Points | {sp} |
| Total Estimated Hours | {hours} |
| Estimated Sprints Needed | {sp / velocity} |
| Tickets Flagged for Decomposition (>13 SP) | {n} |
```

### Step 5: Update Work Tickets
After estimates are approved, update the Estimation section in each work ticket:
```markdown
### Estimation
- **Story Points**: {points}
- **T-Shirt Size**: {size}
- **Estimated Hours**: {hours}
```

Also add a change log entry to each updated ticket:
```markdown
| {Date} | {Estimator} | Added effort estimation: {SP} SP, {Size}, {Hours}h |
```

### Step 6: Update Backlog
If a prioritized backlog exists, update the Effort column with the new estimates.

### Step 7: Review with User
- Present the estimation report
- Highlight any tickets flagged for decomposition (>13 SP)
- Ask for feedback and adjustments
- Confirm before updating ticket files

## Key Rules
- Every estimate MUST include a rationale — never assign points without justification
- Tickets estimated at 21+ story points MUST be flagged for decomposition
- Always present the estimation scale before estimating so the user can confirm or customize
- Update both the estimation report AND the individual tickets after approval
- Add change log entries to every ticket that gets updated
- If no velocity data is available, note this in the report and skip the sprint count calculation
- Do NOT estimate without understanding the ticket scope — read the full description and acceptance criteria first
