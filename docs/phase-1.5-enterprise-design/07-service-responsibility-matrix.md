# Service Responsibility Matrix

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Service Responsibility Matrix |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the responsibility of every microservice in the Enterprise Hospital Management System (EHMS).

Each service has a clearly defined ownership boundary that includes:

- Business capability
- Database ownership
- API ownership
- Domain events
- Dependencies
- Implementation phase
- Criticality

The matrix prevents overlapping responsibilities and promotes loose coupling.

---

# 1. Purpose

The Service Responsibility Matrix aims to:

- Clearly define service ownership.
- Avoid duplicate business logic.
- Identify dependencies.
- Simplify implementation.
- Improve maintainability.
- Support independent deployment.

---

# 2. Responsibility Principles

Every microservice:

- Owns one business capability.
- Owns one database schema.
- Owns its REST APIs.
- Publishes domain events.
- Consumes required events.
- Never directly modifies another service's database.

---

# 3. Responsibility Matrix

| Service | Primary Responsibility | Owns Data | Phase | Criticality |
|----------|------------------------|-----------|--------|-------------|
| api-gateway | Request routing | No | A | Critical |
| auth-service | Authentication | Users, Tokens | A | Critical |
| user-service | User profiles | Users | A | High |
| notification-service | Notifications | Notification Logs | A | High |
| patient-service | Patient records | Patients | A | Critical |
| doctor-service | Doctor profiles | Doctors | A | Critical |
| appointment-service | Appointments | Appointments | A | Critical |
| opd-service | OPD workflow | OPD Visits | A | Critical |
| emergency-service | Emergency workflow | Emergency Cases | A | Critical |
| ipd-service | Admissions | Admissions | A | Critical |
| ehr-service | Medical records | Clinical Records | A | Critical |
| laboratory-service | Laboratory workflow | Lab Orders & Results | A | Critical |
| radiology-service | Radiology workflow | Imaging Orders | A | Critical |
| pharmacy-service | Medication management | Medicines & Dispensing | A | Critical |
| billing-service | Billing | Invoices | A | Critical |
| analytics-service | Reporting & KPIs | Analytics Data | A | High |
| blood-bank-service | Blood management | Blood Units | B | High |
| ambulance-service | Ambulance operations | Dispatch Records | B | High |
| insurance-service | Insurance claims | Claims | B | High |
| inventory-service | Stock management | Inventory | B | High |
| hr-service | Human resources | Employees | B | High |
| attendance-service | Attendance | Attendance | B | Medium |
| payroll-service | Payroll | Payroll | B | Medium |
| biomedical-service | Equipment | Equipment | B | Medium |
| maintenance-service | Facility maintenance | Maintenance | B | Medium |
| queue-service | Queue management | Queue Tokens | B | Medium |
| reporting-service | Report generation | Reports | B | Medium |
| audit-service | Audit logs | Audit Records | B | High |
| ai-service | AI predictions | AI Models & Predictions | B | High |

---

# 4. API Ownership

Each service exposes only its own APIs.

Examples:

| Service | API Prefix |
|----------|------------|
| patient-service | /patients |
| doctor-service | /doctors |
| appointment-service | /appointments |
| laboratory-service | /laboratory |
| billing-service | /billing |
| pharmacy-service | /pharmacy |

No service exposes another service's business functionality.

---

# 5. Database Ownership

Every service owns its own schema.

| Service | Database Schema |
|----------|-----------------|
| patient-service | patient_db |
| appointment-service | appointment_db |
| laboratory-service | laboratory_db |
| billing-service | billing_db |
| hr-service | hr_db |

Cross-service joins are prohibited.

---

# 6. Event Ownership

| Service | Publishes |
|----------|-----------|
| patient-service | PatientRegistered |
| appointment-service | AppointmentBooked |
| laboratory-service | LabResultReady |
| pharmacy-service | MedicineDispensed |
| billing-service | InvoiceGenerated |
| payment-service* | PaymentCompleted |

> *Payment functionality may initially be implemented within `billing-service` during Phase A and later separated into a dedicated `payment-service` as the platform grows.

---

# 7. Event Consumers

| Service | Consumes |
|----------|----------|
| notification-service | All business events |
| analytics-service | All business events |
| audit-service | All business events |
| ai-service | Clinical events |

---

# 8. Dependency Matrix

| Service | Depends On |
|----------|------------|
| appointment-service | patient-service, doctor-service |
| opd-service | appointment-service |
| emergency-service | patient-service |
| laboratory-service | opd-service, ipd-service |
| radiology-service | opd-service, ipd-service |
| pharmacy-service | ehr-service |
| billing-service | All clinical services |
| analytics-service | All services |

---

# 9. Service Lifecycle

Every service follows:

Planning

↓

Design

↓

Development

↓

Testing

↓

Deployment

↓

Monitoring

↓

Maintenance

---

# 10. Implementation Roadmap

## Phase A – Core Services

- api-gateway
- auth-service
- user-service
- notification-service
- patient-service
- doctor-service
- appointment-service
- opd-service
- emergency-service
- ipd-service
- ehr-service
- laboratory-service
- radiology-service
- pharmacy-service
- billing-service
- analytics-service

---

## Phase B – Enterprise Expansion

- blood-bank-service
- ambulance-service
- insurance-service
- inventory-service
- hr-service
- attendance-service
- payroll-service
- biomedical-service
- maintenance-service
- queue-service
- reporting-service
- audit-service
- ai-service

---

## Phase C – Advanced Features

- Multi-hospital services
- Home healthcare
- IoT gateway
- Clinical research
- Population health
- Advanced AI

---

# 11. Architecture Decisions

| Decision | Reason |
|----------|--------|
| One capability per service | Clear ownership |
| Database per service | Data isolation |
| API-first communication | Standardization |
| Event-driven integration | Scalability |
| Phased implementation | Reduced delivery risk |

---

# 12. Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Service overlap | Responsibility matrix |
| Circular dependencies | Clear dependency rules |
| Database coupling | Database-per-service |
| Scope growth | Phased roadmap |

---

# 13. Related Documents

- 03 Bounded Contexts
- 04 Context Map
- 05 Enterprise System Architecture
- 06 Microservice Architecture
- 08 Service Dependency Map

---

# 14. Conclusion

The Service Responsibility Matrix defines the ownership and responsibilities of every microservice in EHMS.

It serves as the primary reference for backend development, ensuring that each service has a clear purpose, well-defined boundaries, and minimal coupling with the rest of the platform.