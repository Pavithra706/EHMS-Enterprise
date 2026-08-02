# Laboratory Information System (LIS) Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Hospital Business Blueprint |
| Document | Laboratory Information System (LIS) Workflow |
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

# 1. Purpose

The Laboratory Information System (LIS) manages the complete lifecycle of laboratory investigations, including test ordering, billing, sample collection, barcode tracking, laboratory processing, quality control, result validation, and report publishing.

---

# 2. Business Objective

The Laboratory workflow aims to:

- Digitize laboratory operations
- Reduce turnaround time
- Eliminate manual errors
- Track samples using barcode technology
- Integrate with OPD, IPD, Emergency, OT, Billing, and EHR
- Maintain complete audit trails
- Provide secure digital laboratory reports

---

# 3. Scope

The workflow includes:

- Test Ordering
- Billing
- Sample Collection
- Barcode Generation
- Sample Transport
- Sample Processing
- Quality Control
- Result Entry
- Result Validation
- Report Publishing
- Critical Value Alerts

---

# 4. Actors

## Primary Actors

- Patient
- Doctor
- Laboratory Technician
- Phlebotomist
- Pathologist

## Secondary Actors

- Nurse
- Receptionist
- Billing Executive

## System Actors

- EHMS
- Laboratory Service
- Billing Service
- EHR Service
- Notification Service
- Barcode Scanner

---

# 5. Preconditions

- Patient is registered.
- Doctor has requested laboratory tests.
- Billing completed (unless emergency).
- Sample collection materials available.
- Laboratory equipment operational.
- Barcode printer available.

---

# 6. Main Laboratory Workflow

## Step 1 – Test Ordering

Doctor selects required laboratory tests.

Examples:

- CBC
- Blood Sugar
- Lipid Profile
- Liver Function Test
- Kidney Function Test
- Urine Analysis
- Culture & Sensitivity
- Histopathology
- Thyroid Profile

Electronic laboratory request is generated.

---

## Step 2 – Billing

Billing Service calculates charges.

Payment options:

- Cash
- UPI
- Card
- Insurance
- Corporate

Invoice generated.

---

## Step 3 – Sample Collection

Phlebotomist verifies:

- Patient Identity
- UHID
- Barcode
- Requested Tests

Required samples are collected.

Examples:

- Blood
- Urine
- Stool
- Sputum
- Tissue
- Swab

---

## Step 4 – Barcode Labeling

Each sample receives:

- Sample ID
- Patient UHID
- Test Name
- Collection Time
- Collector Name
- Barcode
- QR Code

---

## Step 5 – Sample Transport

Samples are transported to the laboratory.

Transport status:

- Collected
- In Transit
- Received
- Processing

---

## Step 6 – Laboratory Reception

Laboratory staff scans the barcode.

Sample integrity is checked:

- Correct Label
- Correct Container
- Adequate Volume
- No Leakage
- No Hemolysis

Accepted samples proceed for testing.

Rejected samples initiate recollection.

---

## Step 7 – Sample Processing

Samples are routed to departments:

- Hematology
- Biochemistry
- Microbiology
- Histopathology
- Immunology
- Molecular Diagnostics

Automated analyzers perform testing.

---

## Step 8 – Quality Control

Internal quality checks are performed.

Equipment calibration verified.

Abnormal analyzer errors are flagged.

---

## Step 9 – Result Entry

Laboratory Technician reviews analyzer results.

Results entered into EHMS.

Critical values are automatically flagged.

---

## Step 10 – Pathologist Validation

Pathologist reviews:

- Test Results
- Quality Control
- Clinical Correlation

Results digitally signed.

---

## Step 11 – Report Publishing

Final report published to:

- Patient Portal
- Doctor Dashboard
- EHR

Notifications sent automatically.

---

# 7. Alternative Workflows

## Emergency Laboratory

Critical samples receive highest priority.

---

## ICU Samples

Continuous urgent processing.

---

## OT Samples

Processed immediately during surgery.

---

## STAT Samples

Highest processing priority.

---

## Home Collection

Samples collected at patient residence.

---

# 8. Exception Handling

## EX-001

Sample mislabeled.

Action:

Reject sample.

Request recollection.

---

## EX-002

Insufficient sample.

Action:

Collect fresh sample.

---

## EX-003

Analyzer failure.

Action:

Redirect sample to backup analyzer.

Notify Biomedical Engineering.

---

## EX-004

Critical value detected.

Action:

Immediate doctor notification.

Document acknowledgment.

---

## EX-005

Sample lost.

Action:

Incident logged.

Recollection initiated.

---

# 9. Business Rules

BR-001

Every sample shall have a unique barcode.

---

BR-002

One barcode represents one collected specimen.

---

BR-003

Critical results require immediate notification.

---

BR-004

Reports require pathologist approval where applicable.

---

BR-005

Every sample movement shall be tracked.

---

BR-006

Rejected samples require recollection documentation.

---

# 10. Notifications

Automatic notifications:

- Test Ordered
- Sample Collected
- Sample Received
- Testing Started
- Report Ready
- Critical Result
- Report Published

---

# 11. Future Database Entities

- LaboratoryOrder
- LaboratoryTest
- Sample
- SampleTracking
- LaboratoryDepartment
- Analyzer
- QualityControl
- LaboratoryResult
- CriticalAlert
- LaboratoryReport

---

# 12. Future REST APIs

POST /laboratory/orders

GET /laboratory/orders/{id}

POST /samples

PUT /samples/{id}/status

POST /results

POST /reports/publish

GET /reports/{id}

---

# 13. Future UI Screens

- Laboratory Dashboard
- Sample Collection Screen
- Barcode Printing
- Sample Tracking
- Analyzer Dashboard
- Result Entry
- Pathologist Approval
- Laboratory Analytics

---

# 14. Role-Based Access Control (RBAC)

| Role | Permissions |
|------|-------------|
| Doctor | Order tests, view reports |
| Laboratory Technician | Process samples, enter results |
| Pathologist | Validate and approve reports |
| Nurse | Collect samples (where applicable) |
| Administrator | Full access |

---

# 15. Audit Logs

The system records:

- Test Ordered
- Sample Collected
- Barcode Printed
- Sample Received
- Sample Processed
- Result Entered
- Report Approved
- Report Published

---

# 16. Key Performance Indicators (KPIs)

- Average Turnaround Time (TAT)
- Sample Rejection Rate
- Critical Result Response Time
- Report Accuracy
- Analyzer Utilization
- Daily Test Volume
- Pending Reports

---

# 17. Future AI Features

The AI module may provide:

- Abnormal Result Detection
- Disease Risk Prediction
- Laboratory Workload Forecasting
- Quality Control Monitoring
- Analyzer Failure Prediction

---

# 18. Security Considerations

- Role-Based Access Control (RBAC)
- Barcode Verification
- Digital Signatures
- End-to-End Encryption
- Audit Logging
- Secure Report Access

---

# 19. Approval

| Role | Status |
|------|--------|
| Chief Pathologist | Pending |
| Laboratory Manager | Pending |
| Hospital Administrator | Pending |
| System Architect | Pending |