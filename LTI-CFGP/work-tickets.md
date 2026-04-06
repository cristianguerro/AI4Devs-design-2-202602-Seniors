# Work Tickets: LTI ATS

**Product**: LTI ATS (Applicant Tracking System)  
**Source PRD**: [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md)  
**User Stories**: [UserStories-CFGP.md](./UserStories-CFGP.md)  
**Backlog**: [product-backlog.md](./product-backlog.md)

---

## Estimation Scale

| Story Points | T-Shirt Size | Complexity | Typical Scope | Approx. Hours |
|-------------|-------------|------------|---------------|---------------|
| 1 | XS | Trivial | Config change, copy update, minor CSS fix | 1–2h |
| 2 | S | Low | Simple feature, minor bug fix, small refactor | 2–4h |
| 3 | S-M | Low-Medium | Well-understood task, single component | 4–8h |
| 5 | M | Medium | Standard feature, moderate complexity | 8–16h |
| 8 | L | Medium-High | Complex feature, multiple components, integration work | 16–24h |
| 13 | XL | High | Major feature, significant unknowns, cross-team coordination | 24–40h |
| 21 | XXL | Very High | Epic-level work — recommend decomposition | 40h+ |

---

## Decomposition Checklist

| User Story | Title | Tickets | Total SP | Status |
|------------|-------|---------|----------|--------|
| US-001 | Sign up & create company account | TK-001, TK-002, TK-003, TK-004 | 16 | ✅ Decomposed |
| US-002 | Invite team members with roles | TK-005, TK-006, TK-007, TK-008 | 18 | ✅ Decomposed |
| US-003 | Configure company profile & branding | TK-009, TK-010, TK-011 | 11 | ✅ Decomposed |
| US-004 | Connect calendar (Google/Outlook) | — | — | ⬜ Pending |
| US-005 | Customize pipeline stages | — | — | ⬜ Pending |
| US-006 | Create job posting with structured fields | — | — | ⬜ Pending |
| US-007 | Preview job on branded career page | — | — | ⬜ Pending |
| US-008 | Publish & syndicate to job boards | — | — | ⬜ Pending |
| US-009 | View syndication status per board | — | — | ⬜ Pending |
| US-010 | Close/archive job across all boards | — | — | ⬜ Pending |
| US-011 | Syndicate to additional boards | — | — | ⬜ Pending |
| US-012 | Receive applications via career page & boards | — | — | ⬜ Pending |
| US-013 | Auto-parse resume data (AI) | — | — | ⬜ Pending |
| US-014 | Review parsed candidate profile | — | — | ⬜ Pending |
| US-015 | Detect duplicate candidates | — | — | ⬜ Pending |
| US-016 | View candidates on Kanban board | — | — | ⬜ Pending |
| US-017 | Drag card to advance or reject candidate | — | — | ⬜ Pending |
| US-018 | Add notes & score to application | — | — | ⬜ Pending |
| US-019 | Auto-send stage change email | — | — | ⬜ Pending |
| US-020 | AI-recommended shortlist | — | — | ⬜ Pending |
| US-021 | Send interview invitation with scheduling link | — | — | ⬜ Pending |
| US-022 | Candidate self-selects available time slot | — | — | ⬜ Pending |
| US-023 | Confirm booking & sync calendar event | — | — | ⬜ Pending |
| US-024 | Send 24h reminder to candidate | — | — | ⬜ Pending |
| US-025 | Candidate reschedules or cancels | — | — | ⬜ Pending |
| US-026 | Record interview feedback & score | — | — | ⬜ Pending |
| US-027 | Hiring Manager approves or rejects | — | — | ⬜ Pending |
| US-028 | Extend offer & send notification | — | — | ⬜ Pending |
| US-029 | Mark candidate as hired | — | — | ⬜ Pending |
| US-030 | Search past candidates by keyword | — | — | ⬜ Pending |
| US-031 | View pipeline analytics dashboard | — | — | ⬜ Pending |

---

# US-001 — Sign up & create company account

---

## Ticket: TK-001

### Title
Create Company and User database schemas and migrations

### Description
Design and implement the PostgreSQL schemas for the `COMPANY` and `USER` tables as defined in the system design data model. Create database migration scripts that set up the tables with all columns, constraints, indexes, and default values. This is the foundational data layer that all other features depend on.

- **Company table**: id (UUID PK), name, slug (unique), logo_url, website, plan_tier (enum), created_at, updated_at
- **User table**: id (UUID PK), company_id (FK → COMPANY), email (unique), password_hash, role (enum: admin, recruiter, hiring_manager), first_name, last_name, calendar_provider, cal_access_token, cal_refresh_token, is_active, created_at, updated_at
- Add unique index on `slug` and `email`
- Add foreign key constraint on `company_id`

### Acceptance Criteria
- [ ] **Given** the migration is run **When** the database is inspected **Then** the `companies` and `users` tables exist with all specified columns, types, and constraints
- [ ] **Given** a UUID is generated for a new Company **When** it is inserted **Then** the PK is a valid UUIDv4
- [ ] **Given** a slug value already exists **When** another company tries to use the same slug **Then** a unique constraint violation is raised
- [ ] **Given** an email already exists **When** another user tries to use the same email **Then** a unique constraint violation is raised

### Priority
Must Have

### Estimation
- **Story Points**: 3
- **T-Shirt Size**: S-M
- **Estimated Hours**: 4–6h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `database`, `migration`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. Foundation for all platform data. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-001 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-001) |
| PRD Requirement | FR-1.1 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | — | None |
| Blocks | TK-002, TK-003, TK-004 | — |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 3 SP, S-M, 4–6h |

---

## Ticket: TK-002

### Title
Implement signup API endpoint with password hashing and company creation

### Description
Build the `POST /api/auth/signup` REST endpoint that handles new user registration. The endpoint receives email, password, and company name, validates input, creates a Company record with auto-generated slug, hashes the password with bcrypt, creates a User record with `admin` role, and returns a JWT access token.

**Business logic:**
- Auto-generate slug from company name (lowercase, hyphenated, deduplicated with suffix if collision)
- Hash password with bcrypt (cost factor 12)
- Generate JWT with user ID, company ID, and role
- Return 201 with JWT on success; 409 on duplicate email; 422 on validation errors

**Validation rules:**
- Email: valid format, required
- Password: min 8 chars, at least 1 uppercase, 1 number
- Company name: required, 2–255 chars

### Acceptance Criteria
- [ ] **Given** valid email, password, and company name **When** `POST /api/auth/signup` is called **Then** a Company and User are created, a JWT is returned with status 201
- [ ] **Given** an email that already exists **When** signup is attempted **Then** the API returns 409 with error message "An account with this email already exists"
- [ ] **Given** a password shorter than 8 characters **When** signup is attempted **Then** the API returns 422 with password requirement details
- [ ] **Given** a company name "Acme Corp" **When** signup completes **Then** the slug is auto-generated as "acme-corp" (or "acme-corp-1" if collision)
- [ ] **Given** a valid signup **When** the password is stored **Then** it is stored as a bcrypt hash, not plaintext

### Priority
Must Have

### Estimation
- **Story Points**: 5
- **T-Shirt Size**: M
- **Estimated Hours**: 10–14h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `api`, `auth`, `security`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. Core auth endpoint — security-critical. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-001 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-001) |
| PRD Requirement | FR-1.1, FR-1.4 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-001 | Database schemas must exist |
| Blocks | TK-005 | Invitation flow needs auth |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 5 SP, M, 10–14h |

---

## Ticket: TK-003

### Title
Build signup page UI with form validation and error handling

### Description
Create the frontend signup page (React + TypeScript) with a registration form containing fields for email, password, password confirmation, and company name. Implement client-side validation matching the backend rules, call the signup API, handle success (redirect to onboarding dashboard) and error states (duplicate email, weak password).

**UI components:**
- Email input with format validation
- Password input with strength indicator (min 8 chars, 1 uppercase, 1 number)
- Password confirmation input with match validation
- Company name input (2–255 chars)
- "Create Account" submit button with loading state
- Error alerts for API-returned errors (409 duplicate, 422 validation)
- Success redirect to `/onboarding`

### Acceptance Criteria
- [ ] **Given** a user visits `/signup` **When** the page loads **Then** the signup form is displayed with all required fields
- [ ] **Given** valid inputs **When** the user clicks "Create Account" **Then** the form submits to the API, shows a loading spinner, and redirects to `/onboarding` on 201
- [ ] **Given** the API returns 409 (duplicate email) **When** the error is received **Then** the form shows "An account with this email already exists" near the email field
- [ ] **Given** a password that fails validation **When** the user tabs away from the field **Then** client-side validation shows the requirements inline before form submission
- [ ] **Given** password and confirmation don't match **When** the user tabs away **Then** an inline error "Passwords do not match" is displayed

### Priority
Must Have

### Estimation
- **Story Points**: 5
- **T-Shirt Size**: M
- **Estimated Hours**: 8–12h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`frontend`, `auth`, `ui`, `forms`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. First user-facing screen — sets UX tone. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-001 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-001) |
| PRD Requirement | FR-1.1, FR-1.4 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-002 | Signup API must be ready |
| Blocks | TK-006 | Team settings page depends on auth flow |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 5 SP, M, 8–12h |

---

## Ticket: TK-004

### Title
Implement JWT authentication middleware and login endpoint

### Description
Create the authentication middleware that validates JWT tokens on protected API routes, and build the `POST /api/auth/login` endpoint for returning users. The middleware extracts the JWT from the `Authorization: Bearer` header, validates signature and expiry, and attaches user context (user ID, company ID, role) to the request.

**Login endpoint:**
- Accepts email + password
- Verifies password against bcrypt hash
- Returns 200 with new JWT on success; 401 on invalid credentials
- JWT includes: `userId`, `companyId`, `role`, `exp` (short-lived, e.g. 1h)

**Middleware:**
- Validates JWT signature (HS256 or RS256)
- Rejects expired tokens (401)
- Populates `req.user` with decoded payload
- Applies to all routes except `/api/auth/signup`, `/api/auth/login`, and public career page routes

### Acceptance Criteria
- [ ] **Given** a valid JWT in the Authorization header **When** a protected API is called **Then** the request proceeds with `req.user` populated
- [ ] **Given** an expired or invalid JWT **When** a protected API is called **Then** the API returns 401 Unauthorized
- [ ] **Given** valid email and password **When** `POST /api/auth/login` is called **Then** a new JWT is returned with status 200
- [ ] **Given** invalid email or password **When** login is attempted **Then** the API returns 401 with a generic "Invalid credentials" message (no email/password distinction for security)
- [ ] **Given** no Authorization header **When** a protected route is called **Then** the API returns 401

### Priority
Must Have

### Estimation
- **Story Points**: 3
- **T-Shirt Size**: S-M
- **Estimated Hours**: 5–8h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `auth`, `security`, `middleware`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. Security-critical — review JWT secret management. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-001 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-001) |
| PRD Requirement | FR-1.4 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-001, TK-002 | Needs DB + signup first |
| Blocks | TK-005, TK-009 | All authenticated features |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 3 SP, S-M, 5–8h |

---

# US-002 — Invite team members with roles

---

## Ticket: TK-005

### Title
Create invitation token schema and team invitation API endpoint

### Description
Build the `POST /api/team/invitations` endpoint that allows an authenticated Admin to invite team members. The endpoint generates a unique invitation token (CSPRNG, 72 chars), stores it with the target email, role, company ID, and expiration (7 days), and triggers an invitation email dispatch.

**Database:** Add `INVITATION` table (or extend users with pending state):
- id (UUID PK), company_id (FK), email, role (enum), token (unique, varchar 128), expires_at (TIMESTAMP), status (enum: pending, accepted, expired), created_by (FK → USER), created_at

**API contract:**
- Auth: requires `admin` role
- Request: `{ email: string, role: "recruiter" | "hiring_manager" }`
- Response 201: `{ invitationId, email, role, status: "pending", expiresAt }`
- Response 403: if caller is not admin
- Response 409: if email already has active invitation or existing user in same company

### Acceptance Criteria
- [ ] **Given** an Admin sends a valid invitation request **When** `POST /api/team/invitations` is called **Then** an invitation record is created with a CSPRNG token, 7-day expiry, and status `pending`
- [ ] **Given** a non-admin user calls the endpoint **When** the request is processed **Then** the API returns 403 Forbidden
- [ ] **Given** an invitation for the same email already exists (pending) **When** a new invitation is sent **Then** the API returns 409 with "An invitation is already pending for this email"
- [ ] **Given** a valid invitation is created **When** the invitation is stored **Then** the token is 72+ characters, generated via CSPRNG

### Priority
Must Have

### Estimation
- **Story Points**: 5
- **T-Shirt Size**: M
- **Estimated Hours**: 10–14h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `api`, `auth`, `rbac`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. RBAC enforcement is critical — only admins can invite. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-002 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-002) |
| PRD Requirement | FR-1.2, FR-1.3 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-001, TK-004 | DB schema + auth middleware |
| Blocks | TK-006, TK-007 | Email + frontend depend on this |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 5 SP, M, 10–14h |

---

## Ticket: TK-006

### Title
Implement invitation email dispatch via SendGrid

### Description
Integrate with SendGrid to send invitation emails when a team invitation is created. The email contains the invitee's role, the company name, the admin's name, and a signup link with the invitation token embedded as a URL parameter (`/signup/invite?token={token}`).

**Email content:**
- Subject: "You've been invited to join {Company Name} on LTI"
- Body: greeting, inviter name, assigned role, call-to-action button linking to the invite signup page, expiration notice ("This link expires in 7 days")
- Use a simple HTML template (not the full template engine from EPIC-05 — that's for candidate emails)

**Technical:**
- SendGrid API v3 integration
- Async dispatch (fire-and-forget with error logging)
- Store email delivery status on the invitation record (sent, failed)

### Acceptance Criteria
- [ ] **Given** an invitation is created successfully **When** the invitation event fires **Then** SendGrid receives a send request with the correct recipient, subject, and body containing the invitation link
- [ ] **Given** SendGrid returns a success response **When** the email is dispatched **Then** the invitation record's delivery status is set to `sent`
- [ ] **Given** SendGrid returns an error **When** dispatch fails **Then** the error is logged, the invitation remains in `pending` status, and the admin can resend from the team settings page

### Priority
Must Have

### Estimation
- **Story Points**: 3
- **T-Shirt Size**: S-M
- **Estimated Hours**: 4–6h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `email`, `integration`, `sendgrid`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. First SendGrid integration — sets pattern for EPIC-05. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-002 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-002) |
| PRD Requirement | FR-1.2 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-005 | Invitation API must create the record |
| Blocks | — | — |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 3 SP, S-M, 4–6h |

---

## Ticket: TK-007

### Title
Build invite-based signup endpoint and token validation

### Description
Create the `POST /api/auth/signup/invite` endpoint that allows an invited user to complete their registration. The endpoint validates the invitation token (exists, not expired, not already used), creates the User record under the inviting company with the pre-assigned role, marks the invitation as `accepted`, and returns a JWT.

**Flow:**
1. `GET /api/auth/invitations/{token}` — validate token and return invitation details (email, role, company name) for pre-populating the form
2. `POST /api/auth/signup/invite` — receives token, first_name, last_name, password; creates user; returns JWT

**Edge cases:**
- Expired token → 410 Gone with "Invitation expired" message
- Already used token → 409 Conflict
- Token not found → 404

### Acceptance Criteria
- [ ] **Given** a valid, non-expired invitation token **When** `GET /api/auth/invitations/{token}` is called **Then** the API returns the invitation details (email, role, company name) with status 200
- [ ] **Given** a valid token, name, and password **When** `POST /api/auth/signup/invite` is called **Then** a User is created with the invited role and company, the invitation status changes to `accepted`, and a JWT is returned
- [ ] **Given** an expired token **When** the endpoint is called **Then** the API returns 410 with "This invitation has expired"
- [ ] **Given** an already-accepted token **When** the endpoint is called **Then** the API returns 409 with "This invitation has already been used"

### Priority
Must Have

### Estimation
- **Story Points**: 5
- **T-Shirt Size**: M
- **Estimated Hours**: 8–12h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `api`, `auth`, `invitation`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. Token validation is security-critical — use constant-time comparison. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-002 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-002) |
| PRD Requirement | FR-1.2, FR-1.3 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-005 | Invitation records must exist |
| Blocks | TK-008 | Frontend invite signup page |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 5 SP, M, 8–12h |

---

## Ticket: TK-008

### Title
Build team settings UI with invite form and member list

### Description
Create the Team Settings page (React + TypeScript) accessible to Admin users. The page includes an invitation form (email + role selector + "Send Invite" button) and a team member list showing all users and pending invitations with their status.

**UI components:**
- Invite form: email input, role dropdown (Recruiter, Hiring Manager), "Send Invite" button with loading state
- Team member table: columns for Name, Email, Role, Status (Active/Pending/Expired), Date Added
- Pending invitations show a "Resend" button
- Success toast on invitation sent
- Error handling for 403 (not admin), 409 (duplicate)
- Page only accessible to users with `admin` role — redirect non-admins

### Acceptance Criteria
- [ ] **Given** an Admin navigates to Team Settings **When** the page loads **Then** the invite form and team member list are displayed
- [ ] **Given** the Admin enters a valid email, selects "Recruiter" role, and clicks "Send Invite" **When** the API returns 201 **Then** a success toast is shown and the invitee appears in the list as "Pending"
- [ ] **Given** a non-admin user navigates to `/settings/team` **When** the page loads **Then** they are redirected to the dashboard with an "Access denied" message
- [ ] **Given** a pending invitation exists **When** the Admin clicks "Resend" **Then** a new invitation email is sent and the expiration is reset

### Priority
Must Have

### Estimation
- **Story Points**: 5
- **T-Shirt Size**: M
- **Estimated Hours**: 10–14h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`frontend`, `ui`, `team`, `rbac`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. RBAC enforcement on frontend — admin-only page. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-002 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-002) |
| PRD Requirement | FR-1.2, FR-1.3 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-005, TK-007 | API endpoints for invite + accept |
| Blocks | — | — |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 5 SP, M, 10–14h |

---

# US-003 — Configure company profile & branding

---

## Ticket: TK-009

### Title
Implement company profile update API with logo upload to S3

### Description
Build the `PUT /api/company/profile` endpoint that allows an Admin to update company profile fields (name, slug, website) and upload a logo image to AWS S3. The endpoint validates file type (PNG/JPG only) and size (≤ 2MB), uploads to S3 with a deterministic key (`companies/{companyId}/logo.{ext}`), stores the CDN URL in the Company record, and returns the updated profile.

**Technical details:**
- Multipart form data handling for file upload
- S3 upload with `public-read` ACL (or via CloudFront)
- Slug validation: lowercase alphanumeric + hyphens, unique check
- If slug changes, validate new slug is not taken

**Validation rules:**
- Name: required, 2–255 chars
- Slug: lowercase, alphanumeric + hyphens, 3–100 chars, unique
- Website: valid URL format, optional
- Logo: PNG/JPG, ≤ 2MB

### Acceptance Criteria
- [ ] **Given** an Admin sends updated name, website, and a valid PNG logo **When** `PUT /api/company/profile` is called **Then** the logo is uploaded to S3, the Company record is updated with the CDN URL, and the API returns the updated profile
- [ ] **Given** a logo file is a GIF (unsupported format) **When** the upload is attempted **Then** the API returns 422 with "Only PNG and JPG formats are supported"
- [ ] **Given** a logo file exceeds 2MB **When** the upload is attempted **Then** the API returns 422 with "File size must not exceed 2MB"
- [ ] **Given** the Admin changes the slug to one already taken **When** the update is submitted **Then** the API returns 409 with "This URL slug is already in use"

### Priority
Must Have

### Estimation
- **Story Points**: 5
- **T-Shirt Size**: M
- **Estimated Hours**: 10–14h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `api`, `s3`, `file-upload`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. First S3 integration — sets pattern for resume uploads later. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-003 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-003) |
| PRD Requirement | FR-1.1 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-001, TK-004 | DB schema + auth middleware |
| Blocks | TK-010, TK-011 | Frontend + career page depend on this |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 5 SP, M, 10–14h |

---

## Ticket: TK-010

### Title
Build company profile settings UI with logo upload preview

### Description
Create the Company Settings page (React + TypeScript) where the Admin can edit company name, slug, website, and upload a logo. The form shows a live preview of the uploaded logo and validates inputs client-side before submission.

**UI components:**
- Company name input (pre-populated)
- Slug input (pre-populated, with `[slug].lti.careers` preview text)
- Website URL input
- Logo upload area with drag-and-drop support and image preview
- File type/size validation before upload (PNG/JPG, ≤ 2MB)
- "Save" button with loading state
- Success toast on save; inline errors on validation failure

### Acceptance Criteria
- [ ] **Given** an Admin navigates to Company Settings **When** the page loads **Then** the form is pre-populated with current company profile data and the current logo is displayed
- [ ] **Given** the Admin uploads a valid PNG logo **When** the file is selected **Then** a preview of the image is displayed before saving
- [ ] **Given** the Admin uploads a 3MB file **When** the file is selected **Then** client-side validation shows "File size must not exceed 2MB" before any API call
- [ ] **Given** the Admin updates name and website and clicks "Save" **When** the API returns success **Then** a success toast is shown and the career page preview URL updates

### Priority
Must Have

### Estimation
- **Story Points**: 3
- **T-Shirt Size**: S-M
- **Estimated Hours**: 6–8h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`frontend`, `ui`, `settings`, `file-upload`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. Logo preview + drag-and-drop are important UX details. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-003 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-003) |
| PRD Requirement | FR-1.1 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-009 | Profile update API |
| Blocks | — | — |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 3 SP, S-M, 6–8h |

---

## Ticket: TK-011

### Title
Implement branded career page route serving company profile data

### Description
Create the public endpoint `GET /careers/{slug}` that serves the branded career page for a company. This endpoint resolves the company by slug, returns the company profile (name, logo URL, website) and a list of active (`published`) job postings. This is a public, unauthenticated route.

**Technical details:**
- No authentication required (public-facing)
- Returns 404 if slug not found
- Returns only `published` job postings for the company
- Response suitable for server-side rendering or SPA hydration
- Cache-friendly (add `Cache-Control` headers, e.g. 5 min)

### Acceptance Criteria
- [ ] **Given** a valid company slug "acme-corp" **When** `GET /careers/acme-corp` is called **Then** the API returns the company profile (name, logo URL) and a list of published job postings with status 200
- [ ] **Given** a slug that does not exist **When** the endpoint is called **Then** the API returns 404
- [ ] **Given** a company has 3 published and 2 draft job postings **When** the career page is loaded **Then** only the 3 published postings are returned
- [ ] **Given** the career page is loaded **When** response headers are inspected **Then** a `Cache-Control` header is present with a TTL ≥ 60 seconds

### Priority
Must Have

### Estimation
- **Story Points**: 3
- **T-Shirt Size**: S-M
- **Estimated Hours**: 4–6h

### Assignee
- **Assigned to**: —
- **Reviewer**: —

### Tags
`backend`, `api`, `public`, `career-page`, `mvp`

### Comments
| Date | Author | Comment |
|------|--------|---------|
| 2026-04-05 | Product Manager | Ticket created. Public-facing — no auth. Sets up career page for EPIC-02 job posting flow. |

### Links & Resources
| Type | Description | URL/Reference |
|------|-------------|---------------|
| User Story | US-003 | [UserStories-CFGP.md](./UserStories-CFGP.md#user-story-us-003) |
| PRD Requirement | FR-1.1, FR-1.7 | [PRD-LTI-CFGP.md](./PRD-LTI-CFGP.md) |
| Depends On | TK-009 | Profile data must be saveable |
| Blocks | — | Needed by US-007 (preview) and US-008 (publish) |

### Change Log
| Date | Author | Change Description |
|------|--------|--------------------|
| 2026-04-05 | Product Manager | Ticket created |
| 2026-04-05 | Product Manager | Added effort estimation: 3 SP, S-M, 4–6h |

---

# Effort Estimation Summary

**Date**: 2026-04-05  
**Estimator**: Product Manager (AI-assisted)  
**Method**: Combined (Story Points + T-Shirt + Hours)

## Ticket Estimates

| Ticket ID | Title | User Story | Complexity | Uncertainty | Story Points | T-Shirt | Est. Hours | Rationale |
|-----------|-------|-----------|------------|-------------|--------------|---------|------------|-----------|
| TK-001 | Create Company/User DB schemas | US-001 | Low | Low | 3 | S-M | 4–6h | Standard schema + migration; data model is well-defined |
| TK-002 | Implement signup API endpoint | US-001 | Medium | Low | 5 | M | 10–14h | Auth logic + bcrypt + JWT + slug generation + validation |
| TK-003 | Build signup page UI | US-001 | Medium | Low | 5 | M | 8–12h | Form with validation, error handling, redirect — standard but needs polish |
| TK-004 | JWT auth middleware + login | US-001 | Low-Medium | Low | 3 | S-M | 5–8h | Well-known pattern; applies to all protected routes |
| TK-005 | Invitation token API endpoint | US-002 | Medium | Low | 5 | M | 10–14h | RBAC enforcement + token generation + DB schema for invitations |
| TK-006 | Invitation email via SendGrid | US-002 | Low-Medium | Medium | 3 | S-M | 4–6h | First SendGrid integration; some uncertainty on email template setup |
| TK-007 | Invite-based signup + token validation | US-002 | Medium | Low | 5 | M | 8–12h | Token validation (expiry, used, not found) + user creation under company |
| TK-008 | Team settings UI | US-002 | Medium | Low | 5 | M | 10–14h | Admin-only page with invite form + member list + resend |
| TK-009 | Company profile API + S3 logo upload | US-003 | Medium | Medium | 5 | M | 10–14h | File upload + S3 integration + slug validation; first S3 usage |
| TK-010 | Company profile settings UI | US-003 | Low-Medium | Low | 3 | S-M | 6–8h | Form with image preview + drag-and-drop — well-understood pattern |
| TK-011 | Branded career page route | US-003 | Low | Low | 3 | S-M | 4–6h | Simple public read endpoint; no auth; cache headers |

## Risks & Assumptions

| Ticket ID | Risk / Assumption | Impact on Estimate |
|-----------|------------------|-------------------|
| TK-002 | Slug collision handling may need iterative suffix logic | Minor — add 1–2h if complex deduplication needed |
| TK-006 | SendGrid account setup and API key provisioning not yet done | Could block development; recommend setting up account in parallel |
| TK-009 | S3 bucket configuration and IAM permissions must be pre-provisioned | Could block upload testing; recommend infrastructure ticket |
| TK-007 | Constant-time token comparison needed for security | Low impact but must not be overlooked in review |

## Summary

| Metric | Value |
|--------|-------|
| Total Tickets Estimated | 11 |
| Total Story Points | 45 |
| Total Estimated Hours | 79–124h |
| Tickets Flagged for Decomposition (>13 SP) | 0 |
| User Stories Covered | US-001, US-002, US-003 |
