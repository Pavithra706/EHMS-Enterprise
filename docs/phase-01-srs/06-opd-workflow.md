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

# 7. Alternative Workflows

## 7.1 Follow-up Patient

The patient returns for a scheduled follow-up consultation.

Workflow:

- Search using UHID / QR Code
- Retrieve previous consultation
- Skip new registration
- OPD billing for follow-up consultation
- Generate new token
- Doctor reviews previous treatment
- Update prescription
- Schedule next follow-up if required

---

## 7.2 Appointment Patient

Patients with prior appointments:

- Appointment verified
- Queue priority assigned
- Registration confirmed
- Token generated
- Consultation proceeds

---

## 7.3 Insurance Patient

Additional verification:

- Insurance policy validation
- Coverage verification
- Cashless approval (if applicable)
- Billing routed through Insurance Service

---

## 7.4 Corporate Patient

- Employee ID verification
- Corporate agreement validation
- Employer billing
- Consultation proceeds normally

---

## 7.5 Senior Citizen / Disabled Patient

Priority queue is automatically assigned.

Special assistance is provided.

---

## 7.6 VIP Patient

Restricted visibility.

Special waiting area.

Priority consultation.

Enhanced privacy controls.

# 8. Exception Handling

## EX-001

Doctor unavailable.

Action:

- Notify Reception.
- Assign another doctor.
- Inform patient.

---

## EX-002

Payment failure.

Action:

- Retry payment.
- Select another payment method.
- Hold token generation until payment succeeds.

---

## EX-003

Barcode unreadable.

Action:

Search using:

- UHID
- Mobile Number
- Aadhaar
- QR Code

---

## EX-004

Laboratory system unavailable.

Action:

- Queue investigation.
- Notify Laboratory.
- Alert doctor.

---

## EX-005

Radiology delay.

Action:

- Notify patient.
- Update expected completion time.

---

## EX-006

Patient condition worsens.

Action:

Immediately transfer patient to Emergency Department.

Generate Emergency Case ID.

Notify Emergency Team.
# 9. Business Rules

BR-001

Every patient shall have a Unique Hospital ID (UHID).

---

BR-002

Every OPD visit shall create a consultation record.

---

BR-003

Every consultation shall be digitally signed.

---

BR-004

Only assigned doctors may modify consultation records.

---

BR-005

Every prescription shall be electronic.

---

BR-006

Every laboratory request shall originate from a doctor.

---

BR-007

All referrals shall be electronically recorded.

---

BR-008

Every patient movement shall generate an audit log.

---

BR-009

Payment must be completed before consultation unless exempted.

---

BR-010

Emergency patients bypass OPD billing.
# 10. Notifications

The Notification Service generates alerts for:

- Token Generated
- Queue Updated
- Doctor Ready
- Investigation Requested
- Laboratory Report Ready
- Radiology Report Ready
- Prescription Generated
- Medicine Ready
- Follow-up Reminder
- Appointment Reminder
- Billing Completed

# 11. Future Database Entities

The following database tables will support OPD:

- Patient
- Appointment
- OPDVisit
- Consultation
- Queue
- Token
- VitalSigns
- ClinicalNote
- Prescription
- Referral
- LaboratoryRequest
- RadiologyRequest
- Billing
- Invoice
- Payment
- AuditLog# 12. Future REST APIs

Patient APIs

POST /patients

GET /patients/{id}

PUT /patients/{id}

---

Appointment APIs

POST /appointments

GET /appointments

---

Queue APIs

POST /queue/token

GET /queue/status

---

Consultation APIs

POST /consultations

GET /consultations/{id}

---

Prescription APIs

POST /prescriptions

GET /prescriptions/{id}

---

Referral APIs

POST /referrals

GET /referrals

# 13. Future UI Screens

Reception Dashboard

Billing Dashboard

Queue Dashboard

Doctor Dashboard

Nurse Dashboard

Patient Dashboard

Laboratory Dashboard

Radiology Dashboard

Pharmacy Dashboard

Administrator Dashboard
# 14. Key Performance Indicators (KPIs)

The OPD monitors:

- Average Registration Time
- Average Waiting Time
- Average Consultation Time
- Average Billing Time
- Daily OPD Count
- Referral Rate
- Laboratory Request Rate
- Radiology Request Rate
- Patient Satisfaction Score
- Follow-up Compliance Rate

# 15. Approval

| Role | Status |
|------|--------|
| Hospital Administrator | Pending |
| Chief Medical Officer | Pending |
| IT Administrator | Pending |
| System Architect | Pending |
| Development Team | Pending |