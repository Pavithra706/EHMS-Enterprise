# IPD Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Hospital Business Blueprint |
| Document | IPD Workflow |
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
2. Business Objective
3. Scope
4. Actors
5. Preconditions
6. Main IPD Workflow
7. Alternative Workflows
8. Exception Handling
9. Business Rules
10. Notifications
11. Future Database Entities
12. Future REST APIs
13. Future UI Screens
14. RBAC
15. Audit Logs
16. KPIs
17. Future AI Features
18. Security Considerations
19. Approval

# 1. Purpose

The Inpatient Department (IPD) manages patients who require admission for continuous medical care, surgery, observation, rehabilitation, or long-term treatment.

The workflow digitizes the complete inpatient lifecycle from admission to discharge while ensuring seamless coordination among all hospital departments.
# 2. Business Objective

The IPD workflow aims to:

- Digitize patient admission.
- Allocate beds efficiently.
- Coordinate multidisciplinary care.
- Maintain complete Electronic Health Records (EHR).
- Support continuous nursing and doctor rounds.
- Integrate diagnostics, pharmacy, billing, and support services.
- Improve patient safety and treatment quality.

# 3. Scope

The workflow includes:

- Patient Admission
- Bed Allocation
- Ward Allocation
- Nursing Assessment
- Doctor Rounds
- Medication Administration
- Laboratory & Radiology Requests
- Operation Theatre Transfers
- ICU Transfers
- Diet Management
- Housekeeping
- Biomedical Equipment
- Billing
- Insurance
- Discharge

# 4. Actors

Primary Actors

- Patient
- Attender
- Admission Desk
- Doctor
- Nurse

Secondary Actors

- Pharmacist
- Laboratory Technician
- Radiology Technician
- Dietitian
- Housekeeping Staff
- Biomedical Engineer
- Billing Executive
- Insurance Executive

System Actors

- EHMS
- Bed Management Service
- Notification Service
- Billing Service
- EHR Service

# 5. Preconditions

Before admission:

- Patient registration is completed.
- Doctor recommends admission.
- Beds are available.
- Ward is operational.
- Billing and Insurance systems are online.
- Nursing staff is assigned.
- Department is active.

