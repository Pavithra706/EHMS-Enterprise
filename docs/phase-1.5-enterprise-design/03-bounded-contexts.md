# Bounded Contexts

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Bounded Contexts |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the bounded contexts of the Enterprise Hospital Management System (EHMS).

A bounded context is an explicit boundary within which a particular domain model applies. Each bounded context owns its business rules, data, APIs, and lifecycle.

This document establishes service ownership and prevents tight coupling between modules.

---

# 1. Purpose

The objectives of bounded contexts are:

- Define ownership boundaries.
- Prevent shared business logic.
- Avoid shared databases.
- Support independent deployment.
- Enable autonomous development.
- Improve scalability.

---

# 2. Design Principles

EHMS follows these DDD principles:

- One business capability = One bounded context
- One bounded context = One primary owner
- One bounded context = One database schema
- Business logic never crosses context boundaries
- Communication occurs only through APIs or domain events

---

# 3. Enterprise Context Landscape

```
EHMS

├── Clinical Context
├── Diagnostic Context
├── Financial Context
├── Administration Context
├── Support Context
└── Platform Context
```

---

# 4. Clinical Context

## Purpose

Provides direct patient healthcare services.

### Bounded Contexts

- Patient
- Appointment
- OPD
- Emergency
- IPD
- ICU
- Operation Theatre
- Nursing
- EHR

### Primary Services

- patient-service
- appointment-service
- opd-service
- emergency-service
- ipd-service
- icu-service
- ot-service
- nurse-service
- ehr-service

---

# 5. Diagnostic Context

## Purpose

Supports diagnosis and investigations.

### Bounded Contexts

- Laboratory
- Radiology
- PACS
- Blood Bank

### Primary Services

- laboratory-service
- radiology-service
- pacs-service
- blood-bank-service

---

# 6. Financial Context

## Purpose

Handles financial operations.

### Bounded Contexts

- Billing
- Insurance
- Payment
- Revenue

### Primary Services

- billing-service
- insurance-service
- payment-service
- finance-service

---

# 7. Administration Context

## Purpose

Manages hospital administration.

### Bounded Contexts

- HR
- Attendance
- Payroll
- Inventory
- Biomedical
- Maintenance

### Primary Services

- hr-service
- attendance-service
- payroll-service
- inventory-service
- biomedical-service
- maintenance-service

---

# 8. Support Context

Provides operational support.

Bounded Contexts

- Ambulance
- Laundry
- Housekeeping
- Diet
- Security
- Visitor Management

Primary Services

- ambulance-service
- laundry-service
- housekeeping-service
- diet-service
- security-service
- visitor-service

---

# 9. Platform Context

Provides enterprise capabilities.

Contexts

- Authentication
- Authorization
- Notification
- Audit
- Analytics
- AI
- Reporting
- Storage
- Monitoring

Primary Services

- auth-service
- notification-service
- analytics-service
- ai-service
- reporting-service
- audit-service
- storage-service
- monitoring-service

---

# 10. Context Ownership Matrix

| Context | Owner | Shared? |
|----------|-------|---------|
| Patient | patient-service | No |
| Appointment | appointment-service | No |
| Laboratory | laboratory-service | No |
| Billing | billing-service | No |
| Pharmacy | pharmacy-service | No |
| HR | hr-service | No |
| Inventory | inventory-service | No |
| Analytics | analytics-service | Read-only |
| AI | ai-service | Read-only |

---

# 11. Context Communication

Contexts communicate using:

### Synchronous

- REST APIs

### Asynchronous

- Domain Events

### Long-running

- Background Jobs

### Notifications

- Event Bus

---

# 12. Shared Kernel

The following are shared through common libraries, **not databases**.

Shared Types

- UHID
- EmployeeID
- DepartmentCode
- Money
- Address
- ContactInfo
- Pagination
- API Response Models

Location

```
packages/

shared-types

shared-constants

validators
```

---

# 13. Customer–Supplier Relationships

| Customer | Supplier |
|-----------|----------|
| OPD | Patient |
| Emergency | Patient |
| Laboratory | OPD |
| Pharmacy | Doctor |
| Billing | All Clinical Modules |
| Analytics | All Services |

---

# 14. Conformist Relationships

External integrations conform to external standards.

Examples

- Payment Gateway
- SMS Provider
- Email Provider
- Government Health Systems
- Insurance APIs

---

# 15. Anti-Corruption Layers

ACL protects EHMS from external models.

External Systems

↓

ACL

↓

EHMS Domain

Examples

- PACS
- LIS Devices
- Government APIs
- Insurance Portals
- Payment Gateways

---

# 16. Open Host Services

Some services expose public interfaces.

Examples

- Authentication API
- Patient API
- Appointment API
- Billing API
- Reporting API

---

# 17. Published Language

All service communication follows:

- REST
- OpenAPI 3
- JSON
- JWT
- OAuth2
- Async Events

---

# 18. Data Ownership Rules

Each bounded context owns:

- Database
- Tables
- Business Rules
- APIs
- Events

Other services must never directly update another context's database.

---

# 19. Context Evolution

Future contexts may include:

- Oncology
- Cardiology
- Neurology
- Organ Transplant
- Clinical Research
- Home Healthcare
- Genomics
- IoT Devices

The architecture must support adding these without modifying existing contexts.

---

# 20. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Independent contexts | Loose coupling |
| Database per service | Data ownership |
| Event-driven integration | Scalability |
| API-first communication | Standardization |
| Shared contracts only | Prevent tight coupling |

---

# 21. Risks

| Risk | Mitigation |
|------|------------|
| Context overlap | Clear ownership |
| Duplicate models | Canonical data model |
| Tight coupling | Event-driven communication |
| Shared database | Database-per-service policy |

---

# 22. Related Documents

- 01 Domain-Driven Design
- 02 Business Capability Model
- 04 Context Map
- 06 Microservice Architecture
- 13 Canonical Data Model

---

# 23. Conclusion

The bounded context model establishes the architectural boundaries of EHMS.

Every microservice, database schema, API, event, and deployment strategy in the project will align with these context boundaries. This ensures the platform remains modular, maintainable, scalable, and adaptable as new hospital capabilities are introduced.