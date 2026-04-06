# User Stories: LTI ATS

- **Product**: LTI ATS (Applicant Tracking System)
- **Source PRD**: [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md)
- **Story Map**: [user-story-map.md](./user-story-map.md)
- **Roadmap**: [product-roadmap.md](./product-roadmap.md)

---

## Epic: EPIC-01 — Company & User Management

---

### User Story: US-001

#### Card
**As a** founder or HR generalist  
**I want** to sign up and create a company account  
**So that** I can start using LTI to manage my company's hiring process

#### Conversation
- **Context**: This is the entry point for all new users. The signup flow must be fast (< 5 min) to support the < 30 min time-to-first-post goal.
- **Assumptions**: Email/password authentication is sufficient for MVP; social login deferred.
- **Dependencies**: None — this is the foundation story.
- **Notes**: Company slug is auto-generated from the company name and used for the branded career page URL (`[slug].lti.careers`).

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Successful signup
- **Given** a user is on the LTI signup page
- **When** they enter their email, password, company name, and click "Create Account"
- **Then** a Company record is created with a unique slug, a User record is created with the `admin` role, and the user is redirected to the onboarding dashboard

**Scenario 2**: Duplicate email rejection
- **Given** a user with email "sarah@acme.com" already exists
- **When** a new user attempts to sign up with "sarah@acme.com"
- **Then** the system shows an error "An account with this email already exists" and does not create a duplicate record

**Scenario 3**: Weak password rejection
- **Given** a user is on the signup page
- **When** they enter a password shorter than 8 characters or missing uppercase/number
- **Then** the system shows a validation error explaining the password requirements

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | No dependencies on other stories |
| **N**egotiable | ✅ | Password policy, onboarding flow details are negotiable |
| **V**aluable | ✅ | Unlocks all product functionality |
| **E**stimable | ✅ | Standard auth signup flow |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Clear pass/fail criteria above |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Company & User Management
- **Epic ID**: EPIC-01
- **PRD Requirement**: FR-1.1, FR-1.4
- **Labels/Tags**: `auth`, `onboarding`, `mvp`

---

### User Story: US-002

#### Card
**As an** HR Admin  
**I want** to invite team members by email and assign them roles  
**So that** recruiters and hiring managers can collaborate within the same company account

#### Conversation
- **Context**: Small teams typically have 1–3 users: the admin, a recruiter, and a hiring manager. Invitations should be simple email-based flows.
- **Assumptions**: Invitation link expires after 7 days. Roles: `admin`, `recruiter`, `hiring_manager`.
- **Dependencies**: US-001 (company account must exist)
- **Notes**: Role-based access control determines what each user can see and do across the platform.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Successful invitation
- **Given** an HR Admin is logged in and navigates to Team Settings
- **When** they enter an email address, select a role (`recruiter` or `hiring_manager`), and click "Send Invite"
- **Then** the system sends an invitation email with a unique signup link, and the invitee appears in the team list with status "Pending"

**Scenario 2**: Invitee completes registration
- **Given** a user received an invitation email
- **When** they click the invitation link, enter their name and password, and submit
- **Then** a User record is created with the assigned role under the inviting company, and the team list status updates to "Active"

**Scenario 3**: Expired invitation link
- **Given** an invitation link is older than 7 days
- **When** the invitee clicks the link
- **Then** the system shows an "Invitation expired" message and suggests contacting the admin for a new invite

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Only depends on US-001 (account exists) |
| **N**egotiable | ✅ | Expiration period, role list negotiable |
| **V**aluable | ✅ | Enables team collaboration |
| **E**stimable | ✅ | Standard invitation flow |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Clear BDD scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Company & User Management
- **Epic ID**: EPIC-01
- **PRD Requirement**: FR-1.2, FR-1.3
- **Labels/Tags**: `auth`, `team`, `rbac`, `mvp`

---

### User Story: US-003

#### Card
**As an** HR Admin  
**I want** to configure my company profile with name, logo, and website  
**So that** our branded career page reflects our company identity

#### Conversation
- **Context**: The company profile powers the branded career page at `[slug].lti.careers`. Logo is uploaded and stored on CDN.
- **Assumptions**: Logo upload supports PNG/JPG up to 2MB. Slug is editable but must remain unique.
- **Dependencies**: US-001
- **Notes**: Career page is public-facing — branding quality directly impacts candidate perception.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Update company profile
- **Given** an HR Admin navigates to Company Settings
- **When** they update the company name, upload a logo, enter a website URL, and click "Save"
- **Then** the Company record is updated and the branded career page reflects the new branding within 30 seconds

**Scenario 2**: Invalid logo format
- **Given** an HR Admin uploads a file that is not PNG or JPG, or exceeds 2MB
- **When** they click "Save"
- **Then** the system shows a validation error specifying the allowed formats and size limit

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Only needs account to exist |
| **N**egotiable | ✅ | Supported formats, size limits negotiable |
| **V**aluable | ✅ | Professional employer branding |
| **E**stimable | ✅ | Form + file upload |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Clear criteria |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Company & User Management
- **Epic ID**: EPIC-01
- **PRD Requirement**: FR-1.1
- **Labels/Tags**: `branding`, `settings`, `mvp`

---

### User Story: US-004

#### Card
**As a** Recruiter or Hiring Manager  
**I want** to connect my Google Calendar or Outlook calendar via OAuth2  
**So that** the system can read my availability and write interview events to my calendar

#### Conversation
- **Context**: Calendar connection is a prerequisite for the self-scheduling flow (EPIC-06). Must support both Google Calendar API and Microsoft Graph API (Outlook).
- **Assumptions**: OAuth2 consent flow; tokens stored AES-256 encrypted. User can disconnect and reconnect at any time.
- **Dependencies**: US-001
- **Notes**: Token refresh must be handled proactively to avoid broken scheduling links.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Connect Google Calendar
- **Given** a user navigates to Calendar Settings and selects "Connect Google Calendar"
- **When** they complete the Google OAuth2 consent flow
- **Then** the system stores encrypted access and refresh tokens, sets `calendar_provider` to `google`, and shows a "Connected" status

**Scenario 2**: Connect Outlook Calendar
- **Given** a user navigates to Calendar Settings and selects "Connect Outlook"
- **When** they complete the Microsoft OAuth2 consent flow
- **Then** the system stores encrypted tokens, sets `calendar_provider` to `outlook`, and shows a "Connected" status

**Scenario 3**: Disconnect calendar
- **Given** a user has a connected calendar
- **When** they click "Disconnect"
- **Then** the system revokes the OAuth tokens, sets `calendar_provider` to `none`, and shows "Not Connected"

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Can be built independently; used by EPIC-06 |
| **N**egotiable | ✅ | Which providers, token refresh strategy |
| **V**aluable | ✅ | Prerequisite for self-scheduling |
| **E**stimable | ✅ | OAuth2 integration pattern |
| **S**mall | ✅ | Single sprint (2 providers) |
| **T**estable | ✅ | Clear connect/disconnect flows |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Company & User Management
- **Epic ID**: EPIC-01
- **PRD Requirement**: FR-1.26
- **Labels/Tags**: `calendar`, `oauth2`, `integration`, `mvp`

---

### User Story: US-005

#### Card
**As an** HR Admin  
**I want** to customize the pipeline stages for my company  
**So that** the Kanban board matches our specific hiring workflow

#### Conversation
- **Context**: Default stages are: Applied, Screening, Interview, Offer, Hired, Rejected. Companies can rename, reorder, add, or remove stages.
- **Assumptions**: At least one terminal-hired and one terminal-rejected stage must exist. Stages have a display color.
- **Dependencies**: US-001
- **Notes**: Stage configuration affects all job postings within the company.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Add a custom stage
- **Given** an HR Admin navigates to Pipeline Settings
- **When** they click "Add Stage", enter a name "Technical Test", select a color, and click "Save"
- **Then** the new stage appears in the pipeline at the selected position and is available on all Kanban boards

**Scenario 2**: Reorder stages
- **Given** an HR Admin is viewing Pipeline Settings with 6 stages
- **When** they drag the "Screening" stage to position 3
- **Then** the stage order updates and the Kanban board reflects the new column order

**Scenario 3**: Prevent removal of terminal stages
- **Given** an HR Admin attempts to delete the only stage marked as `is_terminal_hired`
- **When** they click "Delete"
- **Then** the system shows an error "You must have at least one hired-terminal stage" and prevents deletion

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Only needs company account |
| **N**egotiable | ✅ | Default stages, color options |
| **V**aluable | ✅ | Adapts product to user's workflow |
| **E**stimable | ✅ | CRUD + ordering logic |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Clear BDD scenarios |

#### Metadata
- **Priority**: Should Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Company & User Management
- **Epic ID**: EPIC-01
- **PRD Requirement**: FR-1.12
- **Labels/Tags**: `pipeline`, `settings`, `kanban`, `mvp`

---

## Epic: EPIC-02 — Job Posting & Syndication

---

### User Story: US-006

#### Card
**As an** HR Admin  
**I want** to create a job posting with structured fields  
**So that** I can define a complete, publication-ready job listing

#### Conversation
- **Context**: The job posting form is the starting point for all recruiting activity. Fields include title, rich-text description, requirements, salary range, employment type, location, and remote flag.
- **Assumptions**: Rich-text editor supports basic formatting (bold, lists, headings). Salary stored in cents with ISO currency code.
- **Dependencies**: US-001 (company account must exist)
- **Notes**: Postings start in `draft` status and can be edited before publishing.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Create a draft job posting
- **Given** an HR Admin navigates to Job Postings and clicks "Create New Job Posting"
- **When** they fill in title, description, requirements, salary range ($80K–$120K USD), employment type (full_time), location, and remote flag, then click "Save as Draft"
- **Then** a JOB_POSTING record is created with status `draft`, and it appears in the job postings list as "Draft"

**Scenario 2**: Validation on required fields
- **Given** an HR Admin is on the job posting form
- **When** they leave the title field empty and click "Save"
- **Then** the system highlights the title field with a validation error "Title is required"

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Only needs company account |
| **N**egotiable | ✅ | Required vs optional fields negotiable |
| **V**aluable | ✅ | Core entry point for recruiting |
| **E**stimable | ✅ | Standard form with rich-text editor |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Clear valid/invalid scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Job Posting & Syndication
- **Epic ID**: EPIC-02
- **PRD Requirement**: FR-1.5, FR-1.6
- **Labels/Tags**: `job-posting`, `mvp`

---

### User Story: US-007

#### Card
**As an** HR Admin  
**I want** to preview how my job posting will appear on the branded career page  
**So that** I can verify the listing looks professional before publishing

#### Conversation
- **Context**: Career page is public-facing (`[slug].lti.careers`). Preview should render exactly as the live page will display.
- **Assumptions**: Preview is available for both draft and published postings.
- **Dependencies**: US-006 (posting must be created), US-003 (company branding configured)
- **Notes**: Preview is read-only; editing returns to the form.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Preview a draft posting
- **Given** an HR Admin has created a draft job posting
- **When** they click "Preview Career Page"
- **Then** the system renders the posting as it will appear on the branded career page, including company logo, job title, description, and an "Apply" button

**Scenario 2**: Preview reflects unsaved changes
- **Given** an HR Admin modifies the description in the job posting form
- **When** they click "Preview" without saving first
- **Then** the preview shows the current (unsaved) content so the admin can verify before saving

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Only needs a created posting |
| **N**egotiable | ✅ | Live preview vs modal, unsaved content handling |
| **V**aluable | ✅ | Prevents publishing errors |
| **E**stimable | ✅ | Rendering logic + preview route |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Visual verification + content match |

#### Metadata
- **Priority**: Should Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Job Posting & Syndication
- **Epic ID**: EPIC-02
- **PRD Requirement**: FR-1.7
- **Labels/Tags**: `career-page`, `preview`, `mvp`

---

### User Story: US-008

#### Card
**As an** HR Admin  
**I want** to publish a job posting and syndicate it to Indeed and LinkedIn in one click  
**So that** my job is distributed across multiple platforms without logging into each one separately

#### Conversation
- **Context**: This is the signature "one-click" feature. On publish, the system simultaneously publishes to the career page and sends syndication requests to selected boards via their APIs.
- **Assumptions**: API credentials for Indeed and LinkedIn are pre-configured in company settings. Syndication is asynchronous — career page publishes immediately while board requests fire in the background.
- **Dependencies**: US-006 (posting exists), FR-1.8/FR-1.9 (syndication with retry logic)
- **Notes**: Failed syndications should not block career page publishing.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Successful one-click publish and syndication
- **Given** an HR Admin has a draft job posting and selects Indeed and LinkedIn as target boards
- **When** they click "Publish"
- **Then** the posting status changes to `published`, the career page URL is generated, syndication requests are sent to both boards, and the admin sees a success screen with the career page link

**Scenario 2**: Partial syndication failure with retry
- **Given** an HR Admin publishes a posting to Indeed and LinkedIn
- **When** LinkedIn's API returns a 500 error
- **Then** the career page and Indeed syndication succeed, LinkedIn syndication is marked as `failed`, the system retries up to 3 times with exponential back-off, and the admin sees a partial success notification

**Scenario 3**: Form validation before publish
- **Given** an HR Admin attempts to publish a posting with no target boards selected
- **When** they click "Publish"
- **Then** the system shows a validation error "Select at least one job board"

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Core publishing flow |
| **N**egotiable | ✅ | Retry count, back-off strategy |
| **V**aluable | ✅ | Primary value proposition — eliminates multi-board hassle |
| **E**stimable | ✅ | API integration with async retry |
| **S**mall | ✅ | Single sprint (with API adapters) |
| **T**estable | ✅ | Success, partial failure, validation scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Job Posting & Syndication
- **Epic ID**: EPIC-02
- **PRD Requirement**: FR-1.7, FR-1.8, FR-1.9
- **Labels/Tags**: `syndication`, `job-boards`, `one-click`, `mvp`

---

### User Story: US-009

#### Card
**As an** HR Admin  
**I want** to view the syndication status for each job board  
**So that** I can see which boards have my posting live and troubleshoot failures

#### Conversation
- **Context**: After publishing, the Syndication Status Dashboard shows per-board status (Pending, Published, Failed) with error messages and manual retry controls.
- **Assumptions**: Dashboard updates in near real-time as async syndication results arrive.
- **Dependencies**: US-008
- **Notes**: Failed syndications show the error message from the board API and a "Retry" button.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: View syndication status
- **Given** an HR Admin has published a job posting to Indeed and LinkedIn
- **When** they navigate to the job posting's syndication dashboard
- **Then** they see a row per board showing status (`published`, `pending`, or `failed`), the external posting ID (if published), and the timestamp

**Scenario 2**: Manual retry on failure
- **Given** LinkedIn syndication shows status `failed` with error "Rate limit exceeded"
- **When** the HR Admin clicks "Retry"
- **Then** the system re-sends the syndication request to LinkedIn and updates the status to `pending`

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Dashboard view independent of syndication logic |
| **N**egotiable | ✅ | UI layout, refresh frequency |
| **V**aluable | ✅ | Transparency into job distribution |
| **E**stimable | ✅ | Read from existing syndication records |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Status display + retry action |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Job Posting & Syndication
- **Epic ID**: EPIC-02
- **PRD Requirement**: FR-1.11
- **Labels/Tags**: `syndication`, `dashboard`, `mvp`

---

### User Story: US-010

#### Card
**As an** HR Admin  
**I want** to close or archive a job posting across all boards and the career page in one action  
**So that** no stale listings remain visible when a position is filled

#### Conversation
- **Context**: Closing a job should withdraw it from all syndicated boards and remove it from the career page simultaneously.
- **Assumptions**: Closing is reversible (can reopen/republish). Archiving is a soft-delete for historical records.
- **Dependencies**: US-008 (posting must be published and syndicated)
- **Notes**: Board withdrawal uses the stored external ID per syndication record.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Close a job posting
- **Given** an HR Admin has a published job posting syndicated to Indeed and LinkedIn
- **When** they click "Close Job"
- **Then** the posting status changes to `closed`, the career page listing is removed, withdrawal requests are sent to Indeed and LinkedIn, and syndication statuses update to `withdrawn`

**Scenario 2**: Archive a closed posting
- **Given** an HR Admin has a closed job posting
- **When** they click "Archive"
- **Then** the posting status changes to `archived` and it moves to the archived postings list, no longer visible in the active job list

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Lifecycle action on existing posting |
| **N**egotiable | ✅ | Archive vs permanent delete behavior |
| **V**aluable | ✅ | Prevents stale listings, professional employer brand |
| **E**stimable | ✅ | Status update + API withdrawal calls |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Clear state transitions |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Job Posting & Syndication
- **Epic ID**: EPIC-02
- **PRD Requirement**: FR-1.10
- **Labels/Tags**: `job-lifecycle`, `mvp`

---

## Epic: EPIC-03 — Candidate Pipeline & Kanban Board

---

### User Story: US-012

#### Card
**As a** Recruiter  
**I want** to receive applications from the career page and job boards into a single inbox  
**So that** I have one centralized place to see all new applicants regardless of source

#### Conversation
- **Context**: Applications arrive from career page (direct submission), Indeed, and LinkedIn. Each application includes the resume file, source attribution, and is linked to the job posting.
- **Assumptions**: Career page submissions are real-time; job board applications are polled or webhook-based depending on board API.
- **Dependencies**: US-008 (jobs must be published), EPIC-04 (parsing triggers on arrival)
- **Notes**: Source attribution is critical for analytics in Phase 2.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Receive career page application
- **Given** a published job posting on the career page
- **When** a candidate submits their resume and optional cover letter via the application form
- **Then** a Candidate record is created (or linked if duplicate), an Application record is created in the `Applied` stage, the source is set to `career_page`, and the Recruiter receives an in-app notification

**Scenario 2**: Receive Indeed application
- **Given** a job posting syndicated to Indeed
- **When** Indeed routes an applicant to LTI via API
- **Then** an Application record is created with source `indeed`, linked to the correct job posting, and appears in the Application Inbox

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Application intake is independent from pipeline management |
| **N**egotiable | ✅ | Polling vs webhook, notification preferences |
| **V**aluable | ✅ | Centralizes applicants — core value prop |
| **E**stimable | ✅ | API endpoints + record creation |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Source attribution + record creation |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.14
- **Labels/Tags**: `applications`, `inbox`, `mvp`

---

### User Story: US-014

#### Card
**As a** Recruiter  
**I want** to view a unified candidate profile with parsed data, application history, notes, and communication log  
**So that** I have full context on a candidate without hunting through email threads

#### Conversation
- **Context**: The candidate profile aggregates AI-parsed resume data (US-013), all applications across postings, interview notes/scores, and email history.
- **Assumptions**: Profile is accessible from the Kanban card, inbox, and candidate search.
- **Dependencies**: US-012 (application exists), US-013 (parsed data populates profile)
- **Notes**: Hiring Managers also have read access to candidate profiles.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: View candidate profile from Kanban card
- **Given** a Recruiter clicks on an application card on the Kanban board
- **When** the candidate profile opens
- **Then** it displays the candidate's parsed name, email, phone, LinkedIn URL, work history, skills, all application records, notes/scores, and a timeline of email communications sent

**Scenario 2**: View multi-application candidate
- **Given** a candidate "Alex Lee" has applied to two different job postings
- **When** the Recruiter views Alex's candidate profile
- **Then** both application records are visible under "Applications" with their respective job titles, stages, and dates

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Read-only aggregation view |
| **N**egotiable | ✅ | Layout, which fields to show |
| **V**aluable | ✅ | Eliminates context-switching; full candidate picture |
| **E**stimable | ✅ | API aggregation + UI rendering |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Data completeness verification |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.16
- **Labels/Tags**: `candidate-profile`, `mvp`

---

### User Story: US-015

#### Card
**As a** Recruiter  
**I want** the system to detect when a candidate with the same email applies again  
**So that** duplicate records are avoided and I can see the full history of returning candidates

#### Conversation
- **Context**: Candidates may apply to multiple postings over time. Deduplication is based on email address.
- **Assumptions**: If a duplicate is found, the new Application is linked to the existing Candidate record; the Recruiter is flagged.
- **Dependencies**: US-012 (application intake)
- **Notes**: No automatic merging of different email addresses — only exact email match.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Duplicate detected and linked
- **Given** a candidate with email "alex@example.com" already exists in the system
- **When** a new application arrives with the same email
- **Then** the system links the new Application to the existing Candidate record and shows a "Returning Candidate" badge on the application card

**Scenario 2**: New unique candidate
- **Given** no candidate with email "new@example.com" exists
- **When** an application arrives with that email
- **Then** the system creates a new Candidate record and a new Application record

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Deduplication logic at intake |
| **N**egotiable | ✅ | Matching criteria (email only vs email+name) |
| **V**aluable | ✅ | Prevents data fragmentation |
| **E**stimable | ✅ | Email lookup + conditional create |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Duplicate vs new scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.17
- **Labels/Tags**: `deduplication`, `candidate`, `mvp`

---

### User Story: US-016

#### Card
**As a** Recruiter or Hiring Manager  
**I want** to view all candidates for a job posting on a visual Kanban board  
**So that** I can see the pipeline status at a glance

#### Conversation
- **Context**: The Kanban board is the primary workspace. Each column represents a pipeline stage; each card is an application.
- **Assumptions**: Board loads with up to 200 active applications within 2 seconds (NFR). Cards show candidate name, source, and applied date.
- **Dependencies**: US-005 (pipeline stages configured), US-012 (applications exist)
- **Notes**: Hiring Managers see a read-and-feedback view; Recruiters have full drag-and-drop control.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: View Kanban board
- **Given** a Recruiter navigates to a job posting with 15 applications across 4 pipeline stages
- **When** the Kanban board loads
- **Then** the board displays one column per pipeline stage (in configured order), with application cards in each column showing candidate name, source badge, and applied date

**Scenario 2**: Empty pipeline
- **Given** a newly published job posting with no applications
- **When** the Recruiter views the Kanban board
- **Then** all stage columns are empty with a message "No applications yet"

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Read-only view of existing data |
| **N**egotiable | ✅ | Card content, column styling |
| **V**aluable | ✅ | Core UX — visual hiring management |
| **E**stimable | ✅ | Frontend Kanban component + API |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Board rendering + data accuracy |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.12
- **Labels/Tags**: `kanban`, `pipeline`, `mvp`

---

### User Story: US-017

#### Card
**As a** Recruiter  
**I want** to drag a candidate card to a different pipeline stage  
**So that** I can advance or reject candidates and trigger automated workflows

#### Conversation
- **Context**: Drag-and-drop is the primary interaction. Moving a card triggers a `STAGE_CHANGED` event which downstream systems (email, scheduling) consume.
- **Assumptions**: Stage transitions are logged for audit. Any stage-to-stage move is allowed (no enforced linear flow).
- **Dependencies**: US-016, US-019 (auto-email triggers on move)
- **Notes**: Moving to a terminal-rejected stage triggers rejection email; moving to Interview triggers scheduling flow.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Advance candidate to next stage
- **Given** a Recruiter views the Kanban board with a candidate card in "Applied"
- **When** they drag the card to the "Screening" column
- **Then** the Application's `pipeline_stage_id` updates to the Screening stage, a `STAGE_CHANGED` event is published, and the card appears in the new column

**Scenario 2**: Reject candidate
- **Given** a Recruiter drags a candidate card to the "Rejected" column (terminal stage)
- **When** the card is dropped
- **Then** the Application status updates to `rejected`, a rejection email is triggered (US-019), and the card appears in the Rejected column

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Drag-and-drop interaction |
| **N**egotiable | ✅ | Which transitions trigger which events |
| **V**aluable | ✅ | Core workflow — pipeline progression |
| **E**stimable | ✅ | DnD frontend + API update + event publish |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Stage update + event emission |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.13
- **Labels/Tags**: `kanban`, `drag-drop`, `pipeline`, `mvp`

---

### User Story: US-018

#### Card
**As a** Recruiter or Hiring Manager  
**I want** to add timestamped notes and a numeric score (1–5) to an application card  
**So that** the hiring team can share evaluations and make aligned decisions

#### Conversation
- **Context**: Notes and scores enable collaborative evaluation. Both Recruiters and Hiring Managers can contribute; all notes are visible in real time.
- **Assumptions**: Notes are append-only (no editing after creation for audit trail). Scores are per-user.
- **Dependencies**: US-016 (Kanban board exists)
- **Notes**: Notes appear on the candidate profile timeline as well.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Add a note and score
- **Given** a Recruiter opens an application card
- **When** they type a note "Strong Python background, good culture fit", select a score of 4, and click "Add Note"
- **Then** the note is saved with the recruiter's name, timestamp, and score, and appears on the card's notes section and the candidate profile

**Scenario 2**: Multiple team members add notes
- **Given** a Recruiter has added a note to a candidate card
- **When** a Hiring Manager views the same card and adds their own note and score
- **Then** both notes are visible with their respective authors and timestamps, ordered chronologically

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Note-taking is independent from pipeline movement |
| **N**egotiable | ✅ | Score range, edit policy |
| **V**aluable | ✅ | Enables team collaboration on hiring |
| **E**stimable | ✅ | Text input + score widget + persistence |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Note persistence + multi-user visibility |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.15
- **Labels/Tags**: `collaboration`, `notes`, `scoring`, `mvp`

---

## Epic: EPIC-04 — AI Resume Parsing

---

### User Story: US-013

#### Card
**As a** Recruiter  
**I want** the system to automatically parse uploaded resumes and extract structured candidate data  
**So that** I don't have to manually enter applicant information

#### Conversation
- **Context**: When a resume (PDF/DOCX) is uploaded with an application, the NLP parsing engine extracts: full name, email, phone, LinkedIn URL, work history, education, and skills. Parsed data populates the Candidate profile.
- **Assumptions**: Parsing completes within 10 seconds (NFR). Resumes are stored in S3; only metadata is in PostgreSQL. Parsed fields are editable by the Recruiter if corrections are needed.
- **Dependencies**: US-012 (application intake triggers parsing)
- **Notes**: Full extracted text is also indexed for keyword search (US-030, Phase 2).

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Successful resume parsing
- **Given** a candidate submits an application with a PDF resume
- **When** the application is created
- **Then** the system uploads the resume to S3, triggers the NLP parser, extracts name/email/phone/LinkedIn/work history/education/skills, and populates the Candidate profile fields within 10 seconds

**Scenario 2**: Unsupported file format
- **Given** a candidate uploads a resume in `.txt` format
- **When** the application is submitted
- **Then** the system accepts the application but flags the resume as "parsing unavailable" and notifies the Recruiter to enter data manually

**Scenario 3**: Partial parse result
- **Given** a resume with unusual formatting
- **When** the parser extracts only name and email but fails to parse work history
- **Then** the system populates the available fields, marks unparsed sections as "Not extracted", and the Recruiter can manually complete the profile

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Parsing module is self-contained |
| **N**egotiable | ✅ | Supported formats, parsing provider |
| **V**aluable | ✅ | Eliminates manual data entry — key differentiator |
| **E**stimable | ✅ | NLP integration + S3 upload |
| **S**mall | ✅ | Single sprint (integration, not building NLP) |
| **T**estable | ✅ | Full, partial, and failed parse scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: AI Resume Parsing
- **Epic ID**: EPIC-04
- **PRD Requirement**: FR-1.18, FR-1.19, FR-1.20, FR-1.21
- **Labels/Tags**: `ai`, `resume-parsing`, `nlp`, `mvp`

---

## Epic: EPIC-05 — Automated Email Communication

---

### User Story: US-019

#### Card
**As a** Recruiter  
**I want** the system to automatically send the appropriate email to a candidate when their application moves to a new pipeline stage  
**So that** candidates stay informed without me writing individual emails

#### Conversation
- **Context**: Each pipeline stage transition triggers a `STAGE_CHANGED` event consumed by the Notification Service. The service selects the matching email template, renders it with merge tags, and dispatches via SendGrid.
- **Assumptions**: Emails are sent asynchronously via RabbitMQ. A failure in email delivery does not block the pipeline move. Templates are pre-configured per company.
- **Dependencies**: US-017 (stage change triggers event), US-022/FR-1.22 (templates exist)
- **Notes**: This story covers the triggering mechanism. Template management is a supporting capability within EPIC-05.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Stage change triggers email
- **Given** an email template is active for the `stage_changed` trigger event
- **When** a Recruiter moves a candidate card from "Applied" to "Screening"
- **Then** the system sends the stage-change email to the candidate's email address with rendered merge tags (candidate name, job title, company name) within 60 seconds

**Scenario 2**: Email delivery failure does not block pipeline
- **Given** SendGrid returns a 500 error when dispatching a stage-change email
- **When** the email dispatch fails
- **Then** the pipeline stage change remains committed, the failure is logged, and the system retries email delivery up to 3 times

**Scenario 3**: No active template — no email sent
- **Given** the email template for `stage_changed` is marked as `inactive`
- **When** a Recruiter moves a candidate card
- **Then** the stage change completes successfully but no email is sent to the candidate

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Async — decoupled from pipeline logic |
| **N**egotiable | ✅ | Retry count, fallback behavior |
| **V**aluable | ✅ | Eliminates manual follow-up emails |
| **E**stimable | ✅ | Event consumer + template renderer + SendGrid call |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Trigger, delivery, and failure scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Automated Email Communication
- **Epic ID**: EPIC-05
- **PRD Requirement**: FR-1.22, FR-1.23, FR-1.24, FR-1.25
- **Labels/Tags**: `email`, `automation`, `notifications`, `mvp`

---

## Epic: EPIC-06 — Interview Self-Scheduling & Calendar Sync

---

### User Story: US-021

#### Card
**As a** Recruiter  
**I want** the system to send an interview invitation email with a self-scheduling link when a candidate reaches the Interview stage  
**So that** interview coordination is fully automated

#### Conversation
- **Context**: When an application transitions to the Interview stage, the Notification Service triggers the interview invitation template with a tokenized scheduling link. The token is CSPRNG-generated, valid for 72 hours.
- **Assumptions**: The interview invitation template must be active. The interviewer must have a connected calendar (US-004).
- **Dependencies**: US-017 (stage change to Interview), US-004 (calendar connected), US-019 (email dispatch mechanism)
- **Notes**: If the interviewer has no connected calendar, the system falls back to a manual scheduling note.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Automatic scheduling link on Interview stage
- **Given** an interviewer has a connected Google Calendar and the interview invitation template is active
- **When** a Recruiter moves a candidate card to the "Interview" stage
- **Then** the system generates a CSPRNG token (72h TTL), creates a SCHEDULED_EVENT with status `pending`, and sends an invitation email with the self-scheduling link to the candidate

**Scenario 2**: No connected calendar fallback
- **Given** the assigned interviewer has `calendar_provider` set to `none`
- **When** a candidate moves to the Interview stage
- **Then** the system sends the interview invitation without a scheduling link and notifies the Recruiter that manual scheduling is required

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Triggered by stage change event |
| **N**egotiable | ✅ | Token TTL, fallback behavior |
| **V**aluable | ✅ | Initiates zero-touch scheduling flow |
| **E**stimable | ✅ | Token generation + email dispatch |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | With and without calendar scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Interview Self-Scheduling & Calendar Sync
- **Epic ID**: EPIC-06
- **PRD Requirement**: FR-1.27
- **Labels/Tags**: `scheduling`, `email`, `mvp`

---

### User Story: US-022

#### Card
**As a** Candidate  
**I want** to click the scheduling link and select an available time slot from the interviewer's calendar  
**So that** I can book my interview without any back-and-forth emails

#### Conversation
- **Context**: The self-scheduling portal shows available slots for the next 14 days based on the interviewer's connected calendar. Slots are filtered by minimum interview duration.
- **Assumptions**: Portal is public-facing (token-authenticated, no login required). Slots refresh on page load.
- **Dependencies**: US-021 (scheduling link sent), US-004 (calendar connected)
- **Notes**: Portal must be mobile-friendly for candidates viewing on their phone.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: View and select available slots
- **Given** a Candidate clicks a valid, non-expired scheduling link
- **When** the self-scheduling portal loads
- **Then** the system queries the interviewer's calendar for free slots in the next 14 days, displays available time slots grouped by date, and the Candidate can select their preferred slot

**Scenario 2**: Expired token
- **Given** a Candidate clicks a scheduling link that is older than 72 hours
- **When** the portal attempts to load
- **Then** the system shows an "This link has expired" message with instructions to contact the Recruiter, and the Recruiter receives an in-app alert

**Scenario 3**: No available slots
- **Given** the interviewer's calendar is fully booked for the next 14 days
- **When** the Candidate loads the scheduling portal
- **Then** the system shows a "No available slots" message and suggests contacting the Recruiter directly

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Self-contained portal page |
| **N**egotiable | ✅ | Date range, slot duration filters |
| **V**aluable | ✅ | Eliminates scheduling back-and-forth |
| **E**stimable | ✅ | Calendar API + slot rendering |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Valid, expired, and no-slots scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Interview Self-Scheduling & Calendar Sync
- **Epic ID**: EPIC-06
- **PRD Requirement**: FR-1.28
- **Labels/Tags**: `scheduling`, `candidate-portal`, `mvp`

---

### User Story: US-023

#### Card
**As a** Candidate  
**I want** to confirm my selected time slot and have it automatically appear in the interviewer's calendar  
**So that** my interview is officially booked with no manual coordination needed

#### Conversation
- **Context**: On slot confirmation, the system performs a real-time availability check (guard against concurrent bookings), creates a SCHEDULED_EVENT, and writes a calendar event via the Calendar Adapter.
- **Assumptions**: Calendar event includes video meeting link (Google Meet / Teams) if supported. Confirmation email includes an `.ics` attachment.
- **Dependencies**: US-022 (slot selected), US-004 (calendar connected)
- **Notes**: Optimistic locking or atomic transaction needed to prevent double-booking.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Successful booking confirmation
- **Given** a Candidate selects an available slot at "2026-04-10 10:00 AM"
- **When** they click "Confirm"
- **Then** the system performs a real-time availability check, creates a SCHEDULED_EVENT with status `confirmed`, writes a calendar event to the interviewer's calendar with video meeting link, sends a confirmation email to the Candidate (with .ics), sends a notification to the Recruiter, and queues a 24-hour reminder

**Scenario 2**: Concurrent booking conflict
- **Given** two candidates attempt to book the same slot simultaneously
- **When** the second candidate clicks "Confirm"
- **Then** the system detects the conflict, shows "This slot is no longer available — please select another", and refreshes the available slots list

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Booking confirmation is a distinct step |
| **N**egotiable | ✅ | Meeting link generation, .ics format |
| **V**aluable | ✅ | Completes the self-service booking |
| **E**stimable | ✅ | Calendar write + conflict detection |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Success + concurrent conflict |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Interview Self-Scheduling & Calendar Sync
- **Epic ID**: EPIC-06
- **PRD Requirement**: FR-1.29, FR-1.30
- **Labels/Tags**: `scheduling`, `calendar`, `booking`, `mvp`

---

### User Story: US-024

#### Card
**As a** Candidate  
**I want** to receive a reminder email 24 hours before my interview  
**So that** I don't forget the scheduled time

#### Conversation
- **Context**: The system queues a reminder email job when a booking is confirmed (US-023). The reminder uses the `interview_reminder` email template.
- **Assumptions**: Reminder includes date/time, interviewer name, video meeting link, and reschedule/cancel links.
- **Dependencies**: US-023 (booking confirmed)
- **Notes**: If the candidate cancels before the reminder fires, the reminder job is cancelled.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Reminder sent 24 hours before interview
- **Given** a confirmed interview scheduled for 2026-04-10 at 10:00 AM
- **When** the current time reaches 2026-04-09 at 10:00 AM
- **Then** the system sends a reminder email to the Candidate with interview details, meeting link, and reschedule/cancel options

**Scenario 2**: Cancelled interview suppresses reminder
- **Given** a confirmed interview with a queued reminder
- **When** the Candidate cancels the interview before the reminder fires
- **Then** the reminder job is cancelled and no reminder email is sent

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Scheduled job runs independently |
| **N**egotiable | ✅ | Reminder timing (24h vs 48h) |
| **V**aluable | ✅ | Reduces no-shows |
| **E**stimable | ✅ | Scheduled job + email dispatch |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Timing + cancellation suppression |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Interview Self-Scheduling & Calendar Sync
- **Epic ID**: EPIC-06
- **PRD Requirement**: FR-1.30
- **Labels/Tags**: `scheduling`, `reminders`, `mvp`

---

### User Story: US-025

#### Card
**As a** Candidate  
**I want** to reschedule or cancel my interview via a one-click link in my confirmation or reminder email  
**So that** I can manage changes without contacting the Recruiter

#### Conversation
- **Context**: Confirmation and reminder emails include reschedule and cancel links. Rescheduling re-opens the self-scheduling portal; cancellation updates the calendar event and alerts the Recruiter.
- **Assumptions**: Reschedule generates a new scheduling token. Cancel is immediate and irreversible (must contact Recruiter to re-initiate).
- **Dependencies**: US-023 (booking exists), US-022 (portal for rescheduling)
- **Notes**: Calendar event is updated (reschedule) or deleted (cancel) via the Calendar Adapter.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Candidate reschedules
- **Given** a Candidate has a confirmed interview and clicks "Reschedule" in the email
- **When** the self-scheduling portal re-opens with fresh available slots
- **Then** the Candidate selects a new slot, the existing SCHEDULED_EVENT is updated, the calendar event is modified, and new confirmation emails are sent to both Candidate and Recruiter

**Scenario 2**: Candidate cancels
- **Given** a Candidate has a confirmed interview and clicks "Cancel" in the email
- **When** they confirm the cancellation
- **Then** the SCHEDULED_EVENT status changes to `cancelled`, the calendar event is deleted, the Recruiter receives an immediate notification via email and in-app, and the 24h reminder job is cancelled

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Self-service action via email link |
| **N**egotiable | ✅ | Reschedule limits, cancel confirmation flow |
| **V**aluable | ✅ | Reduces scheduling friction and no-shows |
| **E**stimable | ✅ | Calendar update + event state change |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Reschedule + cancel flows |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Interview Self-Scheduling & Calendar Sync
- **Epic ID**: EPIC-06
- **PRD Requirement**: FR-1.31, FR-1.32
- **Labels/Tags**: `scheduling`, `self-service`, `mvp`

---

## Epic: EPIC-03 — Candidate Pipeline & Kanban Board (continued — Hiring Decision)

---

### User Story: US-026

#### Card
**As a** Recruiter or Hiring Manager  
**I want** to record interview feedback and a score after the interview is completed  
**So that** the hiring team can make informed decisions based on structured evaluations

#### Conversation
- **Context**: After an interview, both the Recruiter and Hiring Manager should be able to submit feedback. This ties back to the Interview record, not just the Application.
- **Assumptions**: Feedback includes free-text notes and a 1–5 score per interviewer. Multiple interviewers can submit independently.
- **Dependencies**: US-023 (interview was scheduled and conducted)
- **Notes**: Interview status should transition to `completed` when feedback is submitted.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Submit post-interview feedback
- **Given** an interview for a candidate has been completed
- **When** the Hiring Manager opens the interview record and enters feedback text and a score of 4
- **Then** the feedback and score are saved on the Interview record, the interview status changes to `completed`, and the feedback appears on the candidate profile timeline

**Scenario 2**: Multiple interviewers provide feedback
- **Given** a panel interview with two interviewers
- **When** each interviewer submits their feedback independently
- **Then** both feedback entries are visible on the Interview record with respective author names, scores, and timestamps

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Feedback submission is self-contained |
| **N**egotiable | ✅ | Score range, structured vs free-text |
| **V**aluable | ✅ | Data-driven hiring decisions |
| **E**stimable | ✅ | Form + persistence |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Single + multi-interviewer scenarios |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.15
- **Labels/Tags**: `interview`, `feedback`, `mvp`

---

### User Story: US-027

#### Card
**As a** Hiring Manager  
**I want** to approve or reject a candidate after reviewing their profile and interview feedback  
**So that** the Recruiter knows whether to proceed with an offer or rejection

#### Conversation
- **Context**: After interviews, the Hiring Manager makes the go/no-go decision. Approval advances the candidate toward Offer; rejection moves them to Rejected.
- **Assumptions**: The Hiring Manager can approve/reject from the candidate profile page. Decision triggers a pipeline stage change.
- **Dependencies**: US-026 (feedback exists), US-017 (stage change mechanism)
- **Notes**: Rejection by the Hiring Manager automatically moves the card to Rejected and triggers a rejection email.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Hiring Manager approves
- **Given** a Hiring Manager reviews a candidate's profile with post-interview feedback and scores
- **When** they click "Approve for Offer"
- **Then** the application card moves to the "Offer" pipeline stage, a `STAGE_CHANGED` event is published, and the Recruiter receives a notification

**Scenario 2**: Hiring Manager rejects
- **Given** a Hiring Manager reviews a candidate and decides not to proceed
- **When** they click "Reject"
- **Then** the application card moves to the "Rejected" stage, a rejection email is triggered to the candidate, and the Recruiter is notified

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Decision action from HM |
| **N**egotiable | ✅ | Approval workflow vs direct stage change |
| **V**aluable | ✅ | Empowers HMs in hiring process |
| **E**stimable | ✅ | Button actions triggering stage changes |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Approve + reject paths |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.13
- **Labels/Tags**: `hiring-decision`, `pipeline`, `mvp`

---

### User Story: US-028

#### Card
**As a** Recruiter  
**I want** to extend an offer to a candidate and send an offer notification email  
**So that** the candidate is formally notified and the offer is tracked in the system

#### Conversation
- **Context**: When the application reaches the "Offer" stage, the Recruiter sends the offer notification. The email uses the `offer_extended` template.
- **Assumptions**: Offer letter generation and e-signatures are out of scope (PRD non-goal). This story covers the notification and status tracking only.
- **Dependencies**: US-027 (HM approved), US-019 (email dispatch)
- **Notes**: The Recruiter may also communicate offer details outside LTI (phone, separate email with attachment).

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Send offer notification
- **Given** a candidate's application is in the "Offer" stage
- **When** the Recruiter clicks "Send Offer Notification"
- **Then** the system dispatches the offer email template with merge tags (candidate name, job title, company name) to the candidate, and the email appears in the candidate's communication log

**Scenario 2**: Offer stage triggers automated email
- **Given** the `offer_extended` email template is active
- **When** a candidate card moves to the "Offer" stage (via HM approval or drag)
- **Then** the offer notification email is automatically sent without additional Recruiter action

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Notification on offer stage |
| **N**egotiable | ✅ | Manual send vs auto-trigger |
| **V**aluable | ✅ | Professional candidate communication |
| **E**stimable | ✅ | Template rendering + email dispatch |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Email dispatch + log entry |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.24
- **Labels/Tags**: `offer`, `email`, `mvp`

---

### User Story: US-029

#### Card
**As a** Recruiter  
**I want** to mark a candidate as hired and close their application  
**So that** the final hiring outcome is recorded and pipeline metrics are accurate

#### Conversation
- **Context**: Moving a candidate to the "Hired" terminal stage completes the recruiting lifecycle for that application.
- **Assumptions**: Hired candidates remain in the candidate database for future reference. Pipeline metrics (time-to-hire) are calculated from `applied_at` to the `hired` timestamp.
- **Dependencies**: US-028 (offer extended, candidate accepted)
- **Notes**: This is the final step in the recruiting workflow.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Mark as hired
- **Given** a candidate's application is in the "Offer" stage and the offer has been accepted
- **When** the Recruiter drags the card to the "Hired" stage (terminal)
- **Then** the Application status updates to `hired`, the pipeline stage is set to the terminal-hired stage, and a timestamp is recorded

**Scenario 2**: Hired candidate visible in history
- **Given** a candidate has been marked as hired
- **When** the Recruiter views the candidate's profile
- **Then** the application shows status "Hired" with the hire date, and all history (notes, scores, interviews, emails) is preserved

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Terminal state transition |
| **N**egotiable | ✅ | Post-hire actions (onboarding trigger?) |
| **V**aluable | ✅ | Completes the recruiting cycle, enables metrics |
| **E**stimable | ✅ | Status update + timestamp |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | State change + data preservation |

#### Metadata
- **Priority**: Must Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Pipeline & Kanban Board
- **Epic ID**: EPIC-03
- **PRD Requirement**: FR-1.13
- **Labels/Tags**: `hiring`, `pipeline`, `mvp`

---

## Epic: EPIC-10 — Additional Job Board Integrations (Phase 2)

---

### User Story: US-011

#### Card
**As an** HR Admin  
**I want** to syndicate job postings to additional job boards (e.g., Glassdoor)  
**So that** I can reach a wider candidate pool beyond Indeed and LinkedIn

#### Conversation
- **Context**: Phase 2 expansion. The adapter pattern from EPIC-02 makes adding new boards straightforward.
- **Assumptions**: Each new board requires an API integration. The syndication dashboard (US-009) already supports multiple boards.
- **Dependencies**: US-008 (syndication infrastructure from MVP)
- **Notes**: Priority of additional boards will be determined by customer demand data.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Syndicate to Glassdoor
- **Given** Glassdoor API credentials are configured and a job posting is ready to publish
- **When** the HR Admin selects Glassdoor in addition to Indeed and LinkedIn and clicks "Publish"
- **Then** the system syndicates the posting to all three boards, and each board appears on the syndication dashboard with its respective status

**Scenario 2**: Board-specific field mapping
- **Given** Glassdoor requires a field not present in the standard job posting form (e.g., company rating)
- **When** the system syndicates to Glassdoor
- **Then** optional Glassdoor-specific fields are either left empty or populated from company profile data, without blocking the syndication

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | New adapter added to existing infrastructure |
| **N**egotiable | ✅ | Which boards, field mappings |
| **V**aluable | ✅ | Expands candidate reach |
| **E**stimable | ✅ | New API adapter per board |
| **S**mall | ✅ | Single sprint per board |
| **T**estable | ✅ | Syndication success + dashboard display |

#### Metadata
- **Priority**: Could Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Additional Job Board Integrations
- **Epic ID**: EPIC-10
- **PRD Requirement**: FR-2.4
- **Labels/Tags**: `syndication`, `job-boards`, `phase-2`

---

## Epic: EPIC-09 — AI Screening Assistant (Phase 2)

---

### User Story: US-020

#### Card
**As a** Recruiter  
**I want** the system to recommend a shortlist of best-fit candidates for a job posting  
**So that** I can focus my time on the most promising applicants

#### Conversation
- **Context**: Phase 2 premium add-on ($99/mo). The AI evaluates parsed resume data against job posting requirements and produces a ranked shortlist.
- **Assumptions**: AI scoring is advisory — the Recruiter always makes the final decision. Scoring criteria are transparent (not a black box).
- **Dependencies**: US-013 (parsed resume data), US-030 (candidate database)
- **Notes**: Must mitigate bias risk — scoring should be based on skills/experience match, not demographic signals.

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Generate AI shortlist
- **Given** a job posting has 50 applications with parsed resume data
- **When** the Recruiter clicks "Generate AI Shortlist"
- **Then** the system evaluates each candidate against the job requirements and displays a ranked list of the top 10 candidates with a fit score and reasoning summary

**Scenario 2**: Recruiter overrides AI recommendation
- **Given** an AI-generated shortlist is displayed
- **When** the Recruiter adds a candidate not in the shortlist to the "Interview" stage
- **Then** the system allows the action without restriction and logs the override

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Add-on feature, separate module |
| **N**egotiable | ✅ | Scoring criteria, shortlist size |
| **V**aluable | ✅ | Revenue driver + recruiter efficiency |
| **E**stimable | ✅ | AI model integration + UI |
| **S**mall | ✅ | Single sprint (integration, not building model) |
| **T**estable | ✅ | Shortlist generation + override behavior |

#### Metadata
- **Priority**: Could Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: AI Screening Assistant
- **Epic ID**: EPIC-09
- **PRD Requirement**: FR-2.3
- **Labels/Tags**: `ai`, `screening`, `premium`, `phase-2`

---

## Epic: EPIC-07 — Candidate Database & Search (Phase 2)

---

### User Story: US-030

#### Card
**As a** Recruiter  
**I want** to search all past candidates by keyword across their parsed resume data  
**So that** I can re-engage suitable applicants for new openings

#### Conversation
- **Context**: Phase 2 feature. Search indexes the `raw_resume_text` field and parsed structured fields (skills, job titles, companies).
- **Assumptions**: Full-text search powered by PostgreSQL `tsvector` or a dedicated search index. Results show candidate name, last application, and matching keywords highlighted.
- **Dependencies**: US-013 (parsed + indexed resume data)
- **Notes**: Respects company-level data isolation (multi-tenant).

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: Keyword search returns results
- **Given** a Recruiter navigates to the Candidate Database and enters "Python Django"
- **When** they click "Search"
- **Then** the system returns a list of candidates whose parsed resumes contain "Python" or "Django", sorted by relevance, with matching terms highlighted

**Scenario 2**: No results found
- **Given** a Recruiter searches for "quantum computing"
- **When** no candidates match
- **Then** the system displays "No candidates found matching your search" with a suggestion to broaden the query

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Search module reads existing data |
| **N**egotiable | ✅ | Search technology, ranking algorithm |
| **V**aluable | ✅ | Talent re-engagement — increases retention |
| **E**stimable | ✅ | Search index + query UI |
| **S**mall | ✅ | Single sprint |
| **T**estable | ✅ | Results + no-results scenarios |

#### Metadata
- **Priority**: Should Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Candidate Database & Search
- **Epic ID**: EPIC-07
- **PRD Requirement**: FR-2.1
- **Labels/Tags**: `search`, `candidate-database`, `phase-2`

---

## Epic: EPIC-08 — Analytics & Reporting (Phase 2)

---

### User Story: US-031

#### Card
**As an** HR Admin  
**I want** to view a dashboard with hiring pipeline analytics  
**So that** I can measure recruiting effectiveness and identify bottlenecks

#### Conversation
- **Context**: Phase 2 feature. Dashboard shows key metrics: time-to-hire, stage conversion rates, source effectiveness (career page vs Indeed vs LinkedIn), and active pipeline counts.
- **Assumptions**: Data computed from existing Application, Interview, and Job Posting records. No external BI tool integration for MVP.
- **Dependencies**: EPIC-02 (job data), EPIC-03 (application data), sufficient data volume
- **Notes**: This supports KPI-3 (recruiter admin time reduction) and KPI-8 (churn reduction).

#### Confirmation (Acceptance Criteria — BDD)

**Scenario 1**: View analytics dashboard
- **Given** an HR Admin navigates to the Analytics section
- **When** the dashboard loads
- **Then** it displays: average time-to-hire (days), stage conversion rates (% moving from each stage to the next), applications by source (pie chart), and active pipeline counts per job posting

**Scenario 2**: Filter by date range
- **Given** an HR Admin is on the analytics dashboard
- **When** they select a date range of "Last 30 days"
- **Then** all metrics update to reflect only applications and hires within that period

#### INVEST Checklist
| Criterion | Met? | Notes |
|-----------|------|-------|
| **I**ndependent | ✅ | Read-only aggregation of existing data |
| **N**egotiable | ✅ | Which metrics, chart types |
| **V**aluable | ✅ | Data-driven hiring improvements |
| **E**stimable | ✅ | Query aggregation + chart rendering |
| **S**mall | ✅ | Single sprint (basic dashboard) |
| **T**estable | ✅ | Metric accuracy + filter behavior |

#### Metadata
- **Priority**: Should Have
- **Story Points**: —
- **Sprint**: —
- **Epic/Feature**: Analytics & Reporting
- **Epic ID**: EPIC-08
- **PRD Requirement**: FR-2.2
- **Labels/Tags**: `analytics`, `dashboard`, `phase-2`

---

## Summary

| Release Slice | Stories | Count |
|---------------|---------|-------|
| **MVP (Phase 1)** | US-001 through US-029 (excl. US-011, US-020) | 27 |
| **Growth (Phase 2)** | US-011, US-020, US-030, US-031 | 4 |
| **Total** | | **31** |

| Epic ID | Epic Name | Stories |
|---------|-----------|---------|
| EPIC-01 | Company & User Management | US-001, US-002, US-003, US-004, US-005 |
| EPIC-02 | Job Posting & Syndication | US-006, US-007, US-008, US-009, US-010 |
| EPIC-03 | Candidate Pipeline & Kanban Board | US-012, US-014, US-015, US-016, US-017, US-018, US-026, US-027, US-028, US-029 |
| EPIC-04 | AI Resume Parsing | US-013 |
| EPIC-05 | Automated Email Communication | US-019 |
| EPIC-06 | Interview Self-Scheduling & Calendar Sync | US-021, US-022, US-023, US-024, US-025 |
| EPIC-07 | Candidate Database & Search | US-030 |
| EPIC-08 | Analytics & Reporting | US-031 |
| EPIC-09 | AI Screening Assistant | US-020 |
| EPIC-10 | Additional Job Board Integrations | US-011 |
