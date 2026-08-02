# Master Data Management (MDM)

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Master Data Management |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

Master Data Management (MDM) ensures that every core business entity within EHMS has a single authoritative source of truth.

It eliminates duplicate records, improves consistency across microservices, and enables reliable reporting, analytics, and future interoperability with external healthcare systems.

---

# 1. Purpose

The objectives of MDM are:

- Establish authoritative ownership.
- Prevent duplicate master records.
- Ensure enterprise-wide consistency.
- Support interoperability.
- Improve reporting accuracy.
- Simplify future integrations.

---

# 2. Design Principles

EHMS follows these MDM principles:

- Single Source of Truth
- Domain Ownership
- Data Consistency
- Unique Identifiers
- Immutable Business Keys
- API-first Access
- Event-driven Synchronization

---

# 3. Master Data Categories

EHMS master data is divided into:

- Patient
- Employee
- Clinical
- Organization
- Financial
- Inventory
- Reference Data

---

# 4. Master Data Ownership

| Master Data | Owner Service |
|--------------|---------------|
| Patient | patient-service |
| Doctor | doctor-service |
| Nurse | nurse-service |
| Employee | hr-service |
| Department | department-service |
| Appointment Type | appointment-service |
| Bed | ipd-service |
| Ward | ipd-service |
| Laboratory Test | laboratory-service |
| Radiology Test | radiology-service |
| Medicine | pharmacy-service |
| Inventory Item | inventory-service |
| Vendor | inventory-service |
| Insurance Provider | insurance-service |

Only the owner service may create, update, or delete master data.

---

# 5. Reference Data

Reference data changes infrequently and is shared across the platform.

Examples:

- Blood Groups
- Gender
- Marital Status
- Nationality
- Department Types
- Designations
- Appointment Status
- Admission Status
- Invoice Status

Reference data is distributed through APIs or synchronized events.

---

# 6. Master Data Lifecycle

```mermaid
flowchart LR

Create --> Validate

Validate --> Approve

Approve --> Publish

Publish --> Consume

Consume --> Archive
```

---

# 7. Data Synchronization

Synchronization occurs using:

### REST APIs

- On-demand retrieval
- Validation
- Lookup operations

### Domain Events

Examples:

- PatientUpdated
- DoctorUpdated
- DepartmentUpdated
- MedicineUpdated

---

# 8. Data Quality Standards

Master data must satisfy:

- Accuracy
- Completeness
- Consistency
- Validity
- Uniqueness
- Timeliness

---

# 9. Duplicate Prevention

Duplicate detection strategies include:

- UHID uniqueness
- Employee ID uniqueness
- Doctor Registration Number
- Mobile Number validation
- Email validation
- National ID verification (future)

---

# 10. Identifier Standards

| Entity | Identifier |
|----------|------------|
| Patient | UHID |
| Employee | Employee ID |
| Doctor | Doctor ID |
| Department | Department Code |
| Medicine | Medicine Code |
| Invoice | Invoice Number |
| Laboratory Test | Lab Test Code |

Identifiers are immutable after creation.

---

# 11. Data Governance

Rules:

- Only owner services modify master data.
- Changes are audited.
- Version history is maintained where required.
- Sensitive data follows organizational security and privacy policies.

---

# 12. Security

Master data is protected through:

- RBAC
- JWT Authentication
- Audit Logging
- Encryption in Transit
- Encryption at Rest
- Secure APIs

---

# 13. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Single owner | Prevent conflicts |
| Event synchronization | Loose coupling |
| Stable identifiers | Traceability |
| API access | Controlled updates |
| Audit logging | Accountability |

---

# 14. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Duplicate records | Validation rules |
| Conflicting updates | Single ownership |
| Data inconsistency | Event synchronization |
| Unauthorized changes | RBAC & audit logs |

---

# 15. Future Enhancements

Future enhancements include:

- Master Patient Index (MPI)
- Enterprise Provider Registry
- Multi-hospital master data federation
- FHIR Master Resources
- AI-assisted duplicate detection

---

# 16. Related Documents

- 13 Canonical Data Model
- 15 Data Flow Architecture
- 20 API Design Standards
- 21 Database Design Standards

---

# 17. Conclusion

Master Data Management establishes authoritative ownership for core business entities within EHMS. By ensuring a single source of truth and standardized governance, the platform maintains high-quality, consistent, and trustworthy data across all microservices.