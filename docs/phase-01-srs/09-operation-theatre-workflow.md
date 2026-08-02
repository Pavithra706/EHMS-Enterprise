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

# 6. Main Operation Theatre Workflow

## Step 1 – Surgery Scheduling

The treating consultant decides that surgery is required.

The doctor creates a digital surgery request containing:

- Patient UHID
- Diagnosis
- Procedure
- Surgery Type
- Priority
- Expected Duration
- Required OT Equipment
- Required Implants
- Blood Requirement

Surgery Status:

SCHEDULED

---

## Step 2 – OT Scheduling

The OT Scheduling Service verifies:

- OT Availability
- Surgeon Availability
- Assistant Surgeon
- Anesthesiologist
- OT Nurse
- OT Technician
- Biomedical Equipment
- CSSD Instrument Sets

The OT room is reserved.

---

## Step 3 – Pre-operative Preparation

Before transferring the patient:

- Identity Verification
- Consent Verification
- Laboratory Reports
- Radiology Reports
- Blood Availability
- Fasting Confirmation
- Allergy Verification
- Implant Availability

Patient Status:

READY_FOR_OT

---

## Step 4 – Patient Transfer

The patient is transported from:

- Ward
- ICU
- Emergency

to

Operation Theatre.

The barcode wristband is scanned before entering OT.

Patient Status:

IN_OPERATION_THEATRE

---

## Step 5 – WHO Surgical Safety Checklist

The OT team performs:

Before Anesthesia

- Patient Identity
- Surgical Site
- Planned Procedure
- Consent
- Allergy Check

Before Incision (Time-Out)

- Team Introduction
- Antibiotic Given
- Required Equipment Available
- Blood Available
- Imaging Available

Before Patient Leaves OT

- Instrument Count
- Sponge Count
- Needle Count
- Specimen Label Verification
- Procedure Documentation Completed

# 7. Surgery Procedure

After anesthesia:

↓

Surgical Incision

↓

Procedure Performed

↓

Implants Recorded (if any)

↓

Blood Transfusion (if required)

↓

Continuous Vital Monitoring

↓

Procedure Completed

↓

Operation Notes Recorded

↓

Digital Signature by Surgeon

↓

Patient Shifted to Recovery Room

# 8. Recovery Workflow

After surgery:

The Recovery Team monitors:

- Blood Pressure
- Pulse
- Oxygen Saturation
- Pain Score
- Consciousness Level
- Bleeding
- Surgical Dressing

Recovery decision:

Stable

↓

Ward Transfer

Critical

↓

ICU Transfer

Further surgery required

↓

OT Reschedule

# 9. CSSD Integration

After every surgery:

Used instruments

↓

Count Verification

↓

Transport to CSSD

↓

Cleaning

↓

Disinfection

↓

Sterilization

↓

Packaging

↓

Quality Check

↓

Returned to OT

Every instrument set is tracked using barcode/RFID.

# 10. Implant & Consumable Tracking

The system records:

- Implant Name
- Manufacturer
- Batch Number
- Serial Number
- Expiry Date
- Surgeon
- Patient UHID

This information becomes part of the patient's permanent Electronic Health Record.

