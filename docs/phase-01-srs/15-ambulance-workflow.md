# Ambulance & Fleet Management System (AFMS)

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Enterprise Functional Specification |
| Module | Ambulance & Fleet Management System |
| Version | 2.0 |
| Status | Draft |
| Author | Pavithra K V |

---

# 1. Purpose

The Ambulance & Fleet Management System manages ambulance dispatch, GPS tracking, emergency response, patient transportation, fleet maintenance, driver management, and emergency communication while integrating with hospital emergency services and Electronic Health Records (EHR).

---

# 2. Business Objective

The Ambulance module aims to:

- Digitize ambulance dispatch.
- Reduce emergency response time.
- Track ambulances in real time.
- Improve coordination between ambulance and hospital.
- Support emergency patient care.
- Maintain fleet maintenance records.
- Integrate with Emergency, ICU, Billing, and EHR.

---

# 3. Scope

The workflow covers:

- Ambulance Request
- Emergency Dispatch
- GPS Tracking
- Driver Assignment
- Patient Pickup
- En-route Monitoring
- Hospital Arrival
- Patient Handover
- Billing
- Fleet Maintenance

---

# 4. Actors

## Primary

- Patient
- Ambulance Driver
- Paramedic
- Emergency Doctor
- Dispatch Officer

## Secondary

- Hospital Administrator
- Billing Executive
- Fleet Manager

## System

- EHMS
- Ambulance Service
- GPS Service
- Notification Service
- Billing Service
- EHR Service
- Analytics Service

---

# 5. Preconditions

- Ambulance available.
- Driver assigned.
- GPS device operational.
- Communication system active.
- Emergency department operational.

---

# 6. Main Workflow

## Step 1 – Ambulance Request

Request received through:

- Emergency Call
- Patient App
- Reception
- Referral Hospital

Request recorded.

↓

Dispatch Queue Created.

---

## Step 2 – Dispatch

System identifies:

- Nearest Ambulance
- Driver Availability
- Paramedic Availability
- Ambulance Type

Examples:

- Basic Life Support (BLS)
- Advanced Life Support (ALS)
- ICU Ambulance
- Neonatal Ambulance

Dispatch confirmed.

---

## Step 3 – GPS Tracking

GPS activated.

Track:

- Current Location
- Estimated Arrival Time (ETA)
- Route
- Speed
- Distance

Live updates visible to dispatcher.

---

## Step 4 – Patient Pickup

Driver reaches location.

Verify:

- Patient Identity
- Emergency Details
- Destination Hospital

Patient loaded.

Status:

PATIENT_ONBOARD

---

## Step 5 – En-route Care

Paramedic records:

- Blood Pressure
- Pulse
- Oxygen Saturation
- ECG (if available)
- Medications Given
- Procedures Performed

Emergency doctor notified if required.

---

## Step 6 – Hospital Arrival

Emergency department alerted.

Patient handed over.

Digital handover completed.

---

## Step 7 – Billing

Calculate:

- Distance
- Ambulance Type
- Waiting Time
- Medical Equipment Used
- Emergency Charges

Invoice generated.

---

## Step 8 – Fleet Update

Ambulance marked:

- Available
- Cleaning Required
- Maintenance Required
- Refueling Required

Fleet dashboard updated.

---

# 7. Workflow State Machine

REQUESTED

↓

DISPATCHED

↓

EN_ROUTE

↓

PATIENT_ONBOARD

↓

ARRIVED

↓

HANDOVER_COMPLETED

↓

AVAILABLE

---

# 8. Event Flow

Emergency Service

↓

Ambulance Service

↓

GPS Service

↓

Notification Service

↓

Emergency Department

↓

Billing Service

↓

EHR Service

↓

Analytics Service

---

# 9. Alternative Workflows

- Inter-Hospital Transfer
- ICU Transfer
- Neonatal Transport
- Organ Transport
- Disaster Response
- Mass Casualty Incident (MCI)

---

# 10. Exception Handling

AMB-EX-001

No Ambulance Available

↓

Dispatch nearest partner ambulance.

---

AMB-EX-002

Vehicle Breakdown

↓

Dispatch backup ambulance.

---

AMB-EX-003

GPS Failure

↓

Manual tracking initiated.

---

AMB-EX-004

Patient Declines Transport

↓

Record refusal.

↓

Close request.

---

AMB-EX-005

Road Block

↓

Alternate route suggested.

---

# 11. Business Rules

AMB-BR-001

Every dispatch shall have a unique Dispatch ID.

---

AMB-BR-002

Every ambulance shall have GPS enabled.

---

AMB-BR-003

Patient handover requires digital confirmation.

---

AMB-BR-004

Fleet maintenance schedules shall be tracked.

---

AMB-BR-005

Emergency requests receive highest priority.

---

# 12. Business Validation Rules

- Ambulance available.
- Driver assigned.
- GPS active.
- Patient verified.
- Destination confirmed.

---

# 13. Error Codes

AMB001 Ambulance Unavailable

AMB002 Driver Unavailable

AMB003 GPS Offline

AMB004 Dispatch Failed

AMB005 Maintenance Overdue

---

# 14. Notifications

- Ambulance Requested
- Ambulance Dispatched
- Driver Assigned
- Ambulance Arrived
- Patient Onboard
- Hospital Notified
- Patient Handover Completed
- Fleet Maintenance Due

---

# 15. Integration Points

- Emergency
- ICU
- OPD
- IPD
- Billing
- EHR
- Analytics
- AI
- GPS Provider

---

# 16. Database Relationships

Ambulance

↓

Dispatch

↓

Driver

↓

Patient

↓

Trip

↓

Billing

↓

Maintenance

---

# 17. Future Database Tables

- Ambulance
- Driver
- Dispatch
- Trip
- GPSLocation
- FleetMaintenance
- FuelLog
- PatientTransport
- AmbulanceEquipment

---

# 18. REST APIs

POST /ambulance/request

POST /ambulance/dispatch

GET /ambulance/location/{id}

PUT /ambulance/status

POST /ambulance/handover

GET /fleet

POST /maintenance

---

# 19. UI Screens

- Emergency Dispatch Dashboard
- GPS Live Tracking
- Ambulance Status Board
- Fleet Dashboard
- Driver Dashboard
- Maintenance Dashboard

---

# 20. RBAC Matrix

| Role | Permission |
|------|------------|
| Dispatcher | Assign Ambulance |
| Driver | Update Trip Status |
| Paramedic | Record Patient Care |
| Fleet Manager | Manage Fleet |
| Administrator | Full Access |

---

# 21. Audit Logs

- Request Received
- Ambulance Assigned
- GPS Activated
- Patient Picked Up
- Hospital Arrival
- Handover Completed
- Maintenance Recorded

---

# 22. KPIs

- Average Response Time
- Average Transport Time
- Fleet Utilization
- Ambulance Availability
- Dispatch Accuracy
- Maintenance Compliance

---

# 23. SLA

Emergency Dispatch ≤ 2 minutes

Average Response Time ≤ 8 minutes

GPS Update Interval ≤ 10 seconds

Fleet Status Update Real-Time

---

# 24. Future AI Features

- Ambulance Demand Prediction
- Route Optimization
- Traffic-Aware Dispatch
- Predictive Vehicle Maintenance
- Emergency Resource Allocation

---

# 25. Healthcare Standards

- HL7 FHIR Encounter
- HL7 FHIR Patient
- ICD-10
- GPS Integration Standards

---

# 26. Microservice Mapping

Primary

↓

ambulance-service

Connected Services

↓

emergency-service

↓

notification-service

↓

billing-service

↓

ehr-service

↓

analytics-service

↓

ai-service

---

# 27. Security

- Role-Based Access Control
- GPS Data Encryption
- Digital Handover Confirmation
- Secure Communication
- Audit Logs

---

# 28. Approval

| Role | Status |
|------|--------|
| Emergency Medical Services Manager | Pending |
| Fleet Manager | Pending |
| Hospital Administrator | Pending |
| System Architect | Pending |