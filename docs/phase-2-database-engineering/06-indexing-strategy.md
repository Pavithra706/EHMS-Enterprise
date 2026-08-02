# Indexing Strategy

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2 – Database Engineering |
| Document | Indexing Strategy |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Indexing Strategy defines how indexes are designed, maintained, and optimized across all PostgreSQL databases in EHMS.

Proper indexing significantly improves query performance while minimizing storage overhead and write amplification. This strategy standardizes index creation for all microservices.

---

# 1. Purpose

This document defines:

- Index types
- Index naming
- Index creation rules
- Composite indexes
- Partial indexes
- Performance monitoring
- Maintenance practices

---

# 2. Indexing Principles

EHMS follows:

- Index only where beneficial
- Prefer selective indexes
- Optimize read-heavy workloads
- Minimize redundant indexes
- Regularly monitor index usage
- Review indexes as data grows

---

# 3. Index Types

EHMS primarily uses:

| Type | Purpose |
|------|---------|
| B-Tree | Default indexing |
| Unique Index | Enforce uniqueness |
| Composite Index | Multi-column queries |
| Partial Index | Frequently filtered data |
| GIN | JSONB & full-text search |
| BRIN | Very large sequential tables (future) |

---

# 4. Primary Key Index

Every table automatically includes:

```sql
PRIMARY KEY (id)
```

Since `id` is a UUID, PostgreSQL automatically creates a primary key index.

---

# 5. Unique Indexes

Create unique indexes for business identifiers.

Examples:

```text
UHID

Doctor Code

Employee Code

Invoice Number

Appointment Number
```

Example SQL:

```sql
CREATE UNIQUE INDEX idx_patients_uhid
ON patients(uhid);
```

---

# 6. Foreign Key Indexes

Every foreign key should have an index.

Examples:

```text
patient_id

doctor_id

appointment_id

department_id
```

Example:

```sql
CREATE INDEX idx_appointments_patient_id
ON appointments(patient_id);
```

---

# 7. Composite Indexes

Use composite indexes for common query patterns.

Examples:

```text
doctor_id + appointment_date

department_id + status

patient_id + created_at
```

Example:

```sql
CREATE INDEX idx_appointments_doctor_date
ON appointments(doctor_id, appointment_date);
```

---

# 8. Partial Indexes

Use partial indexes for filtered queries.

Example:

```sql
CREATE INDEX idx_active_patients
ON patients(id)
WHERE is_deleted = FALSE;
```

Benefits:

- Smaller indexes
- Faster queries
- Reduced storage

---

# 9. JSONB Indexes

For JSONB columns, use GIN indexes.

Example:

```sql
CREATE INDEX idx_patient_metadata
ON patients
USING GIN(metadata);
```

---

# 10. Search Optimization

Frequently searched columns:

- UHID
- Mobile Number
- Email
- Invoice Number
- Appointment Number
- Doctor Code

These should be indexed based on actual query patterns.

---

# 11. Audit Indexes

Index:

```text
created_at

updated_at

created_by
```

These support reporting and auditing.

---

# 12. Soft Delete Indexes

Every soft-delete table should include:

```sql
CREATE INDEX idx_patients_is_deleted
ON patients(is_deleted);
```

For large tables, a partial index on active records may be more efficient.

---

# 13. Index Naming

Pattern:

```text
idx_<table>_<column>

idx_<table>_<column1>_<column2>
```

Examples:

```text
idx_patients_mobile_number

idx_patients_email

idx_appointments_doctor_date

idx_invoice_status
```

---

# 14. Monitoring

Monitor:

- Index usage
- Sequential scans
- Slow queries
- Unused indexes
- Index size
- Query execution plans

Use PostgreSQL's `EXPLAIN ANALYZE` during performance tuning.

---

# 15. Maintenance

Regular maintenance includes:

- REINDEX (when required)
- VACUUM
- VACUUM ANALYZE
- Statistics updates

Maintenance schedules should minimize operational impact.

---

# 16. Architecture Decisions

| Decision | Reason |
|----------|--------|
| B-Tree | General-purpose indexing |
| Composite indexes | Faster multi-column queries |
| Partial indexes | Efficient filtering |
| Foreign key indexes | Faster joins |
| Regular monitoring | Long-term performance |

---

# 17. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Too many indexes | Review index necessity |
| Slow writes | Limit unnecessary indexes |
| Unused indexes | Monitor usage |
| Missing indexes | Query analysis |

---

# 18. Future Enhancements

Future improvements include:

- Automated index recommendations
- Query performance dashboards
- Index health reports
- Partition-aware indexing
- AI-assisted query optimization

---

# 19. Related Documents

- 01 PostgreSQL Architecture
- 05 Soft Delete Strategy
- 08 Transaction Strategy
- 26 Performance & Scalability Strategy (Phase 1.5)

---

# 20. Conclusion

The Indexing Strategy provides a standardized approach to optimizing database performance across EHMS. By carefully selecting index types, monitoring usage, and maintaining indexes over time, the platform delivers efficient query execution while supporting future growth.