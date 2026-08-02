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

# 6. Main OPD Workflow

## Step 1 – Patient Arrival

The patient arrives at the hospital through the main entrance.

Possible patient types:

- Walk-in Patient
- Appointment Patient
- Corporate Patient
- Insurance Patient
- Follow-up Patient
- Government Scheme Patient

The patient proceeds to the Reception Counter.

---

## Step 2 – Registration

Reception verifies whether the patient already exists.

### Existing Patient

- Search using:
  - Hospital ID
  - Mobile Number
  - Aadhaar / Government ID
  - QR Code
  - Barcode

Patient record is retrieved.

### New Patient

Reception collects:

- Full Name
- Age
- Gender
- Date of Birth
- Mobile Number
- Email
- Address
- Blood Group
- Emergency Contact
- Aadhaar / Government ID
- Insurance Information
- Patient Photograph

The system generates:

- Hospital ID
- UHID (Unique Hospital ID)
- Barcode
- QR Code
- Digital Patient Card

All information is stored in the Electronic Health Record (EHR).

---

## Step 3 – OPD Registration Billing

The receptionist selects:

- Department
- Doctor
- Consultation Type
- Visit Type
- Insurance Category

The Billing Service calculates:

- Consultation Fee
- Registration Fee (if applicable)
- Taxes
- Discounts
- Insurance Coverage

The patient completes payment through:

- Cash
- UPI
- Credit Card
- Debit Card
- Net Banking
- Insurance
- Corporate Credit

After successful payment:

- Digital Receipt is generated.
- Invoice is stored.
- Billing record is created.

---

## Step 4 – Token Generation

The Queue Service automatically generates:

- OPD Token Number
- Queue Position
- Estimated Waiting Time
- Consultation Room

The patient receives:

- SMS
- Mobile App Notification
- Printed Token (optional)

The patient's status becomes:

WAITING_FOR_NURSE

---

## Step 5 – Nurse Assessment

The nurse scans the patient's barcode.

Immediately displayed:

- Patient Profile
- Allergies
- Previous Visits
- Medical History
- Current Medications

The nurse records:

- Height
- Weight
- Temperature
- Blood Pressure
- Pulse Rate
- Oxygen Saturation (SpO₂)
- Blood Sugar (if required)
- Pain Score
- Chief Complaint

The patient's status becomes:

READY_FOR_DOCTOR

---

## Step 6 – Doctor Consultation

The doctor opens the patient's EHR.

The doctor can view:

- Previous Visits
- Lab Reports
- Radiology Reports
- Current Medications
- Allergies
- Chronic Diseases
- Previous Surgeries
- Family History

The doctor performs:

- Clinical Examination
- Diagnosis
- Differential Diagnosis
- Clinical Notes

---

## Step 7 – Clinical Decision

The doctor decides one of the following:

1. Prescription Only

↓

Digital Prescription

↓

Pharmacy

↓

Patient Exit

---

2. Laboratory Investigation

↓

Digital Lab Request

↓

Laboratory

↓

Results Uploaded

↓

Doctor Reviews

---

3. Radiology Investigation

↓

Digital Radiology Request

↓

Radiology

↓

Report Uploaded

↓

Doctor Reviews

---

4. Specialist Referral

↓

Electronic Referral

↓

Selected Department

↓

New Queue Generated

---

5. Hospital Admission

↓

IPD Admission Request

↓

Bed Allocation

↓

Ward Transfer

---

6. Emergency Escalation

↓

Emergency Department

↓

Trauma / ICU

---

## Step 8 – Prescription

The doctor generates:

- Medicines
- Dosage
- Frequency
- Duration
- Food Instructions
- Follow-up Date

Prescription is digitally signed.

The Pharmacy receives the prescription instantly.

---

## Step 9 – Pharmacy

The pharmacist verifies:

- Prescription
- Allergies
- Drug Interactions
- Medicine Availability

Medicines are dispensed.

Inventory updates automatically.

---

## Step 10 – Patient Exit

The patient receives:

- Digital Prescription
- Investigation Reports
- Medical Certificate (if applicable)
- Follow-up Appointment
- Digital Invoice

The OPD visit is marked as:

COMPLETED