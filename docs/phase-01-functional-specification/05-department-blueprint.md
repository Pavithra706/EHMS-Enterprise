# Department Blueprint

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Hospital Business Blueprint |
| Document | Department Blueprint |
| Version | 1.0 |
| Status | Draft |
| Author | Pavithra K V |
| Date | 2026-08-03 |

---

# Version History

| Version | Date | Description | Author |
|----------|------|-------------|--------|
| 1.0 | 2026-08-03 | Initial Version | Pavithra K V |

---

# Table of Contents

1. Purpose
2. Department Classification
3. Clinical Departments
4. Diagnostic Departments
5. Surgical Departments
6. Critical Care Departments
7. Support Departments
8. Administrative Departments
9. Department Standard Structure
10. Department Workflow
11. Inter-Department Communication
12. Digital Responsibilities
13. Business Rules
14. KPIs
15. Future Database Entities
16. Future APIs
17. Future Dashboards
18. Approval

---

# 1. Purpose

This document defines the organizational structure of all departments within the Enterprise Hospital Management System (EHMS). It establishes departmental responsibilities, communication channels, digital workflows, and operational standards for a modern super speciality hospital.

---

# 2. Department Classification

The hospital departments are grouped into the following categories:

- Clinical Departments
- Diagnostic Departments
- Surgical Departments
- Critical Care Departments
- Emergency Departments
- Support Services
- Administrative Departments
- Allied Health Services

---

# 3. Clinical Departments

The hospital includes the following clinical departments:

- General Medicine
- Cardiology
- Neurology
- Neurosurgery
- Nephrology
- Urology
- Gastroenterology
- Surgical Gastroenterology
- Oncology
- Endocrinology
- Pulmonology
- Orthopedics
- Pediatrics
- Obstetrics & Gynecology
- ENT
- Ophthalmology
- Dermatology
- Psychiatry
- Dentistry
- Physiotherapy

---

# 4. Diagnostic Departments

The diagnostic services include:

- Laboratory
- Pathology
- Microbiology
- Biochemistry
- Radiology
- MRI
- CT Scan
- Ultrasound
- X-Ray
- PACS

---

# 5. Surgical Departments

The surgical services include:

- Operation Theatre
- CSSD
- Cath Lab
- Organ Transplant
- Day Care Surgery
- Recovery Unit

---

# 6. Critical Care Departments

Critical care includes:

- Emergency Medicine
- Trauma
- ICU
- NICU
- PICU
- CCU
- HDU
- Isolation Ward

---

# 7. Support Departments

Support services include:

- Pharmacy
- Blood Bank
- Biomedical Engineering
- Housekeeping
- Laundry
- Diet Services
- Maintenance
- Ambulance Services
- Security
- Visitor Management

---

# 8. Administrative Departments

Administrative services include:

- Director Office
- Co-Director Office
- Hospital Administration
- Human Resources
- Finance
- Billing
- Insurance
- Medical Records
- Information Technology
- Quality Assurance

---

# 9. Standard Department Structure

Every clinical department follows the same staffing structure.

## Department Head

Responsible for overall department management.

## Consultant Doctors

2

## Specialist Doctors

2

## MD Doctors

2

## Junior Doctors

2

## Nurses

10

## Department Coordinator

1

## Reception (if applicable)

1

---

# 10. Department Workflow

Every department follows this digital workflow.

```
Patient Arrives

↓

Barcode Scan

↓

Patient Record Opens

↓

Queue Generated

↓

Nurse Assessment

↓

Vitals

↓

Junior Doctor

↓

MD Doctor

↓

Consultant

↓

Diagnosis

↓

Tests (if required)

↓

Treatment

↓

Prescription

↓

Admission / Discharge
```

---

# 11. Inter-Department Communication

Departments communicate electronically.

Examples:

Emergency

↓

Radiology

↓

Laboratory

↓

Blood Bank

↓

Operation Theatre

↓

ICU

↓

Ward

↓

Billing

↓

Pharmacy

↓

Discharge

Every communication is digitally logged.

---

# 12. Digital Responsibilities

Each department can:

- View assigned patients
- Scan patient barcode
- Update patient status
- Create clinical notes
- Request investigations
- View reports
- Prescribe medicines
- Refer patients
- Admit patients
- Transfer patients
- Discharge patients

---

# 13. Business Rules

BR-001

Every patient must belong to at least one department.

BR-002

Departments cannot modify records belonging to another department without permission.

BR-003

Every department activity must generate an audit log.

BR-004

Patient movement between departments must be digitally recorded.

BR-005

Every consultation must be time stamped.

BR-006

Only authorized staff may approve treatment decisions.

---

# 14. Key Performance Indicators (KPIs)

Every department measures:

- Average Waiting Time
- Consultation Time
- Patient Satisfaction
- Bed Occupancy
- Staff Utilization
- Emergency Response Time
- Report Turnaround Time
- Queue Length
- Referral Count

---

# 15. Future Database Entities

The following database tables will support departments:

Department

DepartmentType

DepartmentRoom

DepartmentQueue

DepartmentStaff

DepartmentShift

DepartmentEquipment

DepartmentInventory

DepartmentAttendance

DepartmentDashboard

---

# 16. Future APIs

Examples:

GET /departments

GET /departments/{id}

POST /departments

PUT /departments/{id}

GET /departments/{id}/staff

GET /departments/{id}/patients

POST /departments/{id}/queue

---

# 17. Future Dashboards

Every department receives its own dashboard showing:

- Today's Patients
- Waiting Queue
- Doctor Availability
- Nurse Availability
- Equipment Status
- Admissions
- Discharges
- Emergency Alerts
- Notifications
- Daily Statistics

---

# 18. Approval

| Role | Status |
|------|--------|
| Hospital Administrator | Pending |
| Chief Medical Officer | Pending |
| System Architect | Pending |
| Development Team | Pending |