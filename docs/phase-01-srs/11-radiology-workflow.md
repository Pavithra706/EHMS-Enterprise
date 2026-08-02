# Radiology Information System (RIS) & PACS Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Hospital Business Blueprint |
| Document | Radiology Information System (RIS) & PACS Workflow |
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

The Radiology Information System (RIS) and Picture Archiving and Communication System (PACS) manage the complete medical imaging workflow from imaging request to image acquisition, interpretation, report generation, and long-term image storage.

---

# 2. Business Objective

The Radiology workflow aims to:

- Digitize radiology operations
- Eliminate paper-based imaging requests
- Manage imaging appointments
- Store DICOM images securely
- Integrate imaging reports with EHR
- Improve reporting turnaround time
- Support AI-assisted image analysis

---

# 3. Scope

The workflow includes:

- Imaging Request
- Appointment Scheduling
- Billing
- Patient Preparation
- Image Acquisition
- Image Processing
- Radiologist Review
- Report Approval
- Report Publishing
- PACS Storage

---

# 4. Actors

## Primary Actors

- Patient
- Doctor
- Radiology Technician
- Radiologist

## Secondary Actors

- Nurse
- Receptionist
- Billing Executive

## System Actors

- EHMS
- RIS Service
- PACS
- Billing Service
- Notification Service
- EHR Service

---

# 5. Preconditions

- Patient registered.
- Imaging ordered by doctor.
- Billing completed (unless emergency).
- Imaging equipment operational.
- PACS available.
- Radiologist available.

---

# 6. Main Radiology Workflow

## Step 1 – Imaging Request

Doctor requests imaging.

Examples:

- X-Ray
- CT Scan
- MRI
- Ultrasound
- Mammography
- PET Scan
- Fluoroscopy

Electronic imaging request generated.

---

## Step 2 – Appointment Scheduling

System checks:

- Machine availability
- Technician availability
- Radiologist availability

Appointment confirmed.

Emergency patients receive highest priority.

---

## Step 3 – Billing

Billing generated.

Supported payment:

- Cash
- UPI
- Card
- Insurance
- Corporate

Invoice stored.

---

## Step 4 – Patient Preparation

Technician verifies:

- Patient Identity
- UHID
- Barcode Wristband
- Imaging Request
- Pregnancy Status (where applicable)
- Contrast Allergy (if applicable)

Patient prepared for scan.

---

## Step 5 – Image Acquisition

Images captured using imaging modality.

Examples:

- Digital X-Ray
- CT
- MRI
- Ultrasound
- Mammography

Images stored in DICOM format.

---

## Step 6 – PACS Storage

Images automatically uploaded to PACS.

Stored information:

- Patient UHID
- Study ID
- Modality
- Body Part
- Acquisition Time
- Technician
- Image Series

---

## Step 7 – Radiologist Review

Radiologist reviews images.

Can perform:

- Measurements
- Image Comparison
- Annotation
- Findings
- Impression

---

## Step 8 – Report Generation

Radiologist prepares report.

Report includes:

- Clinical History
- Findings
- Impression
- Recommendations

Digital signature applied.

---

## Step 9 – Report Publishing

Report published to:

- Doctor Dashboard
- Patient Portal
- EHR

Notification sent automatically.

---

# 7. Alternative Workflows

## Emergency Imaging

Immediate scan.

Priority reporting.

---

## Portable Imaging

Portable X-Ray or Ultrasound performed at bedside.

---

## ICU Imaging

Dedicated priority workflow.

---

## OT Imaging

Real-time imaging during surgery.

---

## Follow-up Imaging

Previous studies compared automatically.

---

# 8. Exception Handling

## EX-001

Machine failure.

Action:

Assign alternate machine.

Notify Biomedical Engineering.

---

## EX-002

Patient unable to cooperate.

Action:

Doctor review.

Sedation if required.

---

## EX-003

Contrast reaction.

Action:

Emergency protocol activated.

Notify Emergency Team.

---

## EX-004

Image quality poor.

Action:

Repeat scan.

Document reason.

---

## EX-005

Critical finding.

Action:

Immediate doctor notification.

Critical alert generated.

---

# 9. Business Rules

BR-001

Every imaging study shall have a unique Study ID.

---

BR-002

All images shall be stored in PACS.

---

BR-003

Radiology reports require radiologist approval.

---

BR-004

Critical findings require immediate notification.

---

BR-005

Previous imaging shall remain permanently available.

---

BR-006

Every image modification shall generate an audit log.

---

# 10. Notifications

Automatic notifications:

- Imaging Scheduled
- Patient Ready
- Scan Started
- Scan Completed
- Report Ready
- Critical Finding
- Report Published

---

# 11. Future Database Entities

- ImagingOrder
- ImagingAppointment
- ImagingStudy
- PACSImage
- RadiologyReport
- RadiologistReview
- ImagingMachine
- ContrastAdministration
- CriticalFinding

---

# 12. Future REST APIs

POST /radiology/orders

GET /radiology/orders/{id}

POST /radiology/studies

POST /radiology/reports

GET /radiology/reports/{id}

GET /pacs/images/{studyId}

POST /critical-findings

---

# 13. Future UI Screens

- Radiology Dashboard
- Imaging Schedule
- PACS Viewer
- Report Editor
- Technician Dashboard
- Radiologist Dashboard
- Imaging Analytics

---

# 14. Role-Based Access Control (RBAC)

| Role | Permissions |
|------|-------------|
| Doctor | Request imaging, view reports |
| Technician | Perform imaging |
| Radiologist | Review and approve reports |
| Administrator | Full access |

---

# 15. Audit Logs

System records:

- Imaging Ordered
- Appointment Scheduled
- Scan Started
- Scan Completed
- Images Uploaded
- Report Created
- Report Approved
- Report Published

---

# 16. Key Performance Indicators (KPIs)

- Average Report Turnaround Time
- Machine Utilization
- Repeat Scan Rate
- Critical Finding Response Time
- Daily Imaging Volume
- Report Accuracy
- Patient Waiting Time

---

# 17. Future AI Features

The AI module may provide:

- Fracture Detection
- Brain Hemorrhage Detection
- Lung Nodule Detection
- Stroke Detection
- Tumor Detection
- Image Quality Assessment
- Automatic Priority Classification

---

# 18. Security Considerations

- Role-Based Access Control
- DICOM Security
- End-to-End Encryption
- Digital Signatures
- Audit Logging
- Secure PACS Access

---

# 19. Approval

| Role | Status |
|------|--------|
| Chief Radiologist | Pending |
| Radiology Manager | Pending |
| Hospital Administrator | Pending |
| System Architect | Pending |