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

# 6. Main IPD Workflow

## Step 1 – Admission Decision

A patient can be admitted through:

- OPD Consultation
- Emergency Department
- Direct Admission
- Referral from another hospital

The treating doctor recommends admission.

The system creates an Admission Request.

Admission Status:

PENDING

---

## Step 2 – Admission Desk Verification

The Admission Desk verifies:

- Patient Identity
- UHID
- Insurance Eligibility
- Corporate Eligibility
- Bed Availability
- Required Department

Admission documents are digitally verified.

---

## Step 3 – Bed Allocation

The Bed Management Service searches for:

- Department
- Ward
- Room
- Bed
- Isolation Requirement
- ICU Requirement
- Gender-specific availability

The selected bed is reserved.

Bed Status:

RESERVED

---

## Step 4 – Ward Assignment

The patient is assigned to:

- Department
- Ward
- Room
- Bed

The assigned Nurse and Duty Doctor are automatically notified.

---

## Step 5 – Barcode Wristband

The system prints:

- Patient Name
- UHID
- Barcode
- QR Code
- Blood Group
- Allergy Alert (if applicable)

The wristband is attached before entering the ward.

Every medication and procedure will be verified using barcode scanning.

---

## Step 6 – Nursing Admission Assessment

The nurse scans the barcode.

The system displays:

- Medical History
- Allergies
- Current Medications
- Diagnosis
- Previous Admissions

The nurse records:

- Height
- Weight
- Blood Pressure
- Temperature
- Pulse
- Respiratory Rate
- Oxygen Saturation
- Pain Score
- Fall Risk Assessment

Admission assessment is saved to the EHR.

---

## Step 7 – Doctor Admission Orders

The doctor creates admission orders:

- Diagnosis
- Treatment Plan
- Medication Orders
- Laboratory Orders
- Radiology Orders
- Diet Orders
- Nursing Instructions
- Isolation Instructions

Orders are digitally signed.

---

## Step 8 – Treatment Begins

The patient status changes to:

ADMITTED

The following departments receive notifications:

- Pharmacy
- Laboratory
- Radiology
- Diet Services
- Nursing Station
- Billing
- Insurance

# 7. Daily Inpatient Care

Every admitted patient follows a daily care cycle.

```
Morning Nursing Assessment

↓

Doctor Ward Round

↓

Medication Administration

↓

Laboratory Tests

↓

Radiology (if required)

↓

Specialist Consultation

↓

Diet Delivery

↓

Physiotherapy (if required)

↓

Evening Nursing Assessment

↓

Night Monitoring
```

The patient's Electronic Health Record (EHR) is updated after every clinical activity.

# 8. Department Integration

During admission, the IPD interacts with:

- Pharmacy
- Laboratory
- Radiology
- Blood Bank
- Operation Theatre
- ICU
- Diet Department
- Housekeeping
- Laundry
- Biomedical Engineering
- Billing
- Insurance
- Security

All department requests are generated electronically.

Every service completion updates the patient's EHR automatically.

