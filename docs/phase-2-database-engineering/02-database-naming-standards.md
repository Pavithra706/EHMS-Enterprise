# Database Naming Standards

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2 – Database Engineering |
| Document | Database Naming Standards |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the naming standards used throughout the Enterprise Hospital Management System (EHMS) database layer.

Consistent naming improves readability, maintainability, automation, and developer productivity while reducing ambiguity across microservices.

---

# 1. Purpose

This document standardizes:

- Database schemas
- Tables
- Columns
- Constraints
- Indexes
- Views
- Sequences
- Migrations
- Prisma models

---

# 2. General Principles

All database objects must follow:

- Meaningful names
- Consistent naming
- Lowercase snake_case for database objects
- Singular Prisma models
- Plural table names
- No abbreviations unless widely accepted
- Predictable naming

---

# 3. Schema Naming

Pattern

```
<service>_db
```

Examples

```
auth_db
user_db
patient_db
doctor_db
appointment_db
ehr_db
billing_db
laboratory_db
radiology_db
pharmacy_db
analytics_db
```

---

# 4. Table Naming

Rules

- lowercase
- snake_case
- plural nouns

Examples

```
patients

patient_addresses

patient_contacts

appointments

appointment_slots

laboratory_orders

laboratory_results

invoice_items
```

Avoid

```
Patient

PATIENTS

tbl_patient

patientTable
```

---

# 5. Column Naming

Rules

- snake_case
- descriptive
- avoid abbreviations

Examples

```
patient_id

doctor_id

appointment_date

created_at

updated_at

first_name

last_name

mobile_number
```

---

# 6. Primary Keys

Every table

```
id UUID PRIMARY KEY
```

Business identifiers

```
uhid

invoice_number

employee_code

doctor_code
```

Internal UUIDs and business identifiers serve different purposes.

---

# 7. Foreign Keys

Pattern

```
<entity>_id
```

Examples

```
patient_id

doctor_id

appointment_id

invoice_id

department_id
```

---

# 8. Audit Columns

Every table contains

```
created_at

updated_at

created_by

updated_by

is_deleted

deleted_at
```

Optional

```
deleted_by
```

---

# 9. Constraint Naming

Primary Key

```
pk_patients
```

Foreign Key

```
fk_appointments_patient
```

Unique

```
uk_patients_uhid
```

Check

```
chk_patient_age
```

---

# 10. Index Naming

Pattern

```
idx_<table>_<column>
```

Examples

```
idx_patients_uhid

idx_appointments_date

idx_invoices_status

idx_lab_orders_created_at
```

Composite Index

```
idx_appointments_doctor_date
```

---

# 11. Sequence Naming

If custom sequences are used:

```
seq_patients

seq_invoice_number
```

---

# 12. View Naming

Pattern

```
vw_<name>
```

Examples

```
vw_daily_revenue

vw_patient_summary

vw_doctor_schedule
```

---

# 13. Migration Naming

Pattern

```
001_initial_schema

002_create_patients

003_create_doctors

004_add_indexes

005_add_constraints
```

Migration names should clearly describe their purpose.

---

# 14. Prisma Naming

Model

```prisma
model Patient
```

Table Mapping

```prisma
@@map("patients")
```

Field

```prisma
firstName
```

Database

```
first_name
```

Prisma uses camelCase for fields while mapping to snake_case columns.

---

# 15. Enum Naming

Database

```
appointment_status
```

Prisma

```prisma
enum AppointmentStatus
```

Values

```
SCHEDULED

COMPLETED

CANCELLED
```

---

# 16. File Naming

Prisma

```
schema.prisma
```

Migration

```
202608030001_initial_schema
```

SQL

```
create_patient_indexes.sql
```

---

# 17. Reserved Words

Avoid using reserved SQL keywords.

Examples

Avoid

```
user

order

group

select
```

Prefer

```
users

patient_orders

user_groups
```

---

# 18. Architecture Decisions

| Decision | Reason |
|----------|--------|
| snake_case | PostgreSQL convention |
| Plural tables | Consistency |
| UUID IDs | Global uniqueness |
| Named constraints | Easier debugging |
| Prisma mapping | Clean code |

---

# 19. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Inconsistent names | Standard naming rules |
| Reserved keywords | Naming review |
| Ambiguous columns | Descriptive names |
| Difficult debugging | Named constraints |

---

# 20. Related Documents

- 01 PostgreSQL Architecture
- 03 Schema Strategy
- 04 UUID Strategy
- 21 Database Design Standards (Phase 1.5)

---

# 21. Conclusion

The Database Naming Standards establish a consistent naming convention across all PostgreSQL schemas, tables, columns, indexes, constraints, and Prisma models within EHMS. These standards improve maintainability, readability, and collaboration while supporting long-term scalability.