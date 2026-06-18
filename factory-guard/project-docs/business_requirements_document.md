# Business Requirements Document

## Product

Factory Guard: Smart Factory Incident & Action Management Platform

## Document Purpose

This Business Requirements Document (BRD) defines the business need, scope, functional expectations, operating model, and success criteria for a SaaS platform that digitizes incident reporting, investigation, escalation, corrective action tracking, and analytics for garment manufacturing factories.

## 1. Executive Summary

Garment factories currently manage machine breakdowns, quality issues, safety incidents, compliance findings, and production disruptions through fragmented tools such as WhatsApp, Excel, phone calls, and email. These disconnected workflows create poor visibility, delayed response times, weak accountability, and inconsistent follow-up on corrective actions.

Factory Guard will provide a centralized multi-factory platform for incident capture, investigation, root cause analysis, corrective action management, escalation, compliance tracking, and operational analytics. The platform will standardize incident handling across departments while improving response time, closure discipline, audit readiness, and management visibility.

## 2. Problem Statement

Current factory operations face the following business problems:

- Incident reporting is decentralized and inconsistent.
- Critical issues are escalated manually and often too late.
- Corrective and preventive actions are hard to assign, track, and verify.
- Management cannot view real-time operational risk across factories.
- Compliance observations and audit findings are not tied to structured CAPA workflows.
- Historical incident data is difficult to analyze for repeat causes and systemic issues.

These issues lead to longer downtime, avoidable production loss, recurring quality failures, higher compliance risk, and weak cross-functional accountability.

## 3. Business Objectives

The platform must support the following business objectives:

- Centralize all operational incident reporting in one system.
- Improve accountability through named ownership and due-date tracking.
- Reduce incident response and resolution time.
- Standardize root cause investigation and corrective action workflows.
- Automate escalation for high-risk and overdue cases.
- Improve compliance management and audit evidence traceability.
- Provide real-time dashboards for factory and corporate management.
- Generate trends and KPI reporting for continuous improvement.
- Support multiple factories, buildings, floors, lines, and departments.

## 4. Stakeholders

Primary stakeholders:

- Factory ownership and executive management
- Factory managers
- Department managers
- Line supervisors
- Workers and operators
- Quality teams
- Maintenance teams
- Safety teams
- Compliance and audit teams
- IT and system administrators

Secondary stakeholders:

- Corporate operations leadership
- External auditors
- Buyers and compliance reviewers
- Continuous improvement teams

## 5. Scope

### In Scope

- Incident capture from web and mobile
- Incident categorization, severity classification, and workflow tracking
- Root cause analysis workflows
- Corrective action and CAPA management
- SLA and severity-based escalation
- Role-based access control
- Notifications through in-app, email, and SMS
- Dashboards, analytics, and exportable reports
- Multi-factory and multi-company support
- Offline-capable mobile incident capture

### Out of Scope for Initial Release

- Direct WhatsApp Business API integration
- Deep ERP, HRMS, and IoT integrations
- Predictive analytics and AI-based recommendations
- Full machine telemetry ingestion
- External contractor portal

## 6. Business Process Overview

The target operating model is:

1. An incident is reported from mobile or web.
2. The system classifies the incident by category, severity, and location.
3. Relevant supervisors or managers are notified immediately.
4. The incident is reviewed and assigned for investigation.
5. Investigation artifacts and root cause analysis are recorded.
6. One or more corrective actions are created and assigned.
7. The system tracks due dates, reminders, SLA compliance, and escalations.
8. Evidence is attached and actions are reviewed and verified.
9. The incident is closed only after validation is complete.
10. Analytics update in near real time for management review.

## 7. User Roles and Responsibilities

### Role Definitions

| Role | Primary Responsibilities |
|------|--------------------------|
| Worker / Operator | Report incidents, attach photos, track own submissions |
| Line Supervisor | Review incidents for assigned lines, acknowledge high-severity issues, coordinate first response |
| Department Manager | Oversee incidents and actions within department, approve escalations, monitor SLA performance |
| Factory Manager | Monitor factory-wide operational risk, approve critical closures, oversee escalations |
| Compliance Officer | Record audit findings, manage CAPA, verify compliance evidence, support reporting |
| Maintenance Engineer | Investigate machine failures, document root causes, execute maintenance actions |
| Quality Manager | Investigate quality issues, define containment and corrective actions, verify quality closure |
| Safety Officer | Investigate safety events, ensure containment, track corrective actions, verify safety compliance |
| System Administrator | Manage users, roles, master data, access policies, and system configuration |

### RBAC Matrix

| Capability | Worker | Supervisor | Dept Manager | Factory Manager | Compliance | Maintenance | Quality | Safety | Sys Admin |
|------------|--------|------------|--------------|-----------------|------------|-------------|---------|--------|-----------|
| Create incident | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| View own incidents | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| View department incidents | N | Y | Y | Y | Y | Y | Y | Y | Y |
| View factory-wide incidents | N | N | Limited | Y | Limited | Limited | Limited | Limited | Y |
| Edit incident before review | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| Change status to Under Review | N | Y | Y | Y | Y | Y | Y | Y | Y |
| Assign investigator | N | Y | Y | Y | Y | Y | Y | Y | Y |
| Add RCA details | N | Y | Y | Y | Y | Y | Y | Y | Y |
| Create corrective actions | N | Y | Y | Y | Y | Y | Y | Y | Y |
| Approve corrective action completion | N | Y | Y | Y | Y | Y | Y | Y | Y |
| Verify and close incident | N | N | Y | Y | Y | N | Y | Y | Y |
| Manage compliance findings | N | N | N | Y | Y | N | N | N | Y |
| Access dashboards and analytics | Limited | Y | Y | Y | Y | Y | Y | Y | Y |
| Export reports | N | Y | Y | Y | Y | Y | Y | Y | Y |
| Manage users and master data | N | N | N | N | N | N | N | N | Y |

Limited = restricted to authorized factory, department, or assigned records.

## 8. Functional Requirements

### 8.1 Incident Management

The system shall:

- Allow incident reporting from web and mobile devices.
- Support image, document, and evidence attachments.
- Capture incident title, description, category, severity, reporter, and occurrence timestamp.
- Tag each incident with company, factory, building, floor, line, machine, and department where applicable.
- Auto-generate a unique incident ID.
- Maintain a full audit trail of status changes, assignments, comments, and edits.
- Support incident categories:
  - Machine Breakdown
  - Quality Issue
  - Safety Incident
  - Compliance Finding
  - Production Delay
  - Utility Failure
  - Environmental Incident
  - Other
- Support severity levels:
  - Low
  - Medium
  - High
  - Critical

### 8.2 Incident Workflow

Standard workflow:

`Open -> Under Review -> Investigation -> Action In Progress -> Pending Verification -> Closed`

Status transition rules:

- `Open` is created by any authorized reporter.
- `Under Review` requires supervisor or above.
- `Investigation` requires an assigned investigator or owner.
- `Action In Progress` requires at least one corrective action.
- `Pending Verification` requires all actions marked completed with evidence attached.
- `Closed` requires verification by an authorized approver.
- Reopen must be allowed when verification fails or repeat issues occur.

### 8.3 Root Cause Analysis

The system shall:

- Allow one or more root causes to be documented per incident.
- Support structured 5 Why analysis.
- Support fishbone analysis inputs by category.
- Capture investigation notes and supporting evidence.
- Route RCA for review or approval where required by workflow.
- Preserve investigation history and approver comments.

### 8.4 Corrective Action Management

Each incident may have one or more corrective actions. Each action must contain:

- Action title
- Action description
- Assigned owner
- Due date
- Priority
- Department
- Status
- Completion percentage
- Evidence attachment

Corrective action workflow:

`Assigned -> In Progress -> Review -> Completed -> Verified`

Validation and approval rules:

- Action owner is mandatory.
- Due date is mandatory.
- Completed status requires completion notes and evidence.
- Verified status requires approval by an authorized verifier.
- Overdue actions must be automatically flagged.

### 8.5 Escalation Engine

The system shall enforce configurable escalation rules.

Severity-based escalation:

- High severity:
  - Notify supervisor immediately.
  - Escalate if not acknowledged within 2 hours.
- Critical severity:
  - Notify department manager immediately.
  - Escalate to factory manager within 30 minutes.

SLA escalation:

- Flag overdue corrective actions.
- Send reminders before due dates.
- Escalate unresolved incidents exceeding SLA.
- Escalate corrective actions exceeding SLA thresholds.

Notification channels:

- In-app notifications
- Email
- SMS
- WhatsApp integration in a future phase

### 8.6 Compliance Management

The platform shall support:

- Compliance observations
- Audit findings
- CAPA tracking
- Evidence management
- Verification workflow
- Regulatory and audit reporting

### 8.7 Dashboard and Analytics

Management dashboards shall provide:

- Incident KPIs:
  - Total incidents
  - Open incidents
  - Closed incidents
  - Overdue incidents
  - Critical incidents
- Performance metrics:
  - Closure rate
  - Average resolution time
  - Average response time
  - SLA compliance percentage
- Trend analysis:
  - Incidents by category
  - Incidents by department
  - Incidents by factory
  - Monthly trends
  - Root cause trends
  - Repeat incidents
- Corrective action analytics:
  - Open actions
  - Completed actions
  - Overdue actions
  - Action completion rate

Analytics must support drill-down and export.

### 8.8 Reporting

The system shall generate:

- Incident Register
- Safety Report
- Quality Incident Report
- Machine Breakdown Report
- Compliance Report
- Corrective Action Report
- SLA Performance Report

Reports must support PDF and Excel export.

### 8.9 Mobile Requirements

The solution shall provide:

- Mobile responsive user experience
- Camera-based photo capture
- Offline incident capture with later sync
- Push notifications
- QR code scanning for machine or asset lookup

## 9. Non-Functional Requirements

### Security

- Role-based access control for all protected functions
- Secure authentication and session management
- Encryption of sensitive data in transit and at rest
- Audit logging for key user and workflow actions

### Performance

- Standard user actions should respond in under 3 seconds under normal load.
- The system should support at least 5,000 active users.

### Availability

- Target uptime shall be 99.9 percent, excluding scheduled maintenance.

### Scalability

- The platform must support multiple factories and multiple companies from a shared SaaS architecture.
- The architecture should support future integration expansion and increased transaction volume.

### Compliance

- The platform should support workflows aligned with ISO 9001, ISO 45001, social compliance audits, and garment-industry best practices.

## 10. Detailed User Stories

### Worker / Operator

- As a worker, I want to report an incident from my phone so that problems are recorded immediately.
- As a worker, I want to attach photos so that supervisors can assess severity quickly.
- As a worker, I want to track the status of incidents I reported so that I know whether action is being taken.

### Line Supervisor

- As a supervisor, I want immediate alerts for high-severity incidents so that I can respond within SLA.
- As a supervisor, I want to assign investigators and action owners so that accountability is clear.

### Department Manager

- As a department manager, I want to monitor overdue incidents and actions so that bottlenecks are removed quickly.
- As a department manager, I want escalation visibility so that unresolved issues do not remain hidden.

### Maintenance Engineer

- As a maintenance engineer, I want to document RCA for machine breakdowns so that repeat failures can be reduced.
- As a maintenance engineer, I want machine-linked history so that repairs can be prioritized using past incidents.

### Quality Manager

- As a quality manager, I want to investigate quality incidents and assign CAPA so that repeat defects are reduced.
- As a quality manager, I want trend data by line and department so that preventive action can be targeted.

### Safety Officer

- As a safety officer, I want safety events investigated and verified through a standard workflow so that compliance risk is reduced.

### Compliance Officer

- As a compliance officer, I want audit findings linked to evidence and closure records so that audits can be managed systematically.

### Factory Manager

- As a factory manager, I want a dashboard of operational risk across the factory so that I can intervene early on critical issues.

### System Administrator

- As a system administrator, I want to manage roles, users, and master data so that access and data quality remain controlled.

## 11. Use Cases

### Use Case 1: Report a Machine Breakdown

- Actor: Worker or Supervisor
- Trigger: Machine stops unexpectedly
- Main flow:
  1. User scans QR code or selects machine and location.
  2. User enters title, description, category, and severity.
  3. User attaches photo evidence.
  4. System generates incident ID and notifies responsible users.
- Outcome: Incident enters `Open` status and SLA timer begins.

### Use Case 2: Investigate a Safety Incident

- Actor: Safety Officer
- Trigger: Safety incident is assigned for investigation
- Main flow:
  1. Safety officer reviews incident details.
  2. Investigation notes, RCA, and evidence are added.
  3. Corrective actions are assigned.
  4. Actions are completed and verified.
- Outcome: Incident is closed after verification.

### Use Case 3: Manage a Compliance Finding

- Actor: Compliance Officer
- Trigger: Audit finding is reported
- Main flow:
  1. Finding is logged as a compliance incident.
  2. CAPA actions are assigned with due dates.
  3. Evidence is uploaded.
  4. Finding is verified and reported.
- Outcome: Audit trail is preserved for compliance reporting.

## 12. Process Flows

### Incident Lifecycle

`Report -> Review -> Investigate -> Assign Actions -> Execute Actions -> Verify -> Close`

### Escalation Flow

`Incident Created -> SLA Timer Starts -> Reminder -> Escalation -> Management Visibility -> Resolution`

### CAPA Flow

`Finding/Incident -> Root Cause -> Corrective Action -> Evidence Submission -> Verification -> Closure`

## 13. Data Model Overview

Core business entities:

| Entity | Description |
|--------|-------------|
| Company | Tenant-level business organization |
| Factory | Physical factory under a company |
| Building | Building within a factory |
| Floor | Floor or area within a building |
| Department | Functional department such as Production, Quality, Maintenance, Safety |
| Line | Production line within a department or factory |
| Machine / Asset | Identified equipment associated with incidents |
| User | Platform user with role and organization mapping |
| Role | Access-control definition |
| Incident | Central record for operational event or finding |
| Incident Category | Classification of the incident type |
| Severity | Business impact level |
| Investigation | RCA and investigation record tied to an incident |
| Corrective Action | Action item tied to an incident or finding |
| Attachment | Photo, document, or evidence file |
| Notification | Alert generated by workflow or SLA events |
| SLA Rule | Time-based service rule for incidents or actions |
| Audit / Compliance Finding | Specialized incident or linked compliance object |
| Comment / Activity Log | Chronological audit trail entry |

Key relationships:

- One company has many factories.
- One factory has many buildings, floors, departments, lines, and users.
- One incident belongs to one company and one factory, and may reference one department, line, and machine.
- One incident may have many attachments, comments, investigations, and corrective actions.
- One corrective action has one owner and one verifier.

## 14. KPI Definitions

| KPI | Definition |
|-----|------------|
| Total Incidents | Total incidents created in selected period |
| Open Incidents | Incidents not yet closed |
| Closed Incidents | Incidents moved to closed status in selected period |
| Overdue Incidents | Incidents exceeding configured SLA |
| Critical Incidents | Incidents marked critical severity |
| Closure Rate | Closed incidents divided by total incidents in period |
| Average Resolution Time | Average time from incident creation to closure |
| Average Response Time | Average time from incident creation to first acknowledged action |
| SLA Compliance % | Percentage of incidents and actions resolved within SLA |
| Open Actions | Corrective actions not verified complete |
| Overdue Actions | Actions past due date |
| Action Completion Rate | Verified completed actions divided by total actions |
| Repeat Incident Rate | Percentage of incidents with recurring cause, location, or asset pattern |

## 15. Dashboard Requirements

Dashboard capabilities must include:

- Role-based home dashboards
- Factory-wide and department-level views
- Date, factory, department, line, category, and severity filters
- Drill-down from KPI to incident list
- Trend charts and comparative views
- Export to PDF and Excel where relevant
- Highlighting of critical, overdue, and repeat-risk cases

## 16. Reporting Requirements

Each report should support filter, sort, export, and scheduled distribution where applicable.

| Report | Primary Users | Business Purpose |
|--------|---------------|------------------|
| Incident Register | Management, Supervisors | Master list of all incidents |
| Safety Report | Safety teams, Management | Review safety events and actions |
| Quality Incident Report | Quality teams | Track defects, causes, and corrections |
| Machine Breakdown Report | Maintenance teams | Monitor downtime and recurring failures |
| Compliance Report | Compliance teams, Auditors | Track findings, CAPA, and evidence |
| Corrective Action Report | Department managers | Monitor action ownership and aging |
| SLA Performance Report | Management | Measure response and closure discipline |

## 17. Assumptions

- Factories will adopt standardized incident categories and severity definitions.
- Users will have mobile devices or shared terminals available in the production environment.
- Internet connectivity may be intermittent, requiring offline capture support.
- Departments will nominate authorized approvers and verifiers.
- The organization will provide location, machine, department, and user master data.

## 18. Risks and Dependencies

### Risks

- User adoption may be slow if workflows are seen as additional administrative work.
- Poor master data quality can reduce reporting accuracy.
- Excessive manual notifications can cause alert fatigue.
- Approval bottlenecks may delay closure unless escalation rules are well tuned.
- Offline sync failures may create duplicate or incomplete incidents if not handled properly.

### Dependencies

- Availability of master data for factories, lines, machines, and departments
- Agreement on SLA rules and severity policies
- IT support for email and SMS notification services
- Security and access policy approval
- Change management and user training

## 19. Future Roadmap

### Phase 1

- Core incident management
- Corrective actions
- RCA workflows
- Dashboards
- Reports
- Mobile-responsive access

### Phase 2

- Offline-first mobile enhancements
- Advanced escalation rules
- Compliance workflow maturity
- QR-based machine workflows
- Scheduled reporting

### Phase 3

- ERP and HRMS integration
- IoT and machine monitoring integration
- WhatsApp Business API integration
- Predictive analytics and repeat-incident intelligence

## 20. Success Metrics

The business should target measurable improvements after rollout:

- 100 percent of reportable incidents logged in the platform
- 30 percent reduction in average incident response time within 6 months
- 25 percent reduction in average corrective action overdue rate within 6 months
- 20 percent reduction in repeat incidents in targeted categories within 12 months
- 90 percent or better SLA compliance for high and critical incidents
- 95 percent audit evidence traceability for compliance-related incidents
- 80 percent active usage among designated operational users within 3 months of go-live

## 21. Recommended Implementation Priorities

Priority 1:

- Incident creation and workflow
- Severity and SLA engine
- Action tracking
- Role-based access control
- Core dashboards

Priority 2:

- RCA templates
- Compliance workflows
- Advanced reports
- Mobile offline support

Priority 3:

- Integrations
- Predictive and cross-factory benchmarking
- Messaging channel expansion

## 22. Approval Criteria

This BRD will be considered accepted when:

- Business stakeholders confirm the scope and workflow reflect operational reality.
- Role and approval responsibilities are agreed across departments.
- KPI and SLA definitions are approved by management.
- Initial release priorities are confirmed for product planning and solution design.
