---
name: prioritize-backlog
description: "Prioritize product backlog using MoSCoW methodology. Use when: prioritizing user stories, organizing backlog, MoSCoW prioritization, ranking features, sprint planning, release planning, backlog grooming."
argument-hint: "Provide user stories or PRD reference to prioritize"
---

# Prioritize Backlog

## When to Use
- Organizing user stories into a prioritized backlog
- Applying MoSCoW prioritization to features
- Planning releases or sprints
- The user asks to prioritize, rank, or organize the backlog

## Procedure

### Step 1: Gather Context
1. Read the PRD and user stories (embedded or from separate file)
2. Understand the project goals and KPIs (PRD Sections 3 and 8)
3. Review the Non-Goals/Out-of-Scope (PRD Section 4) — items listed as "Won't Have" may already be defined there
4. Check the user's artifact placement preference (embedded in PRD or separate file)

### Step 2: Apply MoSCoW Prioritization
Classify each user story using these criteria:

| Category | Definition | Criteria |
|----------|-----------|----------|
| **Must Have** (P0) | Critical for launch. Product fails without these. | Core functionality, legal/compliance, security requirements, blockers for other Must Haves |
| **Should Have** (P1) | Important but not critical. Workarounds exist. | Significant value, strong user demand, but launch is possible without them |
| **Could Have** (P2) | Desirable if time/resources permit. | Nice-to-have, improves UX, low risk to defer |
| **Won't Have** (P3) | Explicitly deferred to a future release. | Out of scope for current release, but acknowledged for future consideration |

### Step 3: Generate the Backlog Artifact

```markdown
# Product Backlog: {Product Name}

**Last Updated**: {Date}
**Product Owner**: {Name}
**Prioritization Method**: MoSCoW

## Must Have (P0 — Critical for launch)
| ID | User Story | Description | Effort | Sprint | Dependencies | Status |
|----|-----------|-------------|--------|--------|--------------|--------|
| US-001 | {Title} | {Brief description} | {SP} | {Sprint #} | {Dependencies} | {Not Started / In Progress / Done} |

## Should Have (P1 — Important but not critical)
| ID | User Story | Description | Effort | Sprint | Dependencies | Status |
|----|-----------|-------------|--------|--------|--------------|--------|
| US-010 | {Title} | {Brief description} | {SP} | {Sprint #} | {Dependencies} | {Status} |

## Could Have (P2 — Desirable if time permits)
| ID | User Story | Description | Effort | Sprint | Dependencies | Status |
|----|-----------|-------------|--------|--------|--------------|--------|
| US-020 | {Title} | {Brief description} | {SP} | {Sprint #} | {Dependencies} | {Status} |

## Won't Have This Release (P3 — Explicitly deferred)
| ID | User Story | Description | Rationale for Deferral | Revisit |
|----|-----------|-------------|------------------------|---------|
| US-030 | {Title} | {Brief description} | {Why deferred} | {Phase/Release to reconsider} |

## Summary
| Category | Count | Total Story Points |
|----------|-------|--------------------|
| Must Have | {n} | {sp} |
| Should Have | {n} | {sp} |
| Could Have | {n} | {sp} |
| Won't Have | {n} | N/A |
| **Total** | {n} | {sp} |

## Prioritization Rationale
{Brief explanation of the prioritization decisions, trade-offs made, and alignment with project goals and KPIs}
```

### Step 4: Validate Prioritization
Review with the user:
1. Are all Must Haves truly critical for launch?
2. Are there dependencies between items that affect ordering?
3. Does the total effort for Must Haves fit within the available capacity?
4. Are Won't Have items properly captured for future consideration?
5. Does the prioritization align with the PRD goals and KPIs?

### Step 5: Place the Artifact
Based on the user's preference:
- **Embedded**: Add the backlog under Section 10 of the PRD
- **Separate file**: Create `product-backlog.md` in the same directory and add a link in Section 10 of the PRD:
  ```markdown
  ## 10. Product Backlog
  > See: [product-backlog.md](./product-backlog.md)
  ```

### Step 6: Review with User
- Present the prioritized backlog
- Ask for feedback and iterate
- Confirm prioritization before proceeding

## Key Rules
- Every user story MUST be classified into exactly one MoSCoW category
- Won't Have items MUST include a rationale and a revisit timeline
- The backlog MUST include a summary table with counts and total story points
- Dependencies between stories must be visible in the backlog
- Prioritization must align with PRD goals and KPIs — explain the rationale
- Do NOT prioritize without understanding the project goals first
- If story points are not yet estimated, leave the Effort column blank and recommend using the `estimate-ticket` skill
