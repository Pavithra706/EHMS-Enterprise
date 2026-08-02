# Operation Theatre (OT) Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Hospital Business Blueprint |
| Document | Operation Theatre Workflow |
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
6. Main OT Workflow
7. Alternative Workflows
8. Exception Handling
9. Business Rules
10. Notifications
11. Future Database Entities
12. Future APIs
13. Future UI Screens
14. RBAC
15. Audit Logs
16. KPIs
17. AI Features
18. Security
19. Approval

# 1. Purpose

The Operation Theatre (OT) workflow manages all surgical procedures performed within the hospital. It coordinates patients, surgeons, anesthesiologists, OT nurses, CSSD, Blood Bank, Pharmacy, ICU, and Biomedical Engineering while maintaining complete digital surgical records.

# 2. Business Objective

The OT workflow aims to:

- Digitally schedule surgeries.
- Reduce surgery delays.
- Improve patient safety.
- Maintain surgical documentation.
- Track surgical instruments.
- Coordinate multidisciplinary teams.
- Integrate OT with EHR, ICU, Pharmacy, Blood Bank, Billing, and CSSD.

# 3. Scope

The workflow covers:

- Surgery Scheduling
- Emergency Surgery
- OT Preparation
- Patient Verification
- Anesthesia
- Surgery
- Recovery
- ICU Transfer
- Ward Transfer
- OT Cleaning
- Instrument Sterilization

# 4. Actors

Primary Actors

- Patient
- Surgeon
- Assistant Surgeon
- Anesthesiologist
- OT Nurse
- OT Technician

Secondary Actors

- Blood Bank
- Pharmacy
- CSSD Staff
- ICU Team
- Biomedical Engineer

System Actors

- EHMS
- OT Scheduling Service
- Notification Service
- Barcode Scanner
- EHR Service

# 5. Preconditions

Before surgery:

- Patient admitted.
- Consent signed digitally.
- OT scheduled.
- Surgeon assigned.
- OT Nurse assigned.
- Instruments sterilized.
- Blood availability confirmed (if required).
- Anesthesia clearance completed.
- Laboratory reports available.
- Radiology reports available.

