# OPD Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Hospital Business Blueprint |
| Document | OPD Workflow |
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
6. OPD Workflow
7. Alternative Workflows
8. Exception Handling
9. Business Rules
10. Notifications
11. Digital Transformation
12. Future Database Entities
13. Future APIs
14. Future UI Screens
15. KPIs
16. Approval

# 1. Purpose

The Outpatient Department (OPD) is the primary entry point for patients seeking consultation without requiring immediate admission.

The purpose of this workflow is to digitize the complete OPD process from patient registration to consultation, investigation, prescription, billing, referral, and discharge while eliminating manual paperwork.

# 2. Business Objective

The OPD workflow aims to:

- Reduce patient waiting time.
- Eliminate paper records.
- Generate Electronic Health Records (EHR).
- Improve doctor productivity.
- Provide real-time patient tracking.
- Enable digital prescriptions.
- Integrate laboratory, radiology, pharmacy, and billing.
- Support referrals to speciality departments.

# 3. Scope

The workflow covers:

- Patient Registration
- Appointment
- Billing
- Token Generation
- Queue Management
- Nurse Assessment
- Doctor Consultation
- Investigations
- Pharmacy
- Referral
- Admission Decision
- Patient Exit

# 4. Actors

Primary Actors

- Patient
- Receptionist
- Billing Executive
- Nurse
- Doctor

Secondary Actors

- Laboratory Technician
- Radiology Technician
- Pharmacist
- Insurance Executive
- Hospital Administrator

System Actors

- EHMS
- Barcode Scanner
- QR Code Generator
- Notification Service
- Payment Gateway

# 5. Preconditions

Before OPD consultation:

- Hospital is operational.
- Doctor is checked in.
- Nurse is checked in.
- OPD room is active.
- Queue system is online.
- Billing system is available.
- Patient is registered or ready for registration.
