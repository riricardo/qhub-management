# QHub – Complete Issues Overview
> Consolidated view of all issues with labels and full descriptions.

---

## Issue #1 — 🧱 EPIC 1 — Platform Foundation and Multi-Tenant Architecture

**Labels**
- `audit-logs`
- `auth`
- `epic`
- `epic:foundation-multitenant`
- `gdpr`
- `rbac`
- `tenant`

**Description**
## Objective
Establish the core technical foundation of the platform, enabling secure authentication,
multi-tenant isolation, and legal compliance from the start.

## Business Value
This epic enables the platform to safely host multiple companies, ensuring that:
- Each company operates in isolation
- Users have secure access
- Legal requirements (GDPR) are met

Without this foundation, no other feature can be safely delivered.

## Scope (Included)
- Authentication (email/password and Google)
- Automatic tenant creation
- Tenant data isolation
- Role-based access control (RBAC)
- Audit logs
- LGPD consent flow

## Out of Scope
- Billing
- Notifications
- Service execution logic

## Expected Outcome
Users can log in securely, operate within their own company environment,
and all actions are traceable for auditing purposes.

---

## Issue #2 — 👥 EPIC 2 — User and Permission Management

**Labels**
- `epic`
- `epic:user-permissions`
- `rbac`
- `tenant`

**Description**
## Goal
Allow managers to control users, roles, and permissions within their company.

## Business Value
Enables scalable team management and controlled access.

## Scope
- Employees
- Clients
- Permissions

---

## Issue #3 — 🚨 EPIC 3 — Incident Creation and Tracking

**Labels**
- `epic`
- `epic:incidents`
- `incidents`

**Description**
## Objective
Allow clients and managers to create, view, and track incidents that represent
service requests.

## Business Value
Incidents are the entry point of the business flow.
This epic enables customers to request services and managers to organize demand.

## Scope (Included)
- Incident creation by client
- Incident creation by manager
- Status tracking
- Attachments
- Cancellation before execution

## Out of Scope
- Budgeting
- Billing
- Notifications

## Expected Outcome
Clients can request services and track progress,
while managers can view and manage all incoming incidents.

---

## Issue #4 — 💰 EPIC 4 — Budgeting and Approval Flow

**Labels**
- `budgets`
- `epic`
- `epic:budget-approval`

**Description**
## Objective
Enable managers to define budgets for incidents and allow clients to approve
or reject them before service execution.

## Business Value
Prevents misunderstandings and ensures financial agreement before work starts.

## Scope (Included)
- Budget creation
- Budget approval/rejection
- Conversion of approved incidents into service orders

## Out of Scope
- Payment processing
- Invoicing

## Expected Outcome
Only approved incidents become executable service orders.

---

## Issue #5 — 🛠️ EPIC 5 — Service Order Execution

**Labels**
- `epic`
- `epic:service-order-execution`
- `service-orders`

**Description**
## Objective
Control the lifecycle of service orders from start to completion, enabling operational
visibility, accountability, and traceability.

## Business Value
This is where the service actually happens. The epic enables:
- Work delegation (assignment)
- Execution tracking (status + notes)
- Evidence collection (attachments)
- Proper closure (finalization) to support billing and reporting

## Scope (Included)
- List and view service orders
- Assignment to employees
- Status updates + status history
- Execution notes
- Evidence/attachments
- Finalization workflow
- Client notification trigger on completion
- Audit log coverage for key actions

## Out of Scope
- Payment processing (Sprint 6)
- WhatsApp integration (Sprint 5)
- Dashboard KPIs (Sprint 7)

## Expected Outcome
Managers and employees can execute services end-to-end with clear tracking,
and clients can be notified when work is completed.

---

## Issue #6 — 📢 EPIC 6 — Communication and Notifications

**Labels**
- `epic`
- `epic:communication`
- `notifications`
- `whatsapp`

**Description**
## Goal
Keep clients informed through automated communication channels.

## Business Value
Improves transparency and customer satisfaction.

## Scope
- Email
- WhatsApp
- Status notifications

## Stories
- [ ] #32
- [ ] #33
- [ ] #34
- [ ] #35
- [ ] #36

---

## Issue #7 — 💳 EPIC 7 — Payments and Billing

**Labels**
- `billing`
- `epic`
- `epic:payments-billing`
- `payments`

**Description**
## Goal
Handle service billing and payments.

## Business Value
Enables revenue generation.

## Scope
- One-time payments
- Monthly billing
- Receipts

---

## Issue #8 — 📊 EPIC 8 — Dashboard and Indicators

**Labels**
- `dashboard`
- `epic`
- `epic:dashboard`

**Description**
## Goal
Provide operational and financial visibility.

## Business Value
Supports management decision-making.

## Scope
- KPIs
- Charts
- Filters

---

## Issue #9 — 🔐 EPIC 9 — GDPR Compliance and Data Governance

**Labels**
- `audit-logs`
- `epic`
- `epic:gdpr-governance`
- `gdpr`

**Description**
## Goal
Ensure legal compliance and data governance.

## Business Value
Reduces legal risk and increases trust.

## Scope
- Anonymization
- Data export
- Retention

---

## Issue #10 — 🧩 User can register using email and password

**Labels**
- `auth`
- `backend`
- `db`
- `docs`
- `epic:foundation-multitenant`
- `frontend`
- `story`

**Description**
## Epic
- #1

## Context
New users must be able to access the platform without external identity providers.

## User Story
As a user  
I want to register using email and password  
So that I can access the platform securely.

## Acceptance Criteria
- User can submit email and password
- Email must be unique
- Password is stored securely (hashed)
- User receives confirmation of successful registration
- User can log in immediately after registration

## Notes
- Keep error messages clear and user-friendly
- Follow security best practices (rate limiting later if needed)

---

## Technical Tasks

### [Frontend]
- [ ] Create Register page (email + password + confirm password)
- [ ] Add form validation (required fields, email format, password rules)
- [ ] Handle API errors and display inline feedback
- [ ] Add success state (redirect to login or auto-login if token returned)

### [Backend]
- [ ] Define request/response contract for registration (DTO)
- [ ] Implement `POST /auth/register`
- [ ] Validate email uniqueness
- [ ] Validate password rules (min length, etc.)
- [ ] Hash password with bcrypt (or equivalent)
- [ ] Create user record and return auth token (or return success + require login)

### [DB]
- [ ] Ensure `users` table exists with unique index on email
- [ ] Add required fields (email, password_hash, created_at, etc.)
- [ ] Create migration if schema is missing/partial

### [Docs]
- [ ] Document `/auth/register` (request, response, error cases)

---

## Issue #11 — 🧩 System automatically creates a tenant when a manager registers

**Labels**
- `backend`
- `db`
- `epic:foundation-multitenant`
- `story`
- `tenant`

**Description**
## Epic
- #1

## Context

Each company using the platform must have its own isolated environment.

## User Story

As a manager  
I want a tenant to be created automatically when I register  
So that I can start using the platform without manual setup.

## Acceptance Criteria

- A new tenant is created upon manager registration
- The manager is associated with the tenant as an admin
- The tenant has a unique identifier
- All future data created by this manager is scoped to the tenant

## Notes

- This flow should not require manual admin intervention

## Technical Tasks

- [ ] Define Tenant entity/schema
- [ ] Create tenants table migration
- [ ] Associate user with tenant
- [ ] Mark registering user as tenant admin
- [ ] Enforce tenant_id on user creation
- [ ] Add transaction to ensure atomicity
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Create tenant-scoped service logic
- [ ] Enforce tenant isolation on all queries
- [ ] Validate permissions for tenant access

### [DB]

- [ ] Ensure tenants table and relations exist
- [ ] Add or verify tenant_id foreign keys and indexes

---

## Issue #12 — 🧩 Client can create an incident from a company link

**Labels**
- `backend`
- `db`
- `epic:incidents`
- `frontend`
- `incidents`
- `story`
- `tenant`

**Description**
## Epic
- #3

## Context

Clients may not have an account before requesting a service.

## User Story

As a client  
I want to create an incident using a company-specific link  
So that I can request a service easily.

## Acceptance Criteria

- Client can access the incident form via a company link
- Client must provide required contact information
- Incident is associated with the correct tenant
- Incident starts with status "Open"
- Client can view the incident after submission

## Notes

- The link must identify the tenant securely

## Technical Tasks

- [ ] Define Incident entity/schema
- [ ] Create incidents table migration
- [ ] Implement POST /incidents endpoint
- [ ] Validate tenant via company link
- [ ] Set default incident status
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Create tenant-scoped service logic
- [ ] Enforce tenant isolation on all queries
- [ ] Validate permissions for tenant access
- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC

### [DB]

- [ ] Ensure tenants table and relations exist
- [ ] Add or verify tenant_id foreign keys and indexes
- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #13 — 🧩 Manager can create a budget for an incident

**Labels**
- `backend`
- `budgets`
- `db`
- `epic:budget-approval`
- `frontend`
- `incidents`
- `story`

**Description**
As a manager, I want to define a budget for an incident
so that the client can approve it.

## Technical Tasks

- [ ] Define Budget entity/schema
- [ ] Create budgets table migration
- [ ] Implement POST /budgets endpoint
- [ ] Associate budget with incident
- [ ] Set default budget status
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC
- [ ] Implement budget creation and approval flow
- [ ] Associate budget with incident

### [DB]

- [ ] Create or update incidents table and relations
- [ ] Create budgets table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #16 — 🧩 Client can pay immediately after service completion

**Labels**
- `backend`
- `billing`
- `db`
- `docs`
- `epic:payments-billing`
- `infra`
- `payments`
- `story`

**Description**
## Epic
- #7

## Context
After a service is completed, the client should be able to pay immediately without additional manual steps or back-office intervention.

## User Story
As a client  
I want to pay immediately after the service is completed  
So that the service can be finalized without delays.

## Acceptance Criteria
- [ ] Payment option becomes available only after service completion
- [ ] Client can initiate payment from the service order
- [ ] Payment status is tracked (pending, paid, failed)
- [ ] Service order reflects the final payment status
- [ ] Errors during payment are handled gracefully

## Notes
- Payment flow must be tenant-scoped
- Initial implementation can support a single payment provider

---

## Technical Tasks

### [Backend]
- [ ] Validate that the service order is in a completed state before allowing payment
- [ ] Create payment initiation logic linked to a service order
- [ ] Integrate with the configured payment provider to create a payment intent
- [ ] Persist payment intent reference and initial status
- [ ] Handle payment confirmation callback (success)
- [ ] Handle payment failure callback and update status accordingly
- [ ] Emit domain event or audit log after payment confirmation

### [DB]
- [ ] Create payments table
- [ ] Store service_order_id, tenant_id, amount, currency, provider_reference, and status
- [ ] Add index for service_order_id lookup
- [ ] Add index for tenant_id to ensure tenant isolation

### [Frontend]
- [ ] Display payment action after service completion
- [ ] Show payment status (pending / success / failed)
- [ ] Handle loading and error states during payment process
- [ ] Provide user feedback on successful or failed payment

### [Infra]
- [ ] Configure payment provider credentials as environment variables
- [ ] Ensure webhook/callback endpoint is reachable and secure
- [ ] Validate webhook signature or provider security mechanism

### [Docs]
- [ ] Document payment flow lifecycle
- [ ] Document payment status transitions and failure scenarios

---

## Issue #17 — 🧩 Manager can view a dashboard with key indicators

**Labels**
- `backend`
- `dashboard`
- `epic:dashboard`
- `frontend`
- `story`

**Description**
Epic: Dashboard and Indicators

As a manager, I want to see KPIs
so that I can monitor performance.

---

## Technical Tasks

### [Backend]

- [ ] Support filtering and pagination in endpoints

### [Frontend]

- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---

## Issue #19 — 🧩 Manager can register employees for their company

**Labels**
- `backend`
- `db`
- `epic:user-permissions`
- `rbac`
- `story`
- `tenant`

**Description**
## Epic
- #2

## Context

Companies may have multiple employees accessing the platform.

## User Story

As a manager  
I want to register employees for my company  
So that they can access the system.

## Acceptance Criteria

- Manager can create a new employee user
- Employee is associated with the same tenant
- Employee receives login credentials or invitation
- Employee can access the platform after activation

## Notes

- Email must be unique across the platform

## Technical Tasks

### [Backend]
- [ ] Implement PATCH /budgets/:id/approve endpoint
- [ ] Validate client ownership
- [ ] Persist approval timestamp
- [ ] Update budget status to Approved
- [ ] Convert incident to service order
- [ ] Add audit log entry
- [ ] Implement budget creation and approval flow
- [ ] Associate budget with incident

### [DB]
- [ ] Create budgets table and relations

---

## Issue #20 — 🧩 Manager can assign permissions to employees

**Labels**
- `backend`
- `db`
- `epic:user-permissions`
- `rbac`
- `story`

**Description**
## Epic
- #2

## Context

Not all employees should have the same level of access.

## User Story

As a manager  
I want to assign permissions to employees  
So that access is controlled.

## Acceptance Criteria

- Manager can select a permission level or role
- Permissions affect visible features
- Changes take effect immediately
- Permission changes are logged

## Notes

- Prefer permission-based access over hard-coded roles

## Technical Tasks

### [Backend]
- [ ] Define permission model (roles vs permissions)
- [ ] Implement role-permission mapping logic
- [ ] Create endpoint to update an employee role/permissions
- [ ] Enforce RBAC middleware on protected routes
- [ ] Add audit log entry when permissions change

### [DB]
- [ ] Create permissions table or enum strategy (choose one)
- [ ] Create role_permissions mapping (table or relation)
- [ ] Ensure indexes for lookup (role_id / permission_id)

---

## Issue #21 — 🧩 Manager can edit or revoke employee access

**Labels**
- `backend`
- `epic:user-permissions`
- `rbac`
- `story`

**Description**
## Epic
- #2

## Context

Employees may change roles or leave the company.

## User Story

As a manager  
I want to edit or revoke employee access  
So that only authorized users can use the system.

## Acceptance Criteria

- Manager can deactivate an employee
- Deactivated users cannot log in
- Existing data is preserved
- Action is logged

## Notes

- Revocation should not delete historical records

## Technical Tasks

- [ ] Implement user deactivation flag
- [ ] Update access control middleware
- [ ] Block login for inactive users
- [ ] Add revoke access endpoint
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #22 — 🧩 Manager can manually register clients

**Labels**
- `backend`
- `db`
- `epic:user-permissions`
- `story`
- `tenant`

**Description**
## Epic
- #2

## Context
Some clients may be onboarded manually.

## User Story
As a manager  
I want to register clients manually  
So that they can access incident tracking.

## Acceptance Criteria
- Manager can create a client profile
- Client is linked to the tenant
- Client receives access instructions
- Client can view their incidents

## Notes
- Client data must follow uniqueness rules

## Technical Tasks

### [Backend]
- [ ] Create manual client registration endpoint
- [ ] Validate identity uniqueness rules
- [ ] Enforce manager-only access

### [DB]
- [ ] Ensure schema supports manual client creation
- [ ] Add required unique indexes

---

## Issue #23 — 🧩 Client maintains a single profile across multiple companies

**Labels**
- `backend`
- `db`
- `epic:user-permissions`
- `story`
- `tenant`

**Description**
## Epic
- #2

## Context
A client may request services from multiple companies.

## User Story
As a client  
I want to have a single profile across companies  
So that I don’t need multiple accounts.

## Acceptance Criteria
- Client profile is unique by CPF/CNPJ
- Client can be linked to multiple tenants
- Profile updates reflect across all tenants

## Notes
- Access rights must still be tenant-scoped

## Technical Tasks

### [Backend]
- [ ] Define global client identity rules
- [ ] Implement identity lookup and linking logic
- [ ] Ensure tenant scoping remains intact

### [DB]
- [ ] Create global client identity table
- [ ] Add uniqueness constraints and indexes

---

## Issue #24 — 🧩 Client can update email, phone number, or password

**Labels**
- `auth`
- `backend`
- `epic:user-permissions`
- `infra`
- `story`

**Description**
## Epic
- #2

## Context

Clients need to keep their contact information updated.

## User Story

As a client  
I want to update my personal information  
So that my data stays correct.

## Acceptance Criteria

- Client can edit email and phone
- Client can change password securely
- Changes are validated and saved
- Update actions are logged

## Notes

- Email updates may require reconfirmation

## Technical Tasks

- [ ] Create update profile endpoint
- [ ] Validate uniqueness on update
- [ ] Hash password updates securely
- [ ] Persist profile changes
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Emit notification events from domain logic

### [Infra]

- [ ] Configure email/notification provider
- [ ] Manage templates and environment variables

---

## Issue #25 — 🧩 System enforces unique CPF or CNPJ, email, and phone number

**Labels**
- `auth`
- `backend`
- `epic:user-permissions`
- `infra`
- `story`

**Description**
## Epic
- #2

## Context

Duplicate client records create inconsistencies.

## User Story

As the system  
I want to enforce unique client identifiers  
So that data remains consistent.

## Acceptance Criteria

- CPF/CNPJ must be unique
- Email must be unique
- Phone number must be unique
- Validation errors are clear

## Notes

- Uniqueness must be enforced at database level

## Technical Tasks

- [ ] Add unique DB constraints
- [ ] Add API-level validation
- [ ] Handle uniqueness violation errors

---

## Technical Tasks

### [Backend]

- [ ] Emit notification events from domain logic

### [Infra]

- [ ] Configure email/notification provider
- [ ] Manage templates and environment variables

---

## Issue #26 — 🧩 Client can attach images to an incident

**Labels**
- `backend`
- `db`
- `epic:incidents`
- `frontend`
- `incidents`
- `story`

**Description**
## Epic
- #3

## Context

Visual information helps diagnose issues faster.

## User Story

As a client  
I want to attach images to an incident  
So that the problem is clearly documented.

## Acceptance Criteria

- Client can upload one or more images
- Images are linked to the incident
- Supported formats are validated
- Upload errors are handled gracefully

## Notes

- Images may be stored externally (e.g. cloud storage)

## Technical Tasks

- [ ] Integrate file storage service
- [ ] Create incident_attachments table
- [ ] Validate file types and size
- [ ] Associate attachments with incident

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC

### [DB]

- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #27 — 🧩 Client can track incident status

**Labels**
- `backend`
- `db`
- `epic:incidents`
- `frontend`
- `incidents`
- `story`

**Description**
## Epic
- #3

## Context

Clients need visibility into service progress.

## User Story

As a client  
I want to track the status of my incident  
So that I know what is happening.

## Acceptance Criteria

- Client can see current status
- Status history is visible
- Status updates are real-time or near real-time

## Notes

- Status names should be user-friendly

## Technical Tasks

- [ ] Create GET /incidents/:id endpoint
- [ ] Implement status history tracking
- [ ] Ensure tenant-based access control

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC
- [ ] Support filtering and pagination in endpoints

### [DB]

- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states
- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---

## Issue #28 — 🧩 Client can cancel an incident that has not started

**Labels**
- `backend`
- `db`
- `epic:incidents`
- `frontend`
- `incidents`
- `story`

**Description**
## Epic
- #3

## Context

Clients may change their mind before service execution.

## User Story

As a client  
I want to cancel an incident that has not started  
So that unnecessary work is avoided.

## Acceptance Criteria

- Cancellation allowed only before execution
- Status changes to "Cancelled"
- Cancellation is logged

## Notes

- Cancelled incidents must remain visible

## Technical Tasks

- [ ] Define cancelable status rules
- [ ] Implement cancel endpoint
- [ ] Update incident status to Cancelled
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC

### [DB]

- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #29 — 🧩 Client can view a detailed budget

**Labels**
- `backend`
- `budgets`
- `db`
- `epic:budget-approval`
- `frontend`
- `story`

**Description**
## Context

Clients must understand what they are being charged for.

## User Story

As a client  
I want to view a detailed budget  
So that I understand the costs.

## Acceptance Criteria

- Budget shows itemized values
- Total amount is clearly visible
- Budget status is visible

## Notes

- Budget must be read-only for clients

## Technical Tasks

- [ ] Implement GET /budgets/:id endpoint
- [ ] Enforce client ownership validation
- [ ] Return read-only budget data

---

## Technical Tasks

### [Backend]

- [ ] Implement budget creation and approval flow
- [ ] Associate budget with incident

### [DB]

- [ ] Create budgets table and relations

### [Frontend]

- [ ] Build UI view aligned with the story requirements
- [ ] Handle loading, empty, and error states

---

## Issue #30 — 🧩 Client can reject a budget

**Labels**
- `backend`
- `budgets`
- `db`
- `epic:budget-approval`
- `story`

**Description**
## Context

Clients may disagree with the proposed budget.

## User Story

As a client  
I want to reject a budget  
So that the service is not executed.

## Acceptance Criteria

- Client can reject the budget
- Budget status changes to "Rejected"
- Incident does not become a service order
- Rejection reason can be recorded

## Notes

- Rejection must be logged

## Technical Tasks

- [ ] Implement PATCH /budgets/:id/reject endpoint
- [ ] Persist rejection reason
- [ ] Update budget status to Rejected
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Implement budget creation and approval flow
- [ ] Associate budget with incident

### [DB]

- [ ] Create budgets table and relations

---

## Issue #31 — 🧩 Manager is notified when a budget is approved or rejected

**Labels**
- `backend`
- `budgets`
- `db`
- `epic:budget-approval`
- `notifications`
- `story`

**Description**
## Context

Managers must act based on client decisions.

## User Story

As a manager  
I want to be notified when a budget is approved or rejected  
So that I can take action.

## Acceptance Criteria

- Manager receives notification
- Notification indicates decision clearly
- Notification is logged

## Notes

- Channel may evolve (email, system, WhatsApp)

## Technical Tasks

### [Backend]
- [ ] Emit budget decision event
- [ ] Create notification handler
- [ ] Persist notification record
- [ ] Implement budget creation and approval flow
- [ ] Associate budget with incident

### [DB]
- [ ] Create budgets table and relations

---

## Issue #32 — 🧩 System sends transactional emails automatically

**Labels**
- `backend`
- `epic:communication`
- `infra`
- `notifications`
- `story`

**Description**
## Context

Clients and managers must receive important updates without manual intervention.

## User Story

As the system  
I want to send transactional emails automatically  
So that users are informed about important events.

## Acceptance Criteria

- Emails are sent on relevant events (budget approval, service completion)
- Email content matches the event context
- Emails are sent to the correct recipients
- Email sending errors are logged

## Business Rules

- Emails must not be sent for cancelled incidents
- Email templates must be configurable

## Notes

- Email delivery should be asynchronous

## Technical Tasks

- [ ] Integrate email provider
- [ ] Define email templates
- [ ] Emit domain events
- [ ] Send emails asynchronously

---

## Technical Tasks

### [Backend]

- [ ] Emit notification events from domain logic

### [Infra]

- [ ] Configure email/notification provider
- [ ] Manage templates and environment variables

---

## Issue #33 — 🧩 Client receives notifications on service status updates

**Labels**
- `backend`
- `epic:communication`
- `infra`
- `notifications`
- `story`

**Description**
## Context

Clients need visibility into service progress.

## User Story

As a client  
I want to receive notifications when the service status changes  
So that I stay informed.

## Acceptance Criteria

- Client receives notification when status changes
- Notification includes new status and timestamp
- Notification delivery is logged

## Notes

- Channel may vary (email, WhatsApp)

## Technical Tasks

- [ ] Create notification dispatcher
- [ ] Subscribe to status change events

---

## Technical Tasks

### [Backend]

- [ ] Emit notification events from domain logic

### [Infra]

- [ ] Configure email/notification provider
- [ ] Manage templates and environment variables

---

## Issue #34 — 🧩 Client receives notifications via WhatsApp

**Labels**
- `backend`
- `epic:communication`
- `infra`
- `notifications`
- `story`
- `whatsapp`

**Description**
## Context

WhatsApp is a preferred communication channel for many clients.

## User Story

As a client  
I want to receive notifications via WhatsApp  
So that communication is faster and more convenient.

## Acceptance Criteria

- WhatsApp messages are sent on relevant events
- Messages include incident or service reference
- Message delivery status is tracked

## Business Rules

- Client must opt-in to WhatsApp notifications
- Messages must follow WhatsApp API policies

## Notes

- Fallback to email if WhatsApp delivery fails

## Technical Tasks

- [ ] Integrate WhatsApp Business API
- [ ] Implement message templates
- [ ] Handle delivery status

---

## Technical Tasks

### [Backend]

- [ ] Emit notification events from domain logic

### [Infra]

- [ ] Configure email/notification provider
- [ ] Manage templates and environment variables

---

## Issue #35 — 🧩 System creates incidents from WhatsApp messages

**Labels**
- `backend`
- `db`
- `epic:communication`
- `frontend`
- `incidents`
- `story`
- `whatsapp`

**Description**
## Context

Some clients prefer initiating requests via WhatsApp.

## User Story

As the system  
I want to create incidents from WhatsApp messages  
So that clients can request services without accessing the web app.

## Acceptance Criteria

- Incoming WhatsApp messages can create incidents
- Incident is linked to the correct client and tenant
- Client receives confirmation of incident creation

## Business Rules

- Only recognized numbers can create incidents
- Manual review may be required before execution

## Notes

- Message parsing should be resilient to free text

## Technical Tasks

- [ ] Implement webhook endpoint
- [ ] Parse inbound messages
- [ ] Map message to incident creation

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC

### [DB]

- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #36 — 🧩 Manager can respond to clients via integrated WhatsApp

**Labels**
- `backend`
- `epic:communication`
- `infra`
- `story`
- `whatsapp`

**Description**
## Context
Managers need to communicate directly with clients.

## User Story
As a manager  
I want to respond to clients via WhatsApp from the platform  
So that all communication is centralized.

## Acceptance Criteria
- Manager can send WhatsApp messages from the platform
- Messages are linked to incidents or service orders
- Message history is stored and visible

## Business Rules
- Messages must be tenant-scoped
- WhatsApp templates must be used when required

## Notes
- Avoid exposing personal phone numbers

## Technical Tasks

### [Backend]
- [ ] Implement WhatsApp message sending service
- [ ] Enforce tenant scoping
- [ ] Log communication events

### [Infra]
- [ ] Configure WhatsApp provider credentials
- [ ] Configure webhook callbacks

---

## Issue #37 — 🧩 One-time clients can pay immediately after service completion

**Labels**
- `backend`
- `billing`
- `db`
- `epic:payments-billing`
- `infra`
- `payments`
- `story`

**Description**
## Epic
- #7

## Context
Some clients pay per service.

## User Story
As a one-time client  
I want to pay immediately after service completion  
So that the service is closed without delays.

## Acceptance Criteria
- Payment link is generated after service completion
- Client can complete payment online
- Payment status updates automatically
- Receipt is generated after payment

## Business Rules
- Payment must be completed before service is fully closed

## Notes
- Integration may use Stripe or Mercado Pago

## Technical Tasks

### [Backend]
- [ ] Validate service order completion before payment
- [ ] Create payment intent with provider
- [ ] Persist payment reference and status
- [ ] Handle payment callbacks

### [DB]
- [ ] Create payments table
- [ ] Add indexes for service_order_id and tenant_id

### [Infra]
- [ ] Configure payment provider credentials
- [ ] Configure webhook endpoint and validation

---

## Issue #38 — 🧩 System generates charges automatically after service completion

**Labels**
- `backend`
- `billing`
- `epic:payments-billing`
- `payments`
- `story`

**Description**
## Epic
- #7

## Context

Manual billing is error-prone.

## User Story

As the system  
I want to generate charges automatically after service completion  
So that billing is consistent and reliable.

## Acceptance Criteria

- Charge is generated upon service completion
- Charge amount matches approved budget
- Charge is linked to service order

## Notes

- Charges must be auditable

## Technical Tasks

- [ ] Emit service completion event
- [ ] Generate charge record

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #39 — 🧩 Plan clients can accumulate services into a monthly invoice

**Labels**
- `backend`
- `billing`
- `db`
- `epic:payments-billing`
- `story`

**Description**
## Epic
- #7

## Context
Some clients operate under a monthly billing plan.

## User Story
As a plan client  
I want services to be accumulated into a monthly invoice  
So that I can pay in a single transaction.

## Acceptance Criteria
- Services are grouped by billing period
- Invoice total reflects all completed services
- Invoice can be reviewed before payment

## Business Rules
- Only completed services are invoiced

## Notes
- Invoicing period must be configurable

## Technical Tasks

### [Backend]
- [ ] Implement monthly invoice aggregation
- [ ] Attach service orders to invoices
- [ ] Generate invoice totals
- [ ] Expose invoice summary endpoints

### [DB]
- [ ] Create invoices and invoice_items tables
- [ ] Add indexes for tenant and client lookup

---

## Issue #40 — 🧩 Manager can view pending and completed payments

**Labels**
- `backend`
- `billing`
- `db`
- `epic:payments-billing`
- `frontend`
- `payments`
- `story`

**Description**
## Epic
- #7

## Context

Managers need financial visibility.

## User Story

As a manager  
I want to view pending and completed payments  
So that I can track revenue.

## Acceptance Criteria

- Manager can see payment status per service or invoice
- Filters by date and status are available

## Notes

- Access restricted to authorized users

## Technical Tasks

- [ ] Implement GET /payments endpoint
- [ ] Filter by status

---

## Technical Tasks

### [Backend]

- [ ] Aggregate billing data per tenant and period
- [ ] Expose billing/reporting endpoints

### [DB]

- [ ] Ensure billing-related tables and indexes

### [Frontend]

- [ ] Build billing or revenue dashboard view
- [ ] Render charts or summaries from API data

---

## Issue #41 — 🧩 Client can view payment history

**Labels**
- `backend`
- `billing`
- `db`
- `epic:payments-billing`
- `frontend`
- `payments`
- `story`

**Description**
## Epic
- #7

## Context

Clients may need proof of past payments.

## User Story

As a client  
I want to view my payment history  
So that I can review past transactions.

## Acceptance Criteria

- Client can see list of past payments
- Each payment shows amount, date, and status

## Notes

- Payment data must be read-only

## Technical Tasks

- [ ] Implement GET /payments/history endpoint

---

## Technical Tasks

### [Backend]

- [ ] Aggregate billing data per tenant and period
- [ ] Expose billing/reporting endpoints

### [DB]

- [ ] Ensure billing-related tables and indexes

### [Frontend]

- [ ] Build billing or revenue dashboard view
- [ ] Render charts or summaries from API data

---

## Issue #42 — 🧩 Client can download payment receipts

**Labels**
- `backend`
- `billing`
- `db`
- `epic:payments-billing`
- `frontend`
- `payments`
- `story`

**Description**
## Epic
- #7

## Context

Receipts may be required for accounting.

## User Story

As a client  
I want to download payment receipts  
So that I can keep financial records.

## Acceptance Criteria

- Receipt is available after successful payment
- Receipt includes service and payment details
- Receipt can be downloaded as PDF

## Notes

- Receipt format should be standardized

## Technical Tasks

- [ ] Generate receipt PDF
- [ ] Store receipt securely

---

## Technical Tasks

### [Backend]

- [ ] Aggregate billing data per tenant and period
- [ ] Expose billing/reporting endpoints

### [DB]

- [ ] Ensure billing-related tables and indexes

### [Frontend]

- [ ] Build billing or revenue dashboard view
- [ ] Render charts or summaries from API data

---

## Issue #43 — 🧩 Manager can view a dashboard with key indicators

**Labels**
- `backend`
- `dashboard`
- `epic:dashboard`
- `frontend`
- `story`

**Description**
## Context

Managers need a high-level overview.

## User Story

As a manager  
I want to see a dashboard with key indicators  
So that I can quickly understand system performance.

## Acceptance Criteria

- Dashboard shows incidents, service orders, and revenue
- Indicators are updated regularly
- Data is tenant-specific

## Notes

- Mobile-first layout

## Technical Tasks

### [Backend]
- [ ] Define KPI queries
- [ ] Create dashboard API endpoint
- [ ] Support filtering and pagination in endpoints

### [Frontend]
- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---

## Issue #44 — 🧩 Manager can view incident counts by status

**Labels**
- `backend`
- `dashboard`
- `db`
- `epic:dashboard`
- `frontend`
- `incidents`
- `story`

**Description**
## Context

Status distribution reveals bottlenecks.

## User Story

As a manager  
I want to see incident counts by status  
So that I can identify operational issues.

## Acceptance Criteria

- Incidents grouped by status
- Counts reflect selected time period

## Notes

- Chart visualization recommended

## Technical Tasks

- [ ] Aggregate incident status data

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC

### [DB]

- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #45 — 🧩 Manager can view ongoing service orders

**Labels**
- `backend`
- `dashboard`
- `epic:dashboard`
- `frontend`
- `service-orders`
- `story`

**Description**
## Context

Active services require monitoring.

## User Story

As a manager  
I want to see ongoing service orders  
So that I can manage execution.

## Acceptance Criteria

- List of active service orders
- Each item shows current status and responsible employee

## Notes

- Sorting by priority is recommended

## Technical Tasks

- [ ] Query active service orders

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

### [Frontend]

- [ ] Build UI view aligned with the story requirements
- [ ] Handle loading, empty, and error states

---

## Issue #46 — 🧩 Manager can track monthly revenue

**Labels**
- `backend`
- `billing`
- `dashboard`
- `db`
- `epic:dashboard`
- `frontend`
- `story`

**Description**
## Context

Revenue tracking supports planning.

## User Story

As a manager  
I want to track monthly revenue  
So that I can evaluate business performance.

## Acceptance Criteria

- Revenue aggregated by month
- Filters by period available

## Notes

- Graph visualization recommended

---

## Technical Tasks

### [Backend]

- [ ] Aggregate billing data per tenant and period
- [ ] Expose billing/reporting endpoints
- [ ] Support filtering and pagination in endpoints

### [DB]

- [ ] Ensure billing-related tables and indexes

### [Frontend]

- [ ] Build billing or revenue dashboard view
- [ ] Render charts or summaries from API data
- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---

## Issue #47 — 🧩 Manager can filter indicators by period

**Labels**
- `backend`
- `dashboard`
- `epic:dashboard`
- `frontend`
- `story`

**Description**
## Context

Managers need flexible analysis.

## User Story

As a manager  
I want to filter dashboard indicators by period  
So that I can analyze trends.

## Acceptance Criteria

- Date range selector available
- All indicators update accordingly

## Notes

- Default period should be current month

---

## Technical Tasks

### [Backend]

- [ ] Support filtering and pagination in endpoints

### [Frontend]

- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---

## Issue #48 — 🧩 Administrator can anonymize client data

**Labels**
- `backend`
- `epic:gdpr-governance`
- `gdpr`
- `story`

**Description**
## Epic
- #9

## Context

Clients may request data anonymization.

## User Story

As an administrator  
I want to anonymize client data  
So that legal requirements are met.

## Acceptance Criteria

- Identifiable fields are anonymized
- Operational data remains intact
- Action is irreversible

## Notes

- Must comply with GDPR rules

## Technical Tasks

- [ ] Identify PII fields
- [ ] Implement anonymization service
- [ ] Add audit log entry

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #49 — 🧩 Client can request data anonymization or deletion

**Labels**
- `backend`
- `epic:gdpr-governance`
- `gdpr`
- `story`

**Description**
## Epic
- #9

## Context

Clients have rights over their personal data.

## User Story

As a client  
I want to request anonymization or deletion of my data  
So that my privacy rights are respected.

## Acceptance Criteria

- Client can submit a request
- Request status is trackable
- Administrator is notified

## Notes

- Some data may be legally retained

## Technical Tasks

- [ ] Create data request endpoint
- [ ] Persist request status

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #50 — 🧩 Manager can export client data

**Labels**
- `backend`
- `epic:gdpr-governance`
- `gdpr`
- `story`

**Description**
## Epic
- #9

## Context

Data portability is a legal requirement.

## User Story

As a manager  
I want to export client data  
So that it can be provided upon request.

## Acceptance Criteria

- Export includes client-related data
- Export format is readable
- Export action is logged

## Notes

- Export scope must be tenant-limited

## Technical Tasks

- [ ] Aggregate client data
- [ ] Export as structured file

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #51 — 🧩 System maintains full audit trails

**Labels**
- `audit-logs`
- `backend`
- `epic:gdpr-governance`
- `gdpr`
- `story`

**Description**
## Epic
- #9

## Context

Auditing is required for security and compliance.

## User Story

As the system  
I want to maintain full audit trails  
So that actions are traceable.

## Acceptance Criteria

- All critical actions are logged
- Logs include user, action, and timestamp
- Logs are immutable

## Notes

- Logs should be queryable

## Technical Tasks

- [ ] Enforce audit logging consistency
- [ ] Validate coverage across modules

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #52 — 🧩 System applies configurable data retention policies

**Labels**
- `backend`
- `epic:gdpr-governance`
- `gdpr`
- `story`

**Description**
## Epic
- #9

## Context

Data should not be retained indefinitely.

## User Story

As the system  
I want to apply data retention policies  
So that stored data complies with regulations.

## Acceptance Criteria

- Retention rules are configurable
- Expired data is anonymized or removed
- Retention actions are logged

## Notes

- Retention rules may vary by data type

## Technical Tasks

- [ ] Define retention rules
- [ ] Schedule retention jobs

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

---

## Issue #53 — 🧩 Manager can view all open service orders

**Labels**
- `backend`
- `epic:service-order-execution`
- `frontend`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context
Managers need visibility over ongoing work to coordinate execution.

## User Story
As a manager  
I want to view all open service orders  
So that I can manage execution and workload.

## Acceptance Criteria
- Manager can access a list of service orders in statuses: Open, In Progress, Waiting Client
- Each row shows: Service Order ID, Client name, Status, Assigned employee(s), Updated date
- List is tenant-scoped (only orders from the manager’s company)
- Sorting is available by updated date (default: most recent)

## Notes
- Keep the list mobile-friendly (responsive layout)

## Technical Tasks

### [Backend]
- [ ] Create endpoint to list open service orders
- [ ] Support pagination and filtering
- [ ] Enforce RBAC visibility rules

### [Frontend]
- [ ] Build open service orders list page
- [ ] Add loading, empty, and error states

---

## Issue #54 — 🧩 Manager can view service order details

**Labels**
- `backend`
- `epic:service-order-execution`
- `frontend`
- `incidents`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context

Managers need full detail to execute correctly and avoid errors.

## User Story

As a manager  
I want to view service order details  
So that I understand what needs to be done.

## Acceptance Criteria

- Detail page shows: client contact, incident description, approved budget summary, attachments
- Shows current status and status history
- Shows assigned employee(s)
- Shows execution notes and evidence section
- Tenant-scoped access enforced

## Notes

- The budget must be read-only here (already approved)

## Technical Tasks

- [ ] Implement GET /service-orders/:id endpoint
- [ ] Aggregate related incident and budget data

---

## Technical Tasks

### [Backend]

- [ ] Implement core business logic for this story
- [ ] Expose required API endpoints with validation

### [Frontend]

- [ ] Build UI view aligned with the story requirements
- [ ] Handle loading, empty, and error states

---

## Issue #55 — 🧩 Manager can assign employees to a service order

**Labels**
- `audit-logs`
- `backend`
- `db`
- `epic:service-order-execution`
- `rbac`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context
Service execution is typically delegated to employees or technicians.

## User Story
As a manager  
I want to assign employees to a service order  
So that responsibilities are clear.

## Acceptance Criteria
- Manager can assign one or more employees to a service order
- Assigned employees appear in the service order list and details
- Assignment updates are saved with timestamp
- Assignment action is recorded in audit logs (who/when/what)

## Business Rules
- Only users with permission can assign
- Only employees from the same tenant can be assigned

## Technical Tasks

### [Backend]
- [ ] Implement assign/unassign employee endpoints
- [ ] Validate employee belongs to tenant
- [ ] Enforce manager-only assignment permissions

### [DB]
- [ ] Create service_order_assignments table
- [ ] Add indexes for employee_id and service_order_id

---

## Issue #56 — 🧩 Employee can view assigned service orders

**Labels**
- `backend`
- `epic:service-order-execution`
- `frontend`
- `rbac`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context
Employees need a clear queue of work assigned to them.

## User Story
As an employee  
I want to view service orders assigned to me  
So that I know what I must work on.

## Acceptance Criteria
- Employee can see a list of only their assigned service orders
- Each row shows: Service Order ID, Client name, Status, Updated date
- Employee cannot view service orders not assigned to them (unless permission allows)

## Notes
- Mobile-first list view is required

## Technical Tasks

### [Backend]
- [ ] Add endpoint to list service orders assigned to the authenticated employee (tenant-scoped)
- [ ] Support pagination and sorting
- [ ] Enforce RBAC so employees see only their assigned orders
- [ ] Return minimal fields needed for list rendering

### [Frontend]
- [ ] Build “My Assigned Orders” list view
- [ ] Add loading, empty, and error states
- [ ] Add basic filters and sorting
- [ ] Link items to service order details

---

## Issue #57 — 🧩 Manager can update service order status

**Labels**
- `audit-logs`
- `backend`
- `epic:service-order-execution`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context

Work progresses through stages and needs to be tracked.

## User Story

As a manager  
I want to update the service order status  
So that progress is accurately reflected.

## Acceptance Criteria

- Status can be changed among: Open, In Progress, Waiting Client, Completed, Cancelled
- Status change requires confirmation
- Each status change is recorded in status history with timestamp
- Status change action is recorded in audit logs

## Business Rules

- Completed orders become read-only (except receipt/payment fields later)
- Cancelled orders cannot be marked Completed

## Technical Tasks

### [Backend]
- [ ] Implement PATCH /service-orders/:id/status endpoint
- [ ] Validate allowed status transitions
- [ ] Persist status history
- [ ] Add audit log entry

---

## Issue #58 — 🧩 Manager can add execution notes to a service order

**Labels**
- `audit-logs`
- `backend`
- `db`
- `epic:service-order-execution`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context
Execution details need to be documented for transparency and internal control.

## User Story
As a manager  
I want to add execution notes  
So that service details are recorded.

## Acceptance Criteria
- Manager can add notes with free text
- Notes are timestamped and show author identity
- Notes are visible in the service order details
- Adding a note is recorded in audit logs

## Business Rules
- Notes cannot be edited after the service order is Completed

## Technical Tasks

### [Backend]
- [ ] Add endpoint to create execution notes for service orders
- [ ] Enforce RBAC rules for note creation
- [ ] Add endpoint to list execution notes

### [DB]
- [ ] Create service_order_notes table
- [ ] Add indexes for service_order_id and tenant_id

---

## Issue #59 — 🧩 Manager can attach evidence to a service order

**Labels**
- `audit-logs`
- `backend`
- `db`
- `epic:service-order-execution`
- `infra`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context
Some services require proof of work (before/after photos, documents).

## User Story
As a manager  
I want to attach evidence to a service order  
So that completion is documented.

## Acceptance Criteria
- Manager can upload one or more images/files as evidence
- Evidence is visible in the service order details
- Upload success/failure is shown to the user
- Evidence upload is recorded in audit logs

## Notes
- Evidence storage can use external provider

## Technical Tasks

### [Backend]
- [ ] Create endpoint to upload evidence for a service order
- [ ] Validate file type, size, and tenant ownership
- [ ] Persist evidence metadata linked to service order
- [ ] Create endpoint to list and download evidence

### [DB]
- [ ] Create service_order_evidence table
- [ ] Add indexes for service_order_id and tenant_id

### [Infra]
- [ ] Configure object storage and credentials
- [ ] Define access strategy (private or signed URLs)

---

## Issue #60 — 🧩 Manager can finalize a service order

**Labels**
- `audit-logs`
- `backend`
- `epic:service-order-execution`
- `notifications`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context

Finalizing a service order closes execution and triggers the next steps (billing and reporting).

## User Story

As a manager  
I want to finalize a service order  
So that it can be closed and billed.

## Acceptance Criteria

- Manager can finalize only if status is not Cancelled
- Finalization sets status to Completed and records completion date
- Service order becomes read-only (except billing integration later)
- Client notification event is triggered (channel handled in Sprint 5)
- Finalization action is recorded in audit logs

## Business Rules

- Finalization can happen only once
- Completed orders cannot return to In Progress

## Technical Tasks

### [Backend]
- [ ] Implement finalize endpoint
- [ ] Lock service order for changes
- [ ] Emit completion event
- [ ] Add audit log entry

---

## Issue #61 — 🧩 Client can approve a budget

**Labels**
- `audit-logs`
- `backend`
- `budgets`
- `db`
- `epic:budget-approval`
- `story`

**Description**
## Context

Before a service can be executed, the client must explicitly approve the proposed budget.
This approval represents a formal agreement between client and service provider.

## User Story

As a client  
I want to approve a budget  
So that the service can be executed under the agreed conditions.

## Acceptance Criteria

- Client can view full budget details (items, quantities, prices, total)
- Client can explicitly approve the budget
- Budget status changes from "Pending" to "Approved"
- Approval date and client identifier are recorded
- Approved budget becomes read-only
- Related incident is automatically converted into a service order
- Client receives confirmation of approval

## Business Rules

- A budget can only be approved once
- Only the client associated with the incident can approve the budget
- Approved budgets cannot be edited or deleted

## Audit & Compliance

- Budget approval action must be logged
- Log must contain user, timestamp, and action type

## Notes

- Approval should require explicit confirmation (prevent accidental clicks)

## Technical Tasks

### [Backend]
- [ ] Implement PATCH /budgets/:id/approve endpoint
- [ ] Validate client ownership
- [ ] Persist approval timestamp
- [ ] Update budget status to Approved
- [ ] Convert incident to service order
- [ ] Add audit log entry
- [ ] Implement budget creation and approval flow
- [ ] Associate budget with incident

### [DB]
- [ ] Create budgets table and relations

---

## Issue #62 — 🧩 Manager can customize dashboard widgets

**Labels**
- `backend`
- `dashboard`
- `db`
- `epic:dashboard`
- `frontend`
- `story`

**Description**
## Context
Different managers focus on different KPIs depending on their operation.

## User Story
As a manager  
I want to customize dashboard widgets  
So that I can focus on the indicators most relevant to me.

## Acceptance Criteria
- Manager can enable or disable dashboard widgets
- Widget order can be rearranged
- Widget configuration is persisted per user
- Default dashboard layout exists for new users
- Changes are applied immediately

## Business Rules
- Customization is user-specific (not global)
- Only available widgets can be selected

## Notes
- Drag-and-drop is optional for MVP
- Mobile-first layout must be respected

## Technical Tasks

### [Backend]
- [ ] Add endpoints to save and load dashboard layouts
- [ ] Validate layout schema

### [DB]
- [ ] Create dashboard_layouts table
- [ ] Add unique constraint for tenant_id and user_id

---

## Issue #63 — 🧩 System logs all critical actions across modules

**Labels**
- `audit-logs`
- `backend`
- `db`
- `epic:foundation-multitenant`
- `gdpr`
- `story`

**Description**
## Epic
- #1

## Context
Security, compliance, and traceability require consistent auditing across the system.

## User Story
As the system  
I want to log all critical actions across modules  
So that activities are traceable for security and compliance purposes.

## Acceptance Criteria
- Critical actions are logged consistently across all modules
- Log entry includes: user, tenant, action type, entity, timestamp
- Logs are immutable (cannot be edited or deleted)
- Logs are stored securely and efficiently
- Logs can be queried by authorized users

## Critical Actions (Minimum)
- Authentication (login, logout)
- Permission changes
- Incident creation and cancellation
- Budget approval and rejection
- Service order status changes
- Payment confirmation
- Data anonymization or deletion

## Business Rules
- Logs must be tenant-scoped
- Only authorized roles can view logs

## Notes
- Logging should be asynchronous to avoid performance impact

## Technical Tasks

### [Backend]
- [ ] Implement centralized audit logging service
- [ ] Define audit event schema
- [ ] Hook audit logs into critical actions
- [ ] Add endpoint to query audit logs

### [DB]
- [ ] Create audit_logs table
- [ ] Add indexes for tenant_id and timestamp

---

## Issue #64 — 🧩 System enforces valid status transitions

**Labels**
- `audit-logs`
- `backend`
- `epic:service-order-execution`
- `incidents`
- `service-orders`
- `story`

**Description**
## Epic
- #5

## Context

Allowing arbitrary status changes leads to inconsistent states and operational errors.

## User Story

As the system  
I want to enforce valid status transitions  
So that incidents and service orders always follow a valid lifecycle.

## Acceptance Criteria

- Status transitions follow a predefined state machine
- Invalid transitions are blocked
- User receives a clear error message when a transition is invalid
- All valid transitions are logged

## Incident Status Flow

- Open → Budget Pending
- Budget Pending → Approved
- Approved → Converted to Service Order
- Open → Cancelled

## Service Order Status Flow

- Open → In Progress
- In Progress → Waiting Client
- Waiting Client → In Progress
- In Progress → Completed
- Open → Cancelled

## Business Rules

- Completed or Cancelled entities cannot transition further
- Transition rules must be centralized (single source of truth)

## Notes

- State machine should be extensible for future statuses

## Technical Tasks

### [Backend]
- [ ] Define status enums for incidents and service orders
- [ ] Implement centralized state machine module
- [ ] Block invalid transitions
- [ ] Return descriptive errors

---

## Issue #65 — Idea: the incident can be created without an company, so any company can take the incident.

**Labels**
- `backend`
- `db`
- `frontend`
- `incidents`
- `story`
- `tenant`

**Description**
See title for story context.

---

## Technical Tasks

### [Backend]

- [ ] Create tenant-scoped service logic
- [ ] Enforce tenant isolation on all queries
- [ ] Validate permissions for tenant access
- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC

### [DB]

- [ ] Ensure tenants table and relations exist
- [ ] Add or verify tenant_id foreign keys and indexes
- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states

---

## Issue #66 — Idea: there should be a page with the incidents for the companies to check

**Labels**
- `backend`
- `db`
- `frontend`
- `incidents`
- `story`

**Description**
See title for story context.

---

## Technical Tasks

### [Backend]

- [ ] Implement incident lifecycle logic
- [ ] Expose incident endpoints with RBAC
- [ ] Support filtering and pagination in endpoints

### [DB]

- [ ] Create or update incidents table and relations

### [Frontend]

- [ ] Build incident form or list view
- [ ] Handle submission, loading, and error states
- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---

## Issue #67 — Idea: there should be a page listing all the companies

**Labels**
- `backend`
- `frontend`
- `story`

**Description**
See title for story context.

---

## Technical Tasks

### [Backend]

- [ ] Support filtering and pagination in endpoints

### [Frontend]

- [ ] Build dedicated page or dashboard widget
- [ ] Implement filters or selectors required by the story
- [ ] Integrate UI with backend endpoints

---
