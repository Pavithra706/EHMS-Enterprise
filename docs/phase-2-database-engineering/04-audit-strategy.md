# Audit Strategy

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2 – Database Engineering |
| Document | Audit Strategy |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Audit Strategy defines how EHMS records creation, modification, and deletion metadata for all business entities.

Audit information provides accountability, traceability, operational visibility, and supports security investigations, reporting, and compliance requirements.

All business tables follow a standardized audit model.

---

# 1. Purpose

This document defines:

- Audit fields
- Audit ownership
- Audit lifecycle
- Audit implementation
- Prisma standards
- Best practices

---

# 2. Audit Principles

EHMS follows:

- Every change is traceable
- Every record has ownership
- Audit data is immutable
- Consistent audit fields
- UTC timestamps
- Secure audit logging

---

# 3. Standard Audit Fields

Every business table contains:

| Column | Type | Description |
|----------|------|-------------|
| created_at | TIMESTAMPTZ | Record creation time |
| updated_at | TIMESTAMPTZ | Last update time |
| created_by | UUID | Creator |
| updated_by | UUID | Last modifier |

Optional fields:

| Column | Type |
|----------|------|
| version | INTEGER |
| last_accessed_at | TIMESTAMPTZ |

---

# 4. Audit Lifecycle

```mermaid
flowchart LR

Create

↓

Update

↓

Update

↓

Update

↓

Archive
```

---

# 5. Prisma Example

```prisma
model Patient {

  id String @id @default(uuid()) @db.Uuid

  createdAt DateTime @default(now()) @map("created_at")

  updatedAt DateTime @updatedAt @map("updated_at")

  createdBy String? @db.Uuid @map("created_by")

  updatedBy String? @db.Uuid @map("updated_by")

  @@map("patients")

}
```

---

# 6. Creation Rules

When a record is created:

- created_at is populated automatically.
- updated_at equals created_at.
- created_by stores the authenticated user.
- updated_by equals created_by.

---

# 7. Update Rules

Every update:

- updates updated_at.
- updates updated_by.
- never modifies created_at.
- never modifies created_by.

---

# 8. Time Standard

All timestamps use:

```
UTC
```

PostgreSQL type:

```
TIMESTAMP WITH TIME ZONE
```

Applications convert timestamps to the user's local timezone when displaying them.

---

# 9. User Tracking

Audit users reference:

```
auth-service

↓

User UUID
```

System-generated operations may use a reserved system user identifier.

---

# 10. Optimistic Locking

Optional version field:

```text
version

1

↓

2

↓

3
```

Useful for preventing concurrent update conflicts.

---

# 11. Audit Events

Important changes also generate audit events.

Examples:

- Patient Created
- Patient Updated
- Invoice Modified
- Prescription Updated
- Employee Created

These events are consumed by the audit-service.

---

# 12. Security

Audit information:

- Cannot be edited manually.
- Must be retained according to organizational policy.
- Is accessible only to authorized users.

---

# 13. Performance

Index:

```
created_at

updated_at

created_by
```

Frequently queried audit fields should be indexed appropriately.

---

# 14. Architecture Decisions

| Decision | Reason |
|----------|--------|
| UTC timestamps | Global consistency |
| Standard audit fields | Uniform implementation |
| User UUID | Traceability |
| Immutable creation data | Data integrity |
| Automatic timestamps | Reduced errors |

---

# 15. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Missing audit data | Mandatory fields |
| Incorrect timestamps | UTC standard |
| User spoofing | JWT validation |
| Concurrent updates | Version field |

---

# 16. Future Enhancements

Future improvements include:

- Full change history
- Field-level auditing
- Audit dashboards
- Data lineage
- Event sourcing for selected domains

---

# 17. Related Documents

- 03 UUID Strategy
- 05 Soft Delete Strategy
- 19 Security Architecture (Phase 1.5)
- 23 Observability Architecture (Phase 1.5)

---

# 18. Conclusion

The Audit Strategy establishes a consistent mechanism for tracking data creation and modification across EHMS. Standardized audit fields improve accountability, operational transparency, and support security investigations while remaining reusable across every microservice database.