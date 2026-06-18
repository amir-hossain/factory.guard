# Feature Specification: Incident Tracking System

**Feature Branch**: `main`

**Created**: 2026-06-18

**Status**: Draft

**Input**: User description: "Build a complete Incident Tracking System (FactoryGuard) for a garment manufacturing factory to centralize incident reporting, root cause analysis, corrective actions, escalations, analytics, and role-based access."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Report and Track Incidents (Priority: P1)

A factory worker can report a machine breakdown, quality issue, safety incident, or compliance finding from one central place, attach supporting images, classify the incident, and later see the status of incidents they reported.

**Why this priority**: Centralized incident capture is the core business need and replaces scattered WhatsApp, Excel, phone, and email tracking.

**Independent Test**: Can be fully tested by creating an incident as a worker with category, severity, department, section, description, and images, then verifying the worker can see only their own submitted incident and its status.

**Acceptance Scenarios**:

1. **Given** a worker is signed in, **When** they submit an incident with required details and images, **Then** the incident is created with an Open status and visible to that worker.
2. **Given** a worker has submitted multiple incidents, **When** they view their incident list, **Then** only incidents created by that worker are shown with current status and key details.
3. **Given** a worker submits an incident without required classification details, **When** they attempt to save it, **Then** they receive clear guidance about missing information and the incomplete incident is not submitted.

---

### User Story 2 - Investigate and Assign Corrective Actions (Priority: P1)

A supervisor can view all incidents, assign or update root cause details, create one or more corrective actions, assign action owners, set due dates, and track each action's completion progress.

**Why this priority**: Incident reports only create value when supervisors can drive investigation and resolution through accountable follow-up work.

**Independent Test**: Can be fully tested by creating an incident as a worker, signing in as a supervisor, assigning a root cause, creating multiple corrective actions, updating completion percentages, and verifying the incident reflects action progress.

**Acceptance Scenarios**:

1. **Given** a supervisor is viewing an open incident, **When** they add root cause findings and corrective actions with owners and due dates, **Then** the incident displays the investigation details and all linked actions.
2. **Given** a corrective action is partially complete, **When** the assigned owner updates its completion percentage, **Then** the action and parent incident show the updated progress.
3. **Given** an incident has multiple corrective actions, **When** one action is completed, **Then** the remaining actions continue to be tracked independently.

---

### User Story 3 - Escalate Urgent and Overdue Work (Priority: P2)

The system automatically escalates high-severity incidents and overdue corrective actions to the appropriate supervisors or managers, making urgent work visible without relying on manual follow-up.

**Why this priority**: Escalation reduces resolution delays for safety, production, quality, and compliance risks.

**Independent Test**: Can be fully tested by creating a high-severity incident and an overdue action, then verifying both are flagged and the intended supervisor or manager receives a notification.

**Acceptance Scenarios**:

1. **Given** a high-severity incident is reported, **When** it is saved, **Then** it is flagged for escalation and the responsible supervisor or manager is notified.
2. **Given** a corrective action passes its due date without completion, **When** overdue work is evaluated, **Then** the action is marked overdue and the responsible supervisor is notified.
3. **Given** an escalated incident requires manager approval to close, **When** a supervisor attempts closure, **Then** the incident remains pending approval until a manager approves or rejects it.

---

### User Story 4 - Manage Operational Configuration and Users (Priority: P2)

A manager can manage users, assign roles, configure incident categories, configure severity levels, maintain factory departments and sections, and define escalation rules.

**Why this priority**: The factory needs controlled administration so the incident system stays aligned with changing factory structure and operating policies.

**Independent Test**: Can be fully tested by signing in as a manager, creating a category and factory section, assigning a user role, configuring an escalation rule, and verifying those values are available in incident workflows.

**Acceptance Scenarios**:

1. **Given** a manager adds a new incident category, **When** a user reports an incident, **Then** the new category is available for selection.
2. **Given** a manager changes a user's role, **When** that user next accesses the system, **Then** their visible actions and incident access match the new role.
3. **Given** a manager configures escalation timing for a severity level, **When** matching incidents or actions meet that rule, **Then** escalation follows the configured policy.

---

### User Story 5 - Monitor Incident Trends (Priority: P3)

Supervisors and managers can view dashboards showing open incident count, closure trends, average resolution time, and incidents by department to identify recurring problems and improvement opportunities.

**Why this priority**: Analytics turn the centralized incident history into operational insight after capture and resolution workflows are in place.

**Independent Test**: Can be fully tested by loading sample incidents across statuses, departments, severities, and closure dates, then verifying dashboard metrics match the underlying records.

**Acceptance Scenarios**:

1. **Given** incidents exist across multiple departments, **When** an authorized user views the dashboard, **Then** incident counts by department are displayed accurately.
2. **Given** incidents have status-change history, **When** closure rate and average resolution time are shown, **Then** the metrics are calculated from the recorded history.
3. **Given** a worker attempts to access system-wide analytics, **When** their permissions are checked, **Then** they are denied access.

---

### Edge Cases

- What happens when an image upload fails while the incident details are otherwise valid?
- What happens when an incident category, severity level, department, or section is deactivated while existing incidents still reference it?
- How does the system handle a corrective action owner whose role or employment status changes before the action is complete?
- What happens when a supervisor and manager attempt conflicting status changes on the same incident?
- How are duplicate incident reports from multiple workers for the same event identified or handled?
- What happens when escalation rules change while incidents are already open or actions are already overdue?
- How does the system preserve audit and status history if an incident is reassigned, reopened, or rejected during closure approval?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow authenticated workers to create incident reports with description, category, severity, factory department or section, occurrence date and time, reporter identity, and optional supporting notes.
- **FR-002**: System MUST allow incident reporters to attach one or more images to an incident report.
- **FR-003**: System MUST validate that every submitted incident has the required classification, location, severity, and description fields before it is accepted.
- **FR-004**: System MUST assign every new incident an Open status at creation.
- **FR-005**: System MUST support an incident status workflow from Open through active resolution states to Closed.
- **FR-006**: System MUST record a full status-change history for every incident, including previous status, new status, who changed it, when it changed, and any required reason or comment.
- **FR-007**: Workers MUST be able to view only incidents they created.
- **FR-008**: Supervisors MUST be able to view all incidents.
- **FR-009**: Supervisors MUST be able to record root cause information for any incident.
- **FR-010**: Supervisors MUST be able to create multiple corrective actions for an incident.
- **FR-011**: Each corrective action MUST include an owner, due date, status, completion percentage, and relationship to its incident.
- **FR-012**: Corrective action completion percentage MUST be constrained to values from 0% through 100%.
- **FR-013**: System MUST allow corrective actions to be updated independently while preserving their relationship to the parent incident.
- **FR-014**: System MUST identify overdue corrective actions based on due date and completion status.
- **FR-015**: System MUST automatically flag high-severity incidents for escalation according to configured rules.
- **FR-016**: System MUST notify the responsible supervisor when an assigned incident or corrective action requires attention.
- **FR-017**: System MUST notify the responsible manager when escalation rules require manager attention or approval.
- **FR-018**: System MUST support manager approval before closure for incidents that meet configured approval criteria.
- **FR-019**: Managers MUST be able to approve or reject closure requests and provide comments.
- **FR-020**: Managers MUST be able to manage user accounts and role assignments.
- **FR-021**: Managers MUST be able to configure incident categories and severity levels.
- **FR-022**: Managers MUST be able to configure factory departments and sections used for incident tagging.
- **FR-023**: Managers MUST be able to configure escalation rules by severity, overdue duration, department or section, and approval requirement.
- **FR-024**: System MUST enforce role-based permissions consistently for all incident, action, analytics, configuration, and user-management capabilities.
- **FR-025**: System MUST provide authorized users with dashboard metrics for open incident count, closure rate trends, average resolution time, and incidents by department.
- **FR-026**: Dashboard metrics MUST be derived from incident records, corrective actions, and status-change history.
- **FR-027**: System MUST maintain audit history for material changes to incidents, corrective actions, user roles, categories, severity levels, factory sections, and escalation rules.
- **FR-028**: System MUST support seed or sample data that demonstrates roles, incidents, corrective actions, categories, severity levels, factory sections, escalation rules, and dashboard metrics.
- **FR-029**: System MUST provide setup guidance sufficient for a new operator or administrator to prepare the system for factory use.
- **FR-030**: System MUST preserve historical incident records when categories, severity levels, departments, sections, or users are later changed or deactivated.

### Key Entities *(include if feature involves data)*

- **User**: A person who accesses the system; includes identity, role, active status, and relationships to reported incidents, assigned actions, and audit events.
- **Role**: Permission grouping for Worker, Supervisor, and Manager access levels.
- **Incident**: A reported factory issue such as machine breakdown, quality issue, safety incident, or compliance finding; includes category, severity, department or section, reporter, status, timestamps, root cause, escalation state, and closure information.
- **Incident Image**: Supporting visual evidence attached to an incident; includes relationship to incident, uploader, upload time, and descriptive metadata.
- **Incident Category**: Configurable classification for incident type, such as machine, quality, safety, or compliance.
- **Severity Level**: Configurable indication of incident impact or urgency, used for prioritization and escalation.
- **Factory Department or Section**: Configurable factory location or ownership area used to route, filter, and analyze incidents.
- **Corrective Action**: Resolution task linked to an incident; includes owner, due date, completion percentage, status, and completion history.
- **Escalation Rule**: Configurable policy that determines when incidents or actions require supervisor or manager attention.
- **Notification**: Alert sent to a responsible user when incidents, actions, escalations, or approvals require attention.
- **Status History**: Chronological record of incident status changes used for auditability and analytics.
- **Audit Event**: Record of important user or system activity affecting incidents, actions, permissions, configuration, or escalation.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: At least 95% of factory incident reports can be submitted with complete classification, location, severity, and supporting images in under 3 minutes.
- **SC-002**: Workers can confirm the current status of their own reported incidents in under 30 seconds without contacting a supervisor.
- **SC-003**: Supervisors can create and assign corrective actions for a reported incident in under 2 minutes.
- **SC-004**: 100% of high-severity incidents are flagged for escalation immediately after submission according to configured rules.
- **SC-005**: 100% of overdue corrective actions are visible as overdue during the next overdue review cycle.
- **SC-006**: Managers can view open incident count, closure trends, average resolution time, and department distribution from current incident history without manual spreadsheet consolidation.
- **SC-007**: Average time to identify unresolved incidents decreases by at least 60% compared with the current fragmented tracking process.
- **SC-008**: At least 90% of sampled incident records include complete status history sufficient to determine resolution time and closure outcome.
- **SC-009**: Unauthorized role access attempts to restricted incident, analytics, configuration, or user-management capabilities are blocked in 100% of tested cases.

## Assumptions

- Factory users have individual accounts so incident ownership, action assignment, approvals, and audit history can be attributed to named users.
- Worker, Supervisor, and Manager are the only required roles for the initial release.
- Initial incident categories include machine breakdown, quality issue, safety incident, and compliance finding, with managers able to change them later.
- Initial severity levels include at least low, medium, high, and critical, with managers able to change them later.
- Status workflow includes Open, active resolution states, closure approval where required, Closed, and Reopened for incidents that fail validation after closure.
- Notifications are required inside the system at minimum; additional delivery channels may be added later without changing the core incident workflow.
- Historical records remain reportable after configuration values or users are deactivated.
- Sample data is sufficient to demonstrate the main workflows and dashboard metrics in a non-production environment.
