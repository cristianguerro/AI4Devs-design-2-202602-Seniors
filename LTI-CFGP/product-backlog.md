# Product Backlog: LTI ATS

**Last Updated**: 2026-04-05  
**Product Owner**: Cristhian Guerrero  
**Prioritization Method**: MoSCoW  
**Source PRD**: [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md)  
**User Stories**: [user-stories.md](./user-stories.md)  
**Work Tickets**: [work-tickets.md](./work-tickets.md)

---

## Must Have (P0 — Critical for launch)

These stories are required for the MVP to function as a complete recruiting workflow. Without any single one, the product cannot deliver its core value proposition of replacing spreadsheet + email hiring.

| ID | User Story | Epic | Description | Effort | Sprint | Dependencies | Status |
|----|-----------|------|-------------|--------|--------|--------------|--------|
| US-001 | Sign up & create company account | EPIC-01 | User creates account with company name, slug auto-generated, admin role assigned | 16 SP | — | None | Not Started |
| US-002 | Invite team members with roles | EPIC-01 | Admin invites recruiters/hiring managers via email with role assignment | 18 SP | — | US-001 | Not Started |
| US-003 | Configure company profile & branding | EPIC-01 | Admin sets company name, logo, website for branded career page | 11 SP | — | US-001 | Not Started |
| US-004 | Connect calendar (Google/Outlook) | EPIC-01 | Users connect calendar via OAuth2 for interview scheduling | — | — | US-001 | Not Started |
| US-006 | Create job posting with structured fields | EPIC-02 | Admin creates job listing with title, description, salary, location, remote flag | — | — | US-001 | Not Started |
| US-008 | Publish & syndicate to job boards | EPIC-02 | One-click publish to career page + Indeed + LinkedIn with async syndication | — | — | US-006 | Not Started |
| US-009 | View syndication status per board | EPIC-02 | Dashboard showing per-board status (published/pending/failed) with retry controls | — | — | US-008 | Not Started |
| US-010 | Close/archive job across all boards | EPIC-02 | One-action close/archive that withdraws from all boards and career page | — | — | US-008 | Not Started |
| US-012 | Receive applications via career page & boards | EPIC-03 | Centralized inbox for all inbound applications with source attribution | — | — | US-008 | Not Started |
| US-013 | Auto-parse resume data (AI) | EPIC-04 | NLP extraction of name, email, phone, work history, skills from PDF/DOCX resumes | — | — | US-012 | Not Started |
| US-014 | Review parsed candidate profile | EPIC-03 | Unified profile with parsed data, application history, notes, and communication log | — | — | US-012, US-013 | Not Started |
| US-015 | Detect duplicate candidates | EPIC-03 | Email-based deduplication links new applications to existing candidate records | — | — | US-012 | Not Started |
| US-016 | View candidates on Kanban board | EPIC-03 | Visual pipeline board with columns per stage, cards per application | — | — | US-005, US-012 | Not Started |
| US-017 | Drag card to advance or reject candidate | EPIC-03 | Drag-and-drop stage transitions that trigger STAGE_CHANGED events | — | — | US-016 | Not Started |
| US-018 | Add notes & score to application | EPIC-03 | Timestamped notes and 1–5 score by any team member, visible in real time | — | — | US-016 | Not Started |
| US-019 | Auto-send stage change email | EPIC-05 | Triggered email dispatch on pipeline stage transition via templates + SendGrid | — | — | US-017 | Not Started |
| US-021 | Send interview invitation with scheduling link | EPIC-06 | Auto-generate CSPRNG token (72h TTL) and send scheduling link on Interview stage | — | — | US-017, US-004 | Not Started |
| US-022 | Candidate self-selects available time slot | EPIC-06 | Self-scheduling portal shows interviewer's free slots for next 14 days | — | — | US-021 | Not Started |
| US-023 | Confirm booking & sync calendar event | EPIC-06 | Real-time availability check, calendar event creation, confirmation emails | — | — | US-022 | Not Started |
| US-024 | Send 24h reminder to candidate | EPIC-06 | Scheduled reminder email with interview details and reschedule/cancel links | — | — | US-023 | Not Started |
| US-025 | Candidate reschedules or cancels | EPIC-06 | One-click reschedule (re-opens portal) or cancel (deletes event, alerts recruiter) | — | — | US-023 | Not Started |
| US-026 | Record interview feedback & score | EPIC-03 | Post-interview feedback (text + 1–5 score) per interviewer on Interview record | — | — | US-023 | Not Started |
| US-027 | Hiring Manager approves or rejects | EPIC-03 | HM decision triggers stage change to Offer or Rejected with notifications | — | — | US-026 | Not Started |
| US-028 | Extend offer & send notification | EPIC-03 | Offer notification email dispatched via offer_extended template | — | — | US-027 | Not Started |
| US-029 | Mark candidate as hired | EPIC-03 | Terminal stage transition to Hired with timestamp for metrics | — | — | US-028 | Not Started |

---

## Should Have (P1 — Important but not critical)

These stories add significant value and polish to the MVP experience. The product can launch without them, but they are high-priority follow-ups within Phase 1 or early Phase 2.

| ID | User Story | Epic | Description | Effort | Sprint | Dependencies | Status |
|----|-----------|------|-------------|--------|--------|--------------|--------|
| US-005 | Customize pipeline stages | EPIC-01 | Admin adds, removes, reorders, and colors pipeline stages; defaults are sufficient for launch | — | — | US-001 | Not Started |
| US-007 | Preview job on branded career page | EPIC-02 | Render preview of posting as it will appear on career page before publishing | — | — | US-006, US-003 | Not Started |
| US-030 | Search past candidates by keyword | EPIC-07 | Full-text search across parsed resume data for candidate re-engagement (Phase 2) | — | — | US-013 | Not Started |
| US-031 | View pipeline analytics dashboard | EPIC-08 | Time-to-hire, stage conversion rates, source effectiveness, active counts (Phase 2) | — | — | US-012, US-008 | Not Started |

---

## Could Have (P2 — Desirable if time permits)

These stories enhance reach or add premium revenue but are not needed for core workflow or initial product-market fit validation.

| ID | User Story | Epic | Description | Effort | Sprint | Dependencies | Status |
|----|-----------|------|-------------|--------|--------|--------------|--------|
| US-011 | Syndicate to additional boards (Glassdoor) | EPIC-10 | Expand syndication beyond Indeed/LinkedIn using adapter pattern (Phase 2) | — | — | US-008 | Not Started |
| US-020 | AI-recommended shortlist | EPIC-09 | AI evaluates candidate-job fit and surfaces ranked shortlist (premium $99/mo add-on, Phase 2) | — | — | US-013, US-030 | Not Started |

---

## Won't Have This Release (P3 — Explicitly deferred)

These items are acknowledged but explicitly out of scope per the PRD Non-Goals section. Each includes a rationale and a target phase for reconsideration.

| ID | Item | Description | Rationale for Deferral | Revisit |
|----|------|-------------|------------------------|---------|
| — | Advanced AI screening / candidate ranking | AI-powered candidate scoring with bias mitigation | MVP focuses on admin automation, not hiring decisions; adds complexity and bias risk | Phase 2 (EPIC-09 is a first step) |
| — | Native mobile application | iOS/Android apps for recruiting on the go | Target users work on desktop; responsive web is sufficient for MVP | Phase 3 |
| — | Offer letter generation & e-signatures | Document generation with legally binding signatures | Specialized legal/compliance domain; users have existing tools (DocuSign) | Phase 2 |
| — | Advanced analytics & reporting | BI-grade dashboards with custom reports and exports | Basic metrics included in Phase 2 (US-031); advanced analytics deferred | Phase 3 |
| — | Multi-language / i18n support | UI and email templates in multiple languages | Initial launch targets English-speaking markets only | Phase 3 |
| — | Payroll / HRIS integration | Connect with BambooHR, Gusto, etc. | LTI is an ATS, not an HRIS; integration complexity too high for MVP | Phase 3 |
| — | Single Sign-On (SSO / SAML) | Enterprise authentication via corporate IdP | Enterprise feature; target segment uses email/password | Phase 3 |
| — | Video interview platform | Built-in video calling for interviews | Calendar sync generates Google Meet / Teams links natively; separate platform unnecessary | Not planned |
| — | Glassdoor and other boards (beyond Phase 2 scope) | Full marketplace of job board integrations | MVP ships with Indeed + LinkedIn; Glassdoor in Phase 2; others based on demand | Phase 2+ |

---

## Summary

| Category | Count | Total Story Points |
|----------|-------|--------------------|
| Must Have (P0) | 25 | — (not yet estimated) |
| Should Have (P1) | 4 | — |
| Could Have (P2) | 2 | — |
| Won't Have (P3) | 9 items | N/A |
| **Total Stories** | **31** | **—** |

---

## Prioritization Rationale

### Why this ordering?

**Must Have (25 stories)** — These 25 stories form the complete end-to-end recruiting workflow that LTI promises: sign up → post jobs → receive applications → parse resumes → manage pipeline → communicate automatically → schedule interviews → hire. Removing any one of these breaks the workflow chain. This directly maps to:
- **G1** (< 30 min time-to-first-post): US-001 → US-008 must be seamless
- **G2** (> 70% self-scheduling rate): US-021 → US-025 are the complete scheduling chain
- **G3** (≥ 60% admin time reduction): US-013, US-019 automate the biggest time sinks
- **G4** (< 2% candidate ghosting): US-019 ensures every stage change triggers communication

**Should Have (4 stories)** — These stories enhance the experience but have workarounds:
- *US-005* (custom pipeline stages): Default stages are sufficient for launch; customization is polish.
- *US-007* (career page preview): Admins can publish and verify; preview is a UX improvement.
- *US-030, US-031* (search + analytics): Phase 2 features that drive retention but aren't needed for initial adoption.

**Could Have (2 stories)** — Expansion and premium features:
- *US-011* (more job boards): Indeed + LinkedIn cover 80%+ of the SMB job posting market.
- *US-020* (AI shortlist): Revenue-driving add-on, but requires sufficient data volume to be valuable.

**Won't Have (9 items)** — Aligned with PRD Non-Goals. Each has a clear rationale and a target phase for reconsideration. None are needed for PMF validation with the target segment (5–100 employee companies in English-speaking markets).

### Dependency-aware ordering within Must Have

The Must Have stories follow the dependency chain from the product roadmap critical path:

```
US-001 (signup) → US-002/003/004 (setup)
                → US-006 (create job) → US-008 (publish) → US-012 (receive apps)
                                                          → US-013 (parse resume)
                                                          → US-014/015 (profile + dedup)
                → US-016 (kanban) → US-017 (drag) → US-019 (auto email)
                                                   → US-021 (scheduling link)
                                                   → US-022 → US-023 → US-024/025
                → US-026 → US-027 → US-028 → US-029 (hiring decision chain)
```

### Recommendation

Story points have not yet been estimated. Use the **estimate-ticket** skill to size each story before sprint planning. The 25 Must Have stories should be estimated first to determine if they fit within the planned MVP timeline.
