# Pharmacy Information System (PIS) Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Enterprise Functional Specification |
| Module | Pharmacy Information System (PIS) |
| Version | 2.0 |
| Status | Draft |
| Author | Pavithra K V |

---

# 1. Purpose

The Pharmacy Information System (PIS) manages the complete medication lifecycle, including prescription validation, inventory management, dispensing, billing, stock monitoring, expiry tracking, and integration with the Electronic Health Record (EHR).

---

# 2. Business Objective

The Pharmacy module aims to:

- Digitize medication dispensing
- Prevent medication errors
- Detect drug interactions
- Detect allergy conflicts
- Track medicine inventory
- Reduce medicine wastage
- Improve patient safety
- Integrate with all clinical departments

---

# 3. Scope

The workflow covers:

- Prescription Processing
- Medication Verification
- Inventory Checking
- Drug Interaction Checking
- Allergy Checking
- Medicine Dispensing
- Barcode Verification
- Billing
- Inventory Updates
- Medicine Returns
- Expiry Monitoring

---

# 4. Actors

## Primary

- Doctor
- Pharmacist
- Patient

## Secondary

- Nurse
- Billing Executive
- Inventory Manager

## System

- EHMS
- Pharmacy Service
- Inventory Service
- Billing Service
- AI Service
- Notification Service
- EHR Service

---

# 5. Preconditions

- Patient registered.
- Valid prescription available.
- Pharmacist logged in.
- Inventory synchronized.
- Billing available.

---

# 6. Main Workflow

Step 1

Doctor generates digital prescription.

↓

Prescription Service

↓

Pharmacy receives order.

---

Step 2

Prescription Validation

Verify

- Doctor Signature
- Patient Identity
- Medicine Availability
- Prescription Validity

---

Step 3

Clinical Validation

Check

- Allergy
- Drug Interaction
- Duplicate Therapy
- Contraindications
- Maximum Dose
- Pediatric Dose
- Pregnancy Safety

AI assists pharmacist.

---

Step 4

Inventory Check

Verify

- Stock Available
- Batch Number
- Expiry Date
- Storage Conditions

Nearest batch selected using FEFO.

(First Expiry First Out)

---

Step 5

Medicine Picking

Medicine picked.

Barcode scanned.

↓

Patient barcode scanned.

↓

Medicine matched.

---

Step 6

Dispensing

Medicine dispensed.

Inventory reduced.

Dispensing record created.

---

Step 7

Patient Counseling

Pharmacist explains

- Dosage
- Frequency
- Duration
- Food Instructions
- Side Effects
- Storage

---

Step 8

EHR Update

Medication history updated.

Doctor notified.

Patient mobile app updated.

---

# 7. Workflow State Machine

PRESCRIBED

↓

VALIDATED

↓

INVENTORY_VERIFIED

↓

PICKED

↓

DISPENSED

↓

COMPLETED

---

# 8. Event Flow

Doctor Service

↓

Pharmacy Service

↓

Inventory Service

↓

Billing Service

↓

Notification Service

↓

EHR Service

↓

Analytics Service

---

# 9. Alternative Workflows

Emergency Medicine

↓

Immediate Dispense

↓

Billing Later

---

Controlled Drugs

↓

Identity Verification

↓

Approval

↓

Dispense

---

Medicine Return

↓

Verification

↓

Inventory

↓

Refund

---

# 10. Exception Handling

PHR-EX-001

Medicine Out of Stock

Action

Suggest alternatives.

---

PHR-EX-002

Expired Medicine

Action

Block dispensing.

---

PHR-EX-003

Drug Interaction

Action

Notify doctor.

---

PHR-EX-004

Allergy Detected

Action

Block dispensing.

---

PHR-EX-005

Barcode Mismatch

Action

Reject dispensing.

---

# 11. Business Rules

PHR-BR-001

Prescription mandatory.

---

PHR-BR-002

Barcode verification mandatory.

---

PHR-BR-003

Expired medicines cannot be dispensed.

---

PHR-BR-004

Controlled drugs require authorization.

---

PHR-BR-005

Inventory updates in real time.

---

# 12. Business Validation Rules

Medicine exists.

Batch active.

Stock > 0.

Expiry valid.

Prescription active.

Patient verified.

---

# 13. Error Codes

PHR001

Medicine unavailable

PHR002

Expired medicine

PHR003

Duplicate dispensing

PHR004

Drug interaction

PHR005

Patient allergy

PHR006

Barcode mismatch

---

# 14. Notifications

- Prescription Received
- Medicine Ready
- Medicine Dispensed
- Low Stock
- Expiry Alert
- Controlled Drug Dispensed

---

# 15. Integration Points

- OPD
- Emergency
- IPD
- ICU
- OT
- Billing
- Inventory
- AI
- EHR

---

# 16. Database Relationships

Patient

↓

Prescription

↓

PrescriptionItem

↓

Medicine

↓

Inventory

↓

DispenseRecord

---

# 17. Future Database Tables

- Prescription
- PrescriptionItem
- Medicine
- Batch
- Inventory
- Dispense
- DrugInteraction
- Allergy
- PharmacyAudit

---

# 18. REST APIs

POST /prescriptions

GET /prescriptions/{id}

POST /dispense

GET /inventory

PUT /inventory

POST /returns

---

# 19. UI Screens

- Pharmacy Dashboard
- Prescription Queue
- Dispensing Screen
- Inventory Dashboard
- Expiry Dashboard
- Controlled Drug Register

---

# 20. RBAC Matrix

| Role | Permission |
|-------|------------|
| Pharmacist | Dispense Medicines |
| Doctor | Create Prescription |
| Nurse | View Medication |
| Admin | Full Access |

---

# 21. Audit Logs

- Prescription Received
- Inventory Verified
- Medicine Dispensed
- Return Processed
- Inventory Updated

---

# 22. KPIs

- Average Dispensing Time
- Medicine Availability
- Stock Accuracy
- Expiry Percentage
- Prescription Error Rate
- Daily Dispensing Count

---

# 23. SLA

Prescription Verification ≤ 2 min

Medicine Dispensing ≤ 5 min

Emergency Medicine ≤ 2 min

Inventory Update Real-Time

---

# 24. Future AI Features

- Drug Interaction Detection
- Allergy Prediction
- Inventory Forecasting
- Expiry Prediction
- Prescription Error Detection

---

# 25. Healthcare Standards

- HL7
- FHIR MedicationRequest
- ATC Classification
- RxNorm (Future)

---

# 26. Microservice Mapping

Primary

↓

pharmacy-service

Connected Services

↓

inventory-service

↓

billing-service

↓

notification-service

↓

ehr-service

↓

analytics-service

↓

ai-service

---

# 27. Security

- RBAC
- MFA
- Audit Logs
- Encryption
- Digital Prescription
- Barcode Verification

---

# 28. Approval

| Role | Status |
|------|--------|
| Chief Pharmacist | Pending |
| Pharmacy Manager | Pending |
| Hospital Administrator | Pending |
| System Architect | Pending |