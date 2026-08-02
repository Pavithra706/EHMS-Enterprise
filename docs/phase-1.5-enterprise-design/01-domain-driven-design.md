# Domain-Driven Design (DDD)

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Domain-Driven Design (DDD) |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# 1. Purpose

This document defines the Domain-Driven Design (DDD) approach adopted by the Enterprise Hospital Management System (EHMS).

DDD ensures that the software architecture mirrors the real-world business structure of a super-specialty hospital. It divides the system into independent business domains with clear responsibilities, ownership, and boundaries.

---

# 2. Why Domain-Driven Design?

Hospital systems are extremely complex.

Instead of building one large application, EHMS separates business capabilities into domains.

Benefits include:

- Loose coupling
- High cohesion
- Independent deployment
- Better maintainability
- Scalability
- Clear ownership
- Easier testing
- Fault isolation

---

# 3. DDD Principles

EHMS follows these Domain-Driven Design principles:

- Ubiquitous Language
- Bounded Contexts
- Aggregates
- Entities
- Value Objects
- Domain Services
- Repositories
- Factories
- Domain Events
- Context Mapping

---

# 4. Enterprise Domain Classification

EHMS is divided into four major domain categories.

## 4.1 Core Domain

The Core Domain represents the primary healthcare operations.

Modules include:

- Patient Management
- OPD
- Emergency
- IPD
- ICU
- Operation Theatre
- Electronic Health Records (EHR)

---

## 4.2 Supporting Domain

Supports clinical operations.

Modules include:

- Laboratory
- Radiology
- Pharmacy
- Blood Bank
- Ambulance
- Telemedicine
- Nursing

---

## 4.3 Business Domain

Handles administration and finance.

Modules include:

- Billing
- Insurance
- HR
- Payroll
- Attendance
- Inventory
- Biomedical
- Maintenance
- Housekeeping
- Laundry
- Diet Management

---

## 4.4 Platform Domain

Provides enterprise-wide technical capabilities.

Modules include:

- Authentication
- Authorization
- Notification
- Analytics
- AI
- Audit
- Reporting
- File Storage
- Monitoring
- Logging

---

# 5. Enterprise Domain Hierarchy

```

EHMS

├── Core Domain
│ ├── Patient
│ ├── OPD
│ ├── Emergency
│ ├── IPD
│ ├── ICU
│ ├── OT
│ └── EHR
│
├── Supporting Domain
│ ├── Laboratory
│ ├── Radiology
│ ├── Pharmacy
│ ├── Blood Bank
│ ├── Ambulance
│ ├── Telemedicine
│ └── Nursing
│
├── Business Domain
│ ├── Billing
│ ├── Insurance
│ ├── HR
│ ├── Inventory
│ ├── Payroll
│ ├── Maintenance
│ └── Finance
│
└── Platform Domain
├── Authentication
├── Authorization
├── Notification
├── Analytics
├── AI
├── Audit
└── Reporting

```

---

# 6. Ubiquitous Language

All stakeholders must use common business terminology.

| Business Term | Meaning |
|--------------|----------|
| Patient | Individual receiving healthcare |
| Doctor | Licensed medical practitioner |
| Nurse | Registered nursing staff |
| Appointment | Scheduled consultation |
| Encounter | Clinical interaction |
| Admission | IPD registration |
| Prescription | Medication order |
| Investigation | Laboratory or Radiology order |
| Invoice | Financial bill |
| Claim | Insurance request |
| Bed | Assigned inpatient location |
| Ward | Hospital inpatient unit |
| Department | Functional hospital division |
| UHID | Unique Hospital Identifier |

---

# 7. Domain Ownership

Each domain has one owning service.

| Domain | Owner Service |
|---------|---------------|
| Patient | patient-service |
| OPD | opd-service |
| Emergency | emergency-service |
| IPD | ipd-service |
| Laboratory | laboratory-service |
| Pharmacy | pharmacy-service |
| Billing | billing-service |
| HR | hr-service |
| Analytics | analytics-service |
| AI | ai-service |

No other service directly modifies another domain's data.

Communication happens through APIs or events.

---

# 8. Domain Relationships

Core Domain

↓

Supporting Domain

↓

Business Domain

↓

Platform Domain

Platform services provide capabilities but do not own clinical data.

---

# 9. Domain Communication Principles

Communication follows:

- REST APIs for synchronous operations
- Event-driven messaging for asynchronous workflows
- Background jobs for long-running tasks
- Shared contracts for interoperability

Direct database access between services is prohibited.

---

# 10. Aggregate Design

Each aggregate has a single Aggregate Root.

Examples:

Patient Aggregate

Patient

↓

Appointments

↓

Admissions

↓

Medical History

↓

Allergies

Doctor Aggregate

Doctor

↓

Schedule

↓

Availability

↓

Appointments

Invoice Aggregate

Invoice

↓

Invoice Items

↓

Payments

↓

Refunds

---

# 11. Entity Examples

Entities possess unique identity.

Examples:

- Patient
- Doctor
- Employee
- Department
- Medicine
- Bed
- Appointment
- Admission
- Laboratory Order
- Invoice

---

# 12. Value Object Examples

Value Objects have no identity.

Examples:

- Address
- Phone Number
- Email
- Blood Pressure
- Temperature
- Height
- Weight
- Money
- Duration
- Coordinates

---

# 13. Domain Services

Domain services encapsulate business logic spanning multiple entities.

Examples:

- Appointment Scheduling Service
- Bed Allocation Service
- Billing Calculation Service
- Insurance Verification Service
- Laboratory Result Validation
- Drug Interaction Service

---

# 14. Repository Pattern

Each aggregate has its own repository.

Examples:

- PatientRepository
- DoctorRepository
- AppointmentRepository
- AdmissionRepository
- InvoiceRepository

Repositories abstract persistence from business logic.

---

# 15. Domain Events

Examples of business events:

- PatientRegistered
- AppointmentBooked
- PatientCheckedIn
- AdmissionCreated
- PrescriptionIssued
- LabOrderCreated
- LabResultCompleted
- RadiologyReportPublished
- InvoiceGenerated
- PaymentCompleted
- PatientDischarged

These events are published to the event bus for downstream processing.

---

# 16. Anti-Corruption Layer (ACL)

External systems integrate through an Anti-Corruption Layer.

Examples:

- Government Health Systems
- Insurance Portals
- Payment Gateways
- SMS Providers
- Email Providers
- Laboratory Devices
- PACS Systems

This layer protects the internal domain model from external differences.

---

# 17. Domain Independence Rules

Each domain:

- Owns its data.
- Owns its business rules.
- Owns its APIs.
- Owns its database schema.
- Can be deployed independently.
- Can be scaled independently.

---

# 18. Design Constraints

- No shared databases between services.
- No business logic in controllers.
- No direct service-to-service database queries.
- APIs must remain backward compatible where feasible.
- Events must be versioned when schemas evolve.

---

# 19. Future Evolution

The domain model should support:

- New hospital departments
- Additional AI services
- IoT medical devices
- Multi-hospital deployment
- Multi-tenancy
- Internationalization
- Cloud-native scaling

---

# 20. Conclusion

Domain-Driven Design establishes the architectural foundation of EHMS. By aligning software boundaries with hospital business capabilities, the system becomes modular, maintainable, scalable, and suitable for enterprise healthcare environments.