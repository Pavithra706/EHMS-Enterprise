# Database Design Standards

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Database Design Standards |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines enterprise database design standards for the Enterprise Hospital Management System (EHMS).

The standards ensure consistency, maintainability, performance, scalability, security, and data integrity across all PostgreSQL databases owned by EHMS microservices.

---

# 1. Purpose

This document aims to:

- Standardize database design.
- Improve maintainability.
- Ensure data integrity.
- Optimize performance.
- Simplify migrations.
- Support scalability.

---

# 2. Database Principles

EHMS follows:

- Database per Service
- Single Source of Truth
- Normalized Design
- Controlled Denormalization
- ACID Transactions
- Immutable Audit History
- Secure by Design

---

# 3. Database Strategy

Every microservice owns:

- Database Schema
- Tables
- Indexes
- Constraints
- Migrations
- Seed Data

No service directly accesses another service's database.

---

# 4. Naming Standards

## Database Schema

```
patient_db

appointment_db

billing_db

laboratory_db
```

---

## Tables

Use:

snake_case

Examples

```
patients

appointments

laboratory_orders

invoice_items
```

---

## Columns

Use:

snake_case

Examples

```
patient_id

created_at

updated_at

doctor_id

appointment_status
```

---

## Primary Keys

Every table contains

```
id UUID PRIMARY KEY
```

UUID Version 7 (preferred) or UUID Version 4 may be used depending on framework support.

---

# 5. Audit Columns

Every table contains:

```sql
created_at TIMESTAMP

updated_at TIMESTAMP

created_by UUID

updated_by UUID

is_deleted BOOLEAN

deleted_at TIMESTAMP
```

These fields support auditing and soft deletion.

---

# 6. Foreign Keys

Foreign keys are allowed **within the same service database**.

Example:

```
patients

appointments
```

Cross-service database foreign keys are prohibited.

Cross-service references should use business identifiers (such as UUIDs) and service APIs.

---

# 7. Constraints

Use:

- PRIMARY KEY
- UNIQUE
- NOT NULL
- CHECK
- FOREIGN KEY (same service only)

Example:

```sql
CHECK(age >= 0)
```

---

# 8. Indexing Strategy

Create indexes for:

- Primary Keys
- Foreign Keys
- Frequently Searched Columns
- Unique Fields

Examples

```
patient_id

appointment_date

doctor_id

invoice_number

created_at
```

Composite indexes should be added for common query patterns.

---

# 9. Soft Delete Policy

EHMS uses soft delete.

Example

```
is_deleted = TRUE

deleted_at = NOW()
```

Records remain recoverable unless regulatory or operational requirements specify permanent deletion.

---

# 10. Transactions

Transactions should:

- Be short-lived.
- Maintain ACID guarantees.
- Roll back on failure.
- Avoid unnecessary locking.

Distributed transactions are avoided.

Cross-service consistency uses event-driven workflows.

---

# 11. Migrations

Rules:

- Version controlled.
- Incremental.
- Reversible where practical.
- Reviewed before production.

Migration naming:

```
001_initial_schema

002_create_patients

003_add_indexes
```

---

# 12. Seed Data

Seed only reference data.

Examples:

- Departments
- Blood Groups
- User Roles
- Permissions
- Appointment Status

Business data must never be seeded.

---

# 13. Data Types

| Field | Type |
|---------|------|
| ID | UUID |
| Name | VARCHAR |
| Description | TEXT |
| Amount | DECIMAL(12,2) |
| Date | DATE |
| Timestamp | TIMESTAMP WITH TIME ZONE |
| Boolean | BOOLEAN |

---

# 14. Security

Database security includes:

- Encryption at Rest
- TLS Connections
- Least Privilege
- Audit Logging
- Secure Credentials
- Backup Encryption

---

# 15. Backup Strategy

Backups:

- Daily Incremental
- Weekly Full
- Monthly Archive

Backups must be encrypted and tested regularly through restoration exercises.

---

# 16. Performance Guidelines

Monitor:

- Query Performance
- Slow Queries
- Index Usage
- Table Growth
- Lock Contention
- Connection Pool

---

# 17. Partitioning

Large tables may be partitioned.

Examples:

- Audit Logs
- Billing Transactions
- Notification Logs
- Event History

Partitioning strategy should be based on access patterns, commonly by date.

---

# 18. Architecture Decisions

| Decision | Reason |
|----------|--------|
| PostgreSQL | Reliability |
| UUID Keys | Global uniqueness |
| Soft Delete | Data recovery |
| Database per Service | Ownership |
| Versioned Migrations | Maintainability |

---

# 19. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Slow queries | Indexing |
| Data corruption | Constraints |
| Duplicate records | Unique indexes |
| Migration failure | Version control & testing |

---

# 20. Future Enhancements

Future improvements include:

- Read Replicas
- Database Sharding
- Multi-region Replication
- Time-series Storage
- Data Archival Policies

---

# 21. Related Documents

- 13 Canonical Data Model
- 14 Master Data Management
- 15 Data Flow Architecture
- 20 API Design Standards

---

# 22. Conclusion

The Database Design Standards provide a consistent and scalable approach for designing EHMS databases. By standardizing naming, constraints, indexing, migrations, security, and operational practices, the platform ensures reliable, high-performance, and maintainable data storage across all microservices.