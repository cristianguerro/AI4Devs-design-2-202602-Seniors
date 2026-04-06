# Product Requirements Document (PRD): LTI ATS

## 1. Overview

- **Product Name**: LTI ATS (Applicant Tracking System)
- **Document Version**: 1.0
- **Author**: Cristhian Guerrero
- **Date**: 2026-04-05
- **Status**: Draft

LTI is a next-generation Applicant Tracking System purpose-built for small and growing companies (5–100 employees) that manage hiring through spreadsheets, disconnected email threads, and separate job-board logins. LTI consolidates the entire recruitment lifecycle — from writing and distributing a job posting to confirming a final-round interview — into a single, lightweight platform that can be set up in minutes and mastered in hours.

---

## 2. Problem Statement

Small companies (< 50–100 employees) manage recruiting through spreadsheets and email, resulting in:

- **Lost applications** — Candidates fall through the cracks when tracked across multiple inboxes and sheets.
- **Missed follow-ups** — Manual processes cause candidate ghosting, damaging employer brand.
- **Scheduling overhead** — 5–7 email exchanges per interview to coordinate times between candidates and interviewers.
- **Inconsistent candidate communication** — No standardized workflows mean a poor, fragmented candidate experience.
- **Excessive administrative burden** — HR generalists and founders who simultaneously manage operations, finance, and people lose hours per week to recruiting mechanics.

Existing ATS tools (Greenhouse, Lever, Workday) are architected for large organizations, requiring weeks of onboarding, costly implementations, and dedicated system administrators. Mid-market options (Workable, BambooHR) carry significant feature bloat and pricing models that scale uncomfortably for teams with fewer than 50 employees. **There is no ATS designed specifically for single-person HR teams or founder-led hiring.**

---

## 3. Goals & Objectives

| # | Goal | SMART Criteria | Linked KPI |
|---|------|----------------|------------|
| G1 | **Minimize time-to-first-post** — Enable new users to sign up and publish their first live job listing in under 30 minutes | Specific, Measurable, Time-bound | KPI-1 |
| G2 | **Eliminate manual scheduling** — Achieve > 70% self-scheduling rate where candidates book interview slots without recruiter intervention | Specific, Measurable, Achievable | KPI-2 |
| G3 | **Reduce recruiter admin time** — Cut time spent on repetitive administrative tasks (data entry, status emails, cross-board posting) by ≥ 60% | Specific, Measurable, Relevant | KPI-3 |
| G4 | **Improve candidate engagement** — Ensure every candidate receives timely, automated communication at each pipeline stage, targeting < 2% candidate ghosting rate | Specific, Measurable, Achievable | KPI-4 |
| G5 | **Achieve product-market fit** — Reach $50K MRR within 12 months of launch with net revenue retention ≥ 100% | Specific, Measurable, Time-bound | KPI-5, KPI-6 |

---

## 4. Non-Goals / Out-of-Scope

| Item | Reason | Revisit Phase |
|------|--------|---------------|
| Advanced AI screening / candidate ranking | MVP focuses on automating administrative work, not hiring decisions. Adds complexity and bias risk. | Phase 2 — post-PMF ($99/mo add-on planned) |
| Native mobile application | Target users (HR admins, recruiters) primarily work on desktop. Mobile responsive web is sufficient for MVP. | Phase 3 — based on user feedback |
| Offer letter generation & e-signatures | Specialized legal/compliance domain. Users can continue with existing tools (DocuSign, HelloSign). | Phase 2 |
| Advanced analytics & reporting dashboards | Basic pipeline metrics are included; BI-grade analytics is out of scope. | Phase 2 |
| Multi-language / i18n support | Initial launch targets English-speaking markets (US, UK, Canada, Australia). | Phase 3 |
| Payroll / HRIS integration | LTI is an ATS, not an HRIS. Integrations with BambooHR/Gusto deferred. | Phase 3 |
| Glassdoor / other job board integrations | MVP supports Indeed and LinkedIn only. Additional boards based on customer demand. | Phase 2 |
| Video interview built-in platform | Calendar integration generates Google Meet / Teams links natively; no need for a custom video tool. | Not planned |
| Single Sign-On (SSO / SAML) | Enterprise feature; target segment uses email/password or OAuth2 social login. | Phase 3 |

---

## 5. Product Roadmap

> See: [product-roadmap.md](./product-roadmap.md)

---

## 6. Epics

| Epic ID | Epic Name | Outcome | Dependencies | Phase |
|---------|-----------|---------|--------------|-------|
| EPIC-01 | **Company & User Management** | Companies can sign up, configure accounts, and manage team members with role-based access | None | Phase 1 |
| EPIC-02 | **Job Posting & Syndication** | HR Admins create job listings and distribute them to Indeed, LinkedIn, and a branded career page in one click | EPIC-01 | Phase 1 |
| EPIC-03 | **Candidate Pipeline & Kanban Board** | Recruiters and Hiring Managers track all applicants through a shared visual pipeline with drag-and-drop stage management | EPIC-01 | Phase 1 |
| EPIC-04 | **AI Resume Parsing** | Inbound applications are automatically parsed to extract structured candidate data, eliminating manual data entry | EPIC-03 | Phase 1 |
| EPIC-05 | **Automated Email Communication** | Candidates receive timely, template-driven emails at every pipeline stage transition without recruiter intervention | EPIC-01, EPIC-03 | Phase 1 |
| EPIC-06 | **Interview Self-Scheduling & Calendar Sync** | Candidates self-schedule interviews by selecting available slots synced with interviewers' Google Calendar or Outlook | EPIC-03, EPIC-05 | Phase 1 |
| EPIC-07 | **Candidate Database & Search** | Recruiters can search and re-engage past applicants for new openings using keyword search across parsed resume fields | EPIC-04 | Phase 2 |
| EPIC-08 | **Analytics & Reporting (Basic)** | Hiring teams gain visibility into pipeline metrics: time-to-hire, stage conversion rates, source effectiveness | EPIC-02, EPIC-03 | Phase 2 |
| EPIC-09 | **AI Screening Assistant** | AI evaluates candidate-job fit and surfaces recommended shortlists (premium add-on) | EPIC-04, EPIC-07 | Phase 2 |
| EPIC-10 | **Additional Job Board Integrations** | Expand syndication to Glassdoor and other boards based on customer demand | EPIC-02 | Phase 2 |

---

## 7. Target Users & Personas

| Persona | Role | Key Needs | Pain Points |
|---------|------|-----------|-------------|
| **Sarah — Founder/CEO** | Founder at a 15-person startup; handles hiring herself alongside product and operations | Quick job posting, minimal time spent on scheduling, professional candidate experience | Loses 6+ hours/week on recruiting admin; copy-pastes job posts to each board individually; tracks candidates in a spreadsheet that's always out of date |
| **Maria — HR Generalist** | Solo HR person at a 60-person growing company; manages recruiting, onboarding, payroll, and compliance | Centralized applicant tracking, automated communication, collaborative hiring with managers | Drowns in 100+ inbound emails per open role; manually enters candidate data; coordinates interviews via 5–7 email chains per candidate |
| **James — Hiring Manager** | Engineering lead at a 40-person company; involved in interviewing but not day-to-day recruiting operations | Visibility into candidate pipeline status, ability to leave feedback and scores, calendar-synced interviews | Has no idea where candidates are in the process; gets forwarded resumes with no context; scheduling conflicts are constant |
| **Alex — Candidate** | Software engineer applying to multiple positions at small companies | Responsive communication, easy interview scheduling, professional experience | Applies and never hears back; scheduling takes days of back-and-forth emails; has no idea where they stand in the process |

---

## 8. Functional Requirements

### Phase 1: MVP Foundation — Core Recruiting Workflow

- **Goal**: Deliver a complete, end-to-end recruiting workflow covering job creation through interview scheduling.
- **Dependencies**: None
- **Requirements**:

  **Company & User Management (EPIC-01)**
  - FR-1.1: Users can sign up with company name, create an account, and set up their organization profile (name, slug, logo, website).
  - FR-1.2: Users can invite team members by email with role assignment (`admin`, `recruiter`, `hiring_manager`).
  - FR-1.3: System enforces role-based access control — Admins manage settings and templates; Recruiters manage candidates; Hiring Managers view candidates and provide feedback.
  - FR-1.4: Users authenticate via email/password with bcrypt hashing and JWT session tokens.

  **Job Posting & Syndication (EPIC-02)**
  - FR-1.5: HR Admins create job postings with structured fields: title, rich-text description, requirements, salary range (min/max in cents with ISO currency), employment type, location, remote flag.
  - FR-1.6: Job postings support draft and publish states. Drafts can be edited and previewed before publishing.
  - FR-1.7: On publish, the system automatically generates a branded career page listing at `[slug].lti.careers`.
  - FR-1.8: On publish, the system syndicates the posting to selected external boards (Indeed, LinkedIn) via their respective APIs in a single click.
  - FR-1.9: The system tracks syndication status per board (`pending`, `published`, `failed`, `withdrawn`) with error messages and automatic retry (up to 3 attempts with exponential back-off).
  - FR-1.10: HR Admins can close, archive, or unpublish a job across all syndicated boards and the career page in a single action.
  - FR-1.11: A Syndication Status Dashboard displays real-time publish status for each board with retry controls.

  **Candidate Pipeline & Kanban Board (EPIC-03)**
  - FR-1.12: The system provides a visual Kanban board with customizable pipeline stages (default: Applied, Screening, Interview, Offer, Hired, Rejected).
  - FR-1.13: Each candidate application is represented as a card that can be dragged between stages, automatically triggering status-change events.
  - FR-1.14: An Application Inbox displays a chronological feed of all new applications with source attribution (career page, Indeed, LinkedIn).
  - FR-1.15: Team members can attach timestamped notes and a numeric score (1–5) to any application card, visible in real time to all collaborators.
  - FR-1.16: A unified Candidate Profile view aggregates parsed resume data, application history, interview notes, scores, and communication log.
  - FR-1.17: At application intake, if a candidate with the same email already exists, the system links the new application to the existing candidate record and flags the recruiter (duplicate detection).

  **AI Resume Parsing (EPIC-04)**
  - FR-1.18: On application submission, the system automatically extracts structured data (full name, email, phone, LinkedIn URL, work history, education, skills) from uploaded PDF/DOCX resumes using an NLP parsing engine.
  - FR-1.19: Parsed data populates the Candidate profile without manual entry.
  - FR-1.20: Full extracted text is indexed for keyword search.
  - FR-1.21: Resume files are stored in AWS S3; only object paths are stored in the database.

  **Automated Email Communication (EPIC-05)**
  - FR-1.22: The system provides a library of pre-built, fully editable email templates for recurring events: application received, stage changed, interview invitation, interview reminder, offer extended, rejection.
  - FR-1.23: Templates support merge tags (`{{candidate_name}}`, `{{job_title}}`, `{{company_name}}`, `{{scheduling_link}}`).
  - FR-1.24: When an application card moves to a new pipeline stage, the system automatically dispatches the corresponding email template to the candidate via SendGrid.
  - FR-1.25: Email dispatch is triggered asynchronously via the message broker (RabbitMQ) — failures in email delivery do not block the core pipeline.

  **Interview Self-Scheduling & Calendar Sync (EPIC-06)**
  - FR-1.26: Recruiters and Hiring Managers connect their Google Calendar or Outlook calendar via OAuth2.
  - FR-1.27: When an application transitions to the Interview stage, the system generates a tokenized, time-limited (72-hour) self-scheduling link included in the interview invitation email.
  - FR-1.28: Candidates click the scheduling link to view the interviewer's real-time available slots (next 14 days, minimum duration filter) and book a preferred time.
  - FR-1.29: The system performs a real-time availability check to guard against concurrent bookings before confirming.
  - FR-1.30: On booking confirmation, the system creates a calendar event in the interviewer's connected calendar (with video meeting link if applicable), sends confirmation emails to both candidate and recruiter, and queues a 24-hour reminder.
  - FR-1.31: Candidates can reschedule or cancel via one-click links in confirmation/reminder emails. Rescheduling re-opens the portal; cancellations update the calendar and alert the recruiter.
  - FR-1.32: Interviews are tracked through states: Pending, Scheduled, Confirmed, Completed, Cancelled, No-Show.

- **Deliverables**: Fully functional ATS web application with job posting, candidate pipeline, resume parsing, automated communications, and self-service interview scheduling.

### Phase 2: Growth — Intelligence & Expansion

- **Goal**: Add search, analytics, AI screening, and broader job board coverage to increase retention and enable premium tier.
- **Dependencies**: Phase 1 (FR-1.1 through FR-1.32)
- **Requirements**:
  - FR-2.1: Candidate database search — recruiters can search all candidates ever processed using keyword search across parsed resume fields (EPIC-07).
  - FR-2.2: Basic analytics dashboard showing time-to-hire, stage conversion rates, source effectiveness, and active pipeline counts (EPIC-08).
  - FR-2.3: AI Screening Assistant — premium add-on that evaluates candidate-job fit based on parsed resume vs. job requirements and surfaces recommended shortlists (EPIC-09).
  - FR-2.4: Additional job board integrations (Glassdoor and others based on customer demand) (EPIC-10).
  - FR-2.5: Sponsored job board credit resale (Indeed Sponsored) as an add-on revenue stream.

- **Deliverables**: Candidate search, analytics dashboard, AI screening premium add-on, expanded job board syndication.

### Phase 3: Scale — Enterprise Readiness & Platform

- **Goal**: Extend the platform for larger teams and international markets.
- **Dependencies**: Phase 2
- **Requirements**:
  - FR-3.1: Multi-language / i18n support for UI and email templates.
  - FR-3.2: SSO / SAML authentication for enterprise customers.
  - FR-3.3: HRIS integrations (BambooHR, Gusto).
  - FR-3.4: Native mobile application (iOS, Android).
  - FR-3.5: API access for Scale tier customers to build custom integrations.

- **Deliverables**: Internationalization, enterprise auth, HRIS integrations, mobile app, public API.

---

## 9. Non-Functional Requirements

- **Performance**:
  - Page load time < 2 seconds for the Kanban board with up to 200 active applications.
  - API response time p95 < 500ms for core CRUD operations.
  - Resume parsing completes within 10 seconds of upload.
  - Job board syndication requests fire within 5 seconds of publish action.

- **Security**:
  - JWT-based authentication with short-lived access tokens and refresh token rotation.
  - OAuth2 for external calendar integrations (Google, Outlook).
  - All passwords stored as bcrypt hashes.
  - OAuth tokens (calendar access/refresh) encrypted at rest using AES-256.
  - Self-scheduling tokens generated via CSPRNG, time-limited (72 hours), single-use.
  - UUIDs for all primary keys to prevent enumerable ID vulnerabilities.
  - TLS termination at API Gateway (Nginx).
  - Rate limiting at API Gateway layer.
  - OWASP Top 10 compliance across all endpoints.

- **Scalability**:
  - Modular monolith architecture with internal service boundaries (Job, Pipeline, Notification, Scheduling, Resume Parser) designed for future extraction into independent microservices.
  - PostgreSQL as primary database with UUID PKs supporting future horizontal partitioning.
  - Redis for session storage, caching, and rate-limiting counters.
  - RabbitMQ for async event-driven flows (email dispatch, scheduling triggers) — decouples core pipeline from integration failures.
  - Initial target: support 500 concurrent companies, 5,000 active job postings.

- **Availability**:
  - 99.9% uptime SLA for the web application.
  - Graceful degradation: job board API failures do not block career page publishing or core pipeline operations.
  - Async retry with exponential back-off for external API failures.

- **Accessibility**:
  - Career page and self-scheduling portal meet WCAG 2.1 Level AA compliance.
  - Candidate-facing interfaces are keyboard navigable and screen-reader compatible.

---

## 10. KPIs & Success Metrics

| KPI | Description | Baseline | Target | Measurement Method | Review Frequency |
|-----|-------------|----------|--------|--------------------|------------------|
| KPI-1: Time-to-first-post | Time from signup to first live job listing | N/A (new product) | < 30 minutes | Application analytics (signup → first `published` event) | Monthly |
| KPI-2: Self-scheduling rate | % of interview invitations where candidates book without recruiter intervention | N/A | > 70% | `SCHEDULED_EVENT` created via self-scheduling token ÷ interview invitation emails sent | Monthly |
| KPI-3: Recruiter admin time reduction | Reduction in time spent on repetitive tasks vs. pre-LTI workflow | Baseline survey at onboarding | ≥ 60% reduction | User surveys + task completion time analytics | Quarterly |
| KPI-4: Candidate ghosting rate | % of candidates who receive no communication within 48h of applying | Industry avg ~40% | < 2% | Applications with no email dispatch within 48h ÷ total applications | Monthly |
| KPI-5: Monthly Recurring Revenue | Total MRR from subscription tiers | $0 | $50K within 12 months | Stripe billing data | Monthly |
| KPI-6: Net Revenue Retention | Revenue retained from existing customers including expansions | N/A | ≥ 100% | Cohort revenue analysis (Stripe) | Quarterly |
| KPI-7: Weekly Active Users | Unique users who perform at least one core action per week per company | N/A | ≥ 3 per company | Application event tracking | Weekly |
| KPI-8: Churn rate | Monthly company-level churn | N/A | < 5% per month | Cancelled subscriptions ÷ active subscriptions | Monthly |

---

## 11. User Story Map

> See: [user-story-map.md](./user-story-map.md)

---

## 12. User Stories

> See: [user-stories.md](./user-stories.md)

---

## 13. Product Backlog

> See: [product-backlog.md](./product-backlog.md)

---

## 14. Technical Considerations

- **Architecture**: Modular monolith with clearly defined internal service boundaries (Job Service, Pipeline Service, Notification Service, Scheduling Service, Resume Parser). Designed for future extraction into microservices as load and team size grow.

- **Integrations**:
  | Integration | Purpose | Protocol |
  |-------------|---------|----------|
  | Indeed API | Job posting syndication | REST API |
  | LinkedIn API | Job posting syndication | REST API |
  | Google Calendar API | Calendar sync, availability, event creation | OAuth2 + REST |
  | Microsoft Graph API (Outlook) | Calendar sync, availability, event creation | OAuth2 + REST |
  | SendGrid | Transactional email delivery | REST API |

- **Data Model**: 9 core entities — Company, User, Job Posting, Job Board Syndication, Candidate, Application, Pipeline Stage, Interview, Email Template, Scheduled Event. PostgreSQL with UUID primary keys, AES-256 encrypted OAuth tokens, timestamps in UTC. Full ER diagram in the [System Design Document](https://github.com/cristianguerro/AI4Devs-design-1-202602-Seniors/blob/feature/lti-cfgp/LTI-CFGP/LTI-CFGP.md#5-data-model).

- **Tech Stack**:
  | Layer | Technology |
  |-------|------------|
  | Frontend | React + TypeScript (SPA) |
  | Backend | Node.js + TypeScript + Express |
  | Database | PostgreSQL |
  | Cache & Sessions | Redis |
  | Message Broker | RabbitMQ |
  | Object Storage | AWS S3 (resumes) |
  | API Gateway | Nginx (upgradeable to Kong) |
  | Email Provider | SendGrid |
  | Hosting | AWS (EC2, RDS, ElastiCache, S3) |

---

## 15. UX/UI Considerations

- **Design Principle**: Zero-learning-curve interface designed for single-person HR teams, not enterprise recruiting departments.
- **Core Interactions**:
  - Drag-and-drop Kanban board as the primary workspace (inspired by Trello simplicity).
  - One-click publish flow for job postings.
  - Candidate self-scheduling portal with clean, mobile-friendly slot selection.
- **Branded Career Page**: Auto-generated at `[slug].lti.careers`, embeddable via iframe on company websites.
- **Email Templates**: WYSIWYG editor with merge tag insertion for non-technical users.
- **Setup Flow**: Guided onboarding targeting < 30 minutes from signup to first published job (company profile → invite team → connect calendar → create job → publish).

---

## 16. Risks & Mitigations

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|
| Job board API changes or deprecation | High — breaks core syndication feature | Medium | Encapsulate each board integration behind an adapter interface; monitor API changelogs; maintain fallback manual posting instructions |
| AI resume parsing accuracy below threshold | Medium — undermines value proposition of eliminating data entry | Medium | Use established NLP parsing providers; implement user-editable parsed fields so recruiters can correct errors; track parsing accuracy metrics |
| Low adoption / product-market fit miss | Critical — threatens business viability | Medium | Validate with early beta users (10–20 companies) before full launch; iterate rapidly based on feedback; measure time-to-first-post and WAU closely |
| Calendar sync OAuth token expiry or revocation | Medium — breaks self-scheduling flow | Medium | Implement proactive token refresh; alert users when calendar connection requires re-authorization; graceful fallback messaging |
| SendGrid deliverability issues (spam filtering) | Medium — candidates don't receive critical emails | Low | Use dedicated IP with proper SPF/DKIM/DMARC setup; monitor bounce rates; provide fallback notification via in-app alerts |
| Data breach / unauthorized access to candidate PII | Critical — regulatory and reputational damage | Low | AES-256 encryption for tokens; bcrypt for passwords; UUID PKs; TLS everywhere; regular security audits; SOC 2 preparation |
| Concurrent booking race condition in self-scheduling | Low — double-booked interviews | Medium | Real-time availability check with optimistic locking before confirming slot; atomic database transaction for booking |

---

## 17. Dependencies & Constraints

| Dependency | Type | Owner | Status |
|------------|------|-------|--------|
| Indeed Job Posting API access | External API | Indeed Developer Program | Requires API key approval |
| LinkedIn Job Posting API access | External API | LinkedIn Developer Program | Requires partnership application |
| Google Calendar API (OAuth2 consent screen) | External API | Google Cloud Console | Requires OAuth consent screen verification |
| Microsoft Graph API (Outlook Calendar) | External API | Microsoft Azure AD | Requires app registration |
| SendGrid account with dedicated IP | External Service | SendGrid | Requires account setup + IP warm-up |
| AWS infrastructure (EC2, RDS, S3, ElastiCache) | Infrastructure | Engineering | To be provisioned |
| NLP resume parsing service/library | External Service / Library | Engineering | Technology selection pending |
| Domain `lti.careers` for branded career pages | Infrastructure | Operations | Requires domain registration + DNS setup |

---

## 18. Timeline & Milestones

| Phase | Milestone | Target Date | Status |
|-------|-----------|-------------|--------|
| Phase 1 | MVP — Company & User Management complete | TBD | Not Started |
| Phase 1 | MVP — Job Posting & Syndication complete | TBD | Not Started |
| Phase 1 | MVP — Candidate Pipeline & Kanban Board complete | TBD | Not Started |
| Phase 1 | MVP — AI Resume Parsing integrated | TBD | Not Started |
| Phase 1 | MVP — Automated Email Communication live | TBD | Not Started |
| Phase 1 | MVP — Interview Self-Scheduling & Calendar Sync live | TBD | Not Started |
| Phase 1 | **MVP Launch — Closed Beta (10–20 companies)** | TBD | Not Started |
| Phase 1 | **MVP Launch — Public Launch** | TBD | Not Started |
| Phase 2 | Candidate Database Search | TBD | Not Started |
| Phase 2 | Analytics Dashboard | TBD | Not Started |
| Phase 2 | AI Screening Assistant (premium add-on) | TBD | Not Started |
| Phase 3 | i18n, SSO, HRIS, Mobile App, Public API | TBD | Not Started |

---

## 19. Stakeholders & Sign-off

| Name | Role | Status | Date |
|------|------|--------|------|
| Cristhian Guerrero | Product Owner | Pending | — |
| TBD | Engineering Lead | Pending | — |
| TBD | UX/Design Lead | Pending | — |
| TBD | QA Lead | Pending | — |

---

## Appendix

### Glossary

| Term | Definition |
|------|------------|
| ATS | Applicant Tracking System — software for managing the recruitment and hiring process |
| Kanban Board | A visual workflow management tool with columns representing process stages and cards representing work items |
| Syndication | The automated distribution of a job posting to multiple external job boards from a single source |
| Self-Scheduling | A workflow where candidates select their own interview time from available slots without recruiter coordination |
| Merge Tags | Placeholder variables in email templates (e.g., `{{candidate_name}}`) that are replaced with actual data at send time |
| Pipeline Stage | A named step in the hiring workflow (e.g., Applied, Screening, Interview, Offer, Hired, Rejected) |
| CSPRNG | Cryptographically Secure Pseudo-Random Number Generator — used for generating secure tokens |
| Modular Monolith | An architecture where the application runs as a single deployment but is internally organized into independent, well-bounded modules |

### References

- [LTI ATS System Design Document](https://github.com/cristianguerro/AI4Devs-design-1-202602-Seniors/blob/feature/lti-cfgp/LTI-CFGP/LTI-CFGP.md) — Source design document with Lean Canvas, use cases, data model, architecture, and C4 diagrams
- [MVP Defined Objectives](https://github.com/cristianguerro/AI4Devs-design-1-202602-Seniors/blob/feature/lti-cfgp/LTI-CFGP/defined-objectives) — Research-backed MVP goal definition

### Change Log

| Date | Author | Version | Change Description |
|------|--------|---------|-------------------|
| 2026-04-05 | Cristhian Guerrero | 1.0 | Initial PRD created from System Design Document |
