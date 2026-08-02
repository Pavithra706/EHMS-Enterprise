# Soft Delete Strategy

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2 – Database Engineering |
| Document | Soft Delete Strategy |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Soft Delete Strategy defines how records are logically deleted across the Enterprise Hospital Management System (EHMS).

Instead of permanently removing data from the database, records are marked as deleted while remaining available for auditing, reporting, legal compliance, and recovery when required.

This strategy protects critical healthcare data and supports long-term operational integrity.

---

# 1. Purpose

This document defines:

- Soft delete implementation
- Standard delete fields
- Recovery process
- Query behavior
- Prisma implementation
- Best practices

---

# 2. Soft Delete Principles

EHMS follows:

- No permanent deletion of business records
- Recoverable data
- Consistent implementation
- Full auditability
- Secure restoration
- Controlled permanent deletion

---

# 3. Standard Soft Delete Fields

Every business table contains:

| Column | Type | Description |
|---------|------|-------------|
| is_deleted | BOOLEAN | Logical deletion flag |
| deleted_at | TIMESTAMPTZ | Deletion timestamp |
| deleted_by | UUID | User performing deletion |

Default values:

```text
is_deleted = FALSE
deleted_at = NULL
deleted_by = NULL
```

---

# 4. Record Lifecycle

```mermaid
flowchart LR

Created

↓

Updated

↓

Soft Deleted

↓

Restored

↓

Archived

↓

Permanent Removal (Exceptional Cases)
```

---

# 5. Prisma Example

```prisma
model Patient {

  id String @id @default(uuid()) @db.Uuid

  isDeleted Boolean @default(false) @map("is_deleted")

  deletedAt DateTime? @map("deleted_at")

  deletedBy String? @db.Uuid @map("deleted_by")

  @@index([isDeleted])

  @@map("patients")

}
```

---

# 6. Delete Process

When deleting a record:

```text
is_deleted = TRUE

deleted_at = CURRENT_TIMESTAMP

deleted_by = Current User UUID
```

The record remains in the database.

---

# 7. Restore Process

When restoring:

```text
is_deleted = FALSE

deleted_at = NULL

deleted_by = NULL
```

The record becomes available again.

---

# 8. Query Standards

Normal application queries must return only active records.

Example SQL

```sql
SELECT *
FROM patients
WHERE is_deleted = FALSE;
```

Administrative tools may optionally include deleted records.

---

# 9. Permanent Deletion

Permanent deletion is allowed only when:

- Required by organizational policy
- Required by applicable legal or regulatory obligations
- Data retention period has expired
- Approved through administrative procedures

Permanent deletion should always be audited.

---

# 10. Business Rules

Soft delete applies to:

- Patients
- Doctors
- Employees
- Departments
- Appointments
- Admissions
- Laboratory Orders
- Pharmacy Records
- Billing Records

Some historical records (such as finalized audit logs) should never be deleted.

---

# 11. Cascading Rules

Deleting a parent record must not automatically delete related business records.

Dependent relationships should be handled explicitly according to business rules.

---

# 12. Security

Only authorized users may:

- Delete records
- Restore records
- Permanently remove records

Every action must be audited.

---

# 13. Performance

Indexes should include:

```text
is_deleted

deleted_at
```

These indexes improve filtering performance.

---

# 14. Backup Considerations

Soft-deleted records remain part of backups.

Recovery procedures should preserve deletion status.

---

# 15. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Logical deletion | Prevent accidental data loss |
| Recovery support | Restore deleted records |
| Audit tracking | Accountability |
| Standard fields | Consistency |
| Controlled hard delete | Compliance |

---

# 16. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Forgotten filters | Repository-level query standards |
| Accidental hard delete | Restricted permissions |
| Storage growth | Archival policies |
| Unauthorized restoration | RBAC + Audit logging |

---

# 17. Future Enhancements

Future improvements include:

- Automatic archival
- Configurable retention periods
- Batch restoration
- Archive database
- Lifecycle management automation

---

# 18. Related Documents

- 04 Audit Strategy
- 07 Indexing Strategy
- 09 Migration Strategy
- 21 Database Design Standards (Phase 1.5)

---

# 19. Conclusion

The Soft Delete Strategy ensures that EHMS protects critical healthcare data by preventing accidental data loss while supporting recovery, auditing, and long-term operational requirements. A standardized implementation across all services improves consistency and simplifies maintenance.