# Business Capability Model

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Business Capability Model |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the business capabilities of the Enterprise Hospital Management System (EHMS).

A business capability represents **what the hospital must be able to do**, independent of technology, implementation, organizational structure, or software design.

The capability model provides the foundation for Domain-Driven Design (DDD), bounded contexts, microservice decomposition, API ownership, and database ownership.

---

# 1. Purpose

The Business Capability Model aims to:

- Identify every business capability of the hospital.
- Separate business concerns.
- Define ownership boundaries.
- Improve scalability.
- Enable modular development.
- Prepare for microservice architecture.

---

# 2. Goals

The capability model should:

- Reflect real hospital operations.
- Be technology independent.
- Support future expansion.
- Minimize coupling.
- Maximize cohesion.
- Enable service ownership.

---

# 3. Non-Goals

This document does NOT define:

- Database schema
- REST APIs
- UI Design
- Deployment
- Implementation details

Those are covered in later documents.

---

# 4. Capability Levels

EHMS capabilities are divided into three levels.

Level 1

Enterprise Capability

↓

Level 2

Business Capability

↓

Level 3

Business Function

---

# 5. Enterprise Capability Map

EHMS

├── Clinical Services

├── Diagnostic Services

├── Administrative Services

├── Financial Services

├── Support Services

└── Platform Services

---

# 6. Clinical Services

Purpose

Deliver healthcare services.

Business Capabilities

- Patient Management
- Registration
- OPD
- Emergency
- IPD
- ICU
- OT
- Nursing
- EHR

Business Functions

Patient Registration

↓

Appointment

↓

Consultation

↓

Admission

↓

Treatment

↓

Discharge

---

# 7. Diagnostic Services

Capabilities

- Laboratory
- Radiology
- PACS
- Blood Bank

Functions

Order Investigation

↓

Sample Collection

↓

Testing

↓

Reporting

↓

Doctor Review

---

# 8. Pharmacy Services

Capabilities

- Drug Inventory
- Prescription Management
- Drug Dispensing
- Controlled Drug Management

Functions

Prescription

↓

Verification

↓

Dispensing

↓

Billing

↓

Inventory Update

---

# 9. Financial Services

Capabilities

- Billing
- Insurance
- Payment
- Revenue Management
- Financial Reporting

Functions

Invoice

↓

Payment

↓

Claim

↓

Settlement

↓

Accounting

---

# 10. Administrative Services

Capabilities

- HR
- Attendance
- Payroll
- Recruitment
- Performance Management

Functions

Recruit

↓

Onboard

↓

Attendance

↓

Payroll

↓

Exit

---

# 11. Support Services

Capabilities

- Inventory
- Biomedical
- Laundry
- Housekeeping
- Diet Management
- Maintenance
- Ambulance

Functions

Request

↓

Assignment

↓

Completion

↓

Verification

---

# 12. Platform Services

Capabilities

- Authentication
- Authorization
- Notification
- Analytics
- AI
- Audit
- Monitoring
- Reporting

Functions

Authenticate

↓

Authorize

↓

Notify

↓

Monitor

↓

Analyze

---

# 13. Capability Ownership

| Capability | Owner |
|------------|-------|
| Patient | patient-service |
| Appointment | appointment-service |
| OPD | opd-service |
| Emergency | emergency-service |
| IPD | ipd-service |
| Laboratory | laboratory-service |
| Radiology | radiology-service |
| Pharmacy | pharmacy-service |
| Billing | billing-service |
| HR | hr-service |
| Inventory | inventory-service |
| Analytics | analytics-service |
| AI | ai-service |

---

# 14. Capability Dependencies

Clinical

↓

Diagnostics

↓

Billing

↓

Analytics

↓

Reporting

Platform services support every capability.

---

# 15. Cross-Cutting Capabilities

The following apply across all modules:

- Authentication
- Authorization
- Audit Logging
- Notifications
- File Storage
- Monitoring
- Reporting
- AI
- Analytics

---

# 16. Business Capability Matrix

| Capability | Criticality | Availability |
|------------|------------|--------------|
| Emergency | Critical | 24×7 |
| OPD | High | Business Hours |
| IPD | Critical | 24×7 |
| Laboratory | Critical | 24×7 |
| Pharmacy | Critical | 24×7 |
| Billing | High | 24×7 |
| HR | Medium | Office Hours |
| Analytics | High | 24×7 |

---

# 17. Design Constraints

- Each capability owns its business logic.
- Capabilities communicate only through contracts.
- No shared business logic.
- No shared database.
- Independent deployment.

---

# 18. Future Expansion

The capability model supports future additions including:

- Organ Transplant Management
- Oncology Center
- Robotic Surgery
- Home Healthcare
- Wearable Device Integration
- Genomics
- Clinical Research
- Multi-Hospital Management

---

# 19. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Capability-based decomposition | Better modularity |
| Domain ownership | Clear responsibilities |
| Independent services | Better scalability |
| API-first communication | Loose coupling |
| Event-driven integration | Improved resilience |

---

# 20. Risks

| Risk | Mitigation |
|------|------------|
| Capability overlap | Clear ownership |
| Tight coupling | Event-driven communication |
| Duplicate logic | Shared standards |
| Future expansion | Modular capability model |

---

# 21. Related Documents

- 00 Enterprise Design Overview
- 01 Domain-Driven Design
- 03 Bounded Contexts
- 04 Context Map
- 06 Microservice Architecture

---

# 22. Conclusion

The Business Capability Model provides the business blueprint for EHMS.

It ensures every capability has clear ownership, defined responsibilities, and enterprise scalability while serving as the bridge between hospital operations and software architecture.