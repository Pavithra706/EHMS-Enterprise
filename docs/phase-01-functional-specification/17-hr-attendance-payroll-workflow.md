# Human Resource, Attendance & Payroll Management System (HRMS)

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Enterprise Functional Specification |
| Module | Human Resource, Attendance & Payroll Management System |
| Version | 2.0 |
| Status | Draft |
| Author | Pavithra K V |

---

# 1. Purpose

The Human Resource Management System (HRMS) manages the complete employee lifecycle, including recruitment, onboarding, attendance, shift scheduling, leave management, payroll processing, performance evaluation, compliance, and employee records while integrating with all hospital departments.

---

# 2. Business Objective

The HRMS aims to:

- Digitize employee management.
- Automate attendance tracking.
- Manage rotating hospital shifts.
- Process payroll accurately.
- Maintain employee records.
- Improve workforce planning.
- Integrate with Finance, Authentication, and Analytics.

---

# 3. Scope

The workflow covers:

- Recruitment
- Employee Onboarding
- Employee Master Records
- Department Assignment
- Shift Scheduling
- Attendance
- Leave Management
- Payroll
- Performance Review
- Training & Certification
- Employee Exit Process

---

# 4. Actors

## Primary

- Employee
- HR Executive
- Department Manager
- Payroll Officer

## Secondary

- Finance Officer
- Hospital Administrator

## System

- EHMS
- HR Service
- Attendance Service
- Payroll Service
- Notification Service
- Analytics Service
- Authentication Service

---

# 5. Preconditions

- Department exists.
- Employee role defined.
- Salary structure configured.
- Attendance devices operational.
- Payroll calendar configured.

---

# 6. Main Workflow

## Step 1 – Recruitment

HR creates job opening.

↓

Candidate applies.

↓

Interview conducted.

↓

Selection approved.

↓

Offer generated.

---

## Step 2 – Employee Onboarding

Employee joins.

↓

Employee ID generated.

↓

Role assigned.

↓

Department assigned.

↓

System account created.

↓

ID card issued.

---

## Step 3 – Attendance

Attendance captured through:

- Biometric
- RFID Card
- Mobile App
- Manual Override (Authorized)

↓

Attendance updated.

---

## Step 4 – Shift Management

Shift assigned.

Examples:

- Morning
- Evening
- Night
- Rotational
- On-call

Duty roster published.

---

## Step 5 – Leave Management

Employee requests leave.

↓

Manager approval.

↓

HR approval (if required).

↓

Leave balance updated.

---

## Step 6 – Payroll Processing

Calculate:

- Basic Salary
- Allowances
- Overtime
- Incentives
- Deductions
- Taxes
- PF
- ESI
- Professional Tax

↓

Salary generated.

↓

Payslip published.

---

## Step 7 – Performance Management

Manager records:

- Goals
- KPIs
- Performance Rating
- Feedback
- Promotions

---

## Step 8 – Exit Process

Resignation

↓

Clearance

↓

Asset Return

↓

Final Settlement

↓

Account Deactivation

---

# 7. Workflow State Machine

APPLIED

↓

SELECTED

↓

ONBOARDED

↓

ACTIVE

↓

ON_LEAVE

↓

RESIGNED

↓

EXIT_COMPLETED

---

# 8. Event Flow

HR Service

↓

Authentication Service

↓

Attendance Service

↓

Payroll Service

↓

Finance Service

↓

Notification Service

↓

Analytics Service

---

# 9. Alternative Workflows

- Emergency Shift Replacement
- Contract Employee
- Visiting Consultant
- Intern / Trainee
- Temporary Staff

---

# 10. Exception Handling

HR-EX-001

Biometric Failure

↓

Manual Attendance Approval

---

HR-EX-002

Payroll Error

↓

Recalculation

↓

Approval

---

HR-EX-003

Leave Balance Insufficient

↓

Reject Request

---

HR-EX-004

Shift Conflict

↓

Manager Resolution

---

# 11. Business Rules

HR-BR-001

Every employee shall have a unique Employee ID.

---

HR-BR-002

Attendance shall be recorded daily.

---

HR-BR-003

Payroll shall be generated monthly.

---

HR-BR-004

Leave requires approval.

---

HR-BR-005

Employee access shall follow assigned roles.

---

# 12. Business Validation Rules

- Employee active.
- Department assigned.
- Shift assigned.
- Attendance available.
- Payroll approved.

---

# 13. Error Codes

HR001 Employee Not Found

HR002 Attendance Missing

HR003 Payroll Failed

HR004 Leave Rejected

HR005 Shift Conflict

---

# 14. Notifications

- Interview Scheduled
- Employee Joined
- Shift Assigned
- Leave Approved
- Payroll Generated
- Promotion Approved
- Exit Completed

---

# 15. Integration Points

- Authentication
- Finance
- Payroll
- Attendance
- Security
- Analytics
- Notification

---

# 16. Database Relationships

Employee

↓

Department

↓

Attendance

↓

Shift

↓

Leave

↓

Payroll

↓

Performance

---

# 17. Future Database Tables

- Employee
- DepartmentAssignment
- Attendance
- Shift
- LeaveRequest
- Payroll
- Payslip
- PerformanceReview
- Training
- ExitClearance

---

# 18. REST APIs

POST /employees

GET /employees/{id}

POST /attendance

POST /leave

POST /payroll/process

GET /payslips/{id}

POST /performance

---

# 19. UI Screens

- HR Dashboard
- Employee Directory
- Attendance Dashboard
- Shift Planner
- Leave Management
- Payroll Dashboard
- Performance Review
- Employee Profile

---

# 20. RBAC Matrix

| Role | Permission |
|------|------------|
| HR Executive | Manage employees |
| Department Manager | Approve leave, review performance |
| Payroll Officer | Process payroll |
| Employee | View profile, attendance, payslips |
| Administrator | Full access |

---

# 21. Audit Logs

- Employee Created
- Attendance Recorded
- Leave Approved
- Payroll Generated
- Performance Updated
- Employee Exited

---

# 22. KPIs

- Employee Attendance Rate
- Payroll Accuracy
- Leave Utilization
- Staff Turnover
- Vacancy Rate
- Overtime Hours
- Employee Satisfaction

---

# 23. SLA

Employee Onboarding ≤ 1 Business Day

Attendance Update Real-Time

Leave Approval ≤ 2 Business Days

Payroll Processing ≤ 4 Hours

---

# 24. Future AI Features

- Shift Optimization
- Staff Demand Forecasting
- Attrition Prediction
- Overtime Prediction
- Performance Analytics
- Leave Pattern Analysis

---

# 25. Healthcare Standards

- HL7 FHIR Practitioner
- HL7 FHIR PractitionerRole
- ISO 27001 (Access Control)
- Labor Law Compliance

---

# 26. Microservice Mapping

Primary

↓

hr-service

Connected Services

↓

attendance-service

↓

payroll-service

↓

notification-service

↓

analytics-service

↓

auth-service

↓

finance-service

---

# 27. Security

- Role-Based Access Control
- Multi-Factor Authentication
- Audit Logs
- Payroll Encryption
- Employee Data Privacy

---

# 28. Approval

| Role | Status |
|------|--------|
| HR Manager | Pending |
| Finance Manager | Pending |
| Hospital Administrator | Pending |
| System Architect | Pending |