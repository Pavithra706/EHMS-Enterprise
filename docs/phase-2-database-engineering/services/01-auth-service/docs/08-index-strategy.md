# Auth Service Index Strategy

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Index Strategy |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the indexing strategy for the Auth Service database.

Indexes are designed to optimize authentication, authorization, session validation, token management, and security-related queries while balancing read performance and write overhead.

---

# 1. Purpose

This document defines:

- Primary indexes
- Unique indexes
- Foreign key indexes
- Composite indexes
- Partial indexes
- Performance recommendations
- Index maintenance

---

# 2. Indexing Principles

EHMS follows:

- Index frequently searched columns
- Index all foreign keys
- Avoid duplicate indexes
- Prefer composite indexes for common query patterns
- Use partial indexes where beneficial
- Monitor index usage regularly

---

# 3. Primary Key Indexes

Every table automatically includes a primary key index.

| Table | Index |
|--------|-------|
| users | id |
| roles | id |
| permissions | id |
| user_roles | id |
| role_permissions | id |
| refresh_tokens | id |
| user_sessions | id |
| login_history | id |
| password_reset_tokens | id |
| email_verification_tokens | id |
| mfa_configurations | id |

---

# 4. Unique Indexes

## Users

```text
email

username
```

---

## Roles

```text
name
```

---

## Permissions

```text
name
```

---

## User Roles

Composite Unique

```text
user_id + role_id
```

---

## Role Permissions

Composite Unique

```text
role_id + permission_id
```

---

## MFA Configuration

```text
user_id
```

---

# 5. Foreign Key Indexes

Create indexes on all foreign keys.

| Table | Column |
|--------|---------|
| user_roles | user_id |
| user_roles | role_id |
| role_permissions | role_id |
| role_permissions | permission_id |
| refresh_tokens | user_id |
| user_sessions | user_id |
| login_history | user_id |
| password_reset_tokens | user_id |
| email_verification_tokens | user_id |
| mfa_configurations | user_id |

---

# 6. Authentication Indexes

Frequently queried columns:

```text
email

username

status

email_verified
```

These support login and account validation.

---

# 7. Session Indexes

```text
user_id

status

expires_at
```

Composite index:

```text
user_id + status
```

---

# 8. Refresh Token Indexes

Indexes:

```text
user_id

expires_at

revoked_at
```

Composite:

```text
user_id + expires_at
```

---

# 9. Login History Indexes

Indexes:

```text
user_id

login_time

login_result
```

Composite:

```text
user_id + login_time
```

Supports audit reports.

---

# 10. Password Reset Indexes

Indexes:

```text
user_id

expires_at
```

---

# 11. Email Verification Indexes

Indexes:

```text
user_id

expires_at
```

---

# 12. Audit Indexes

Every table includes indexes on:

```text
created_at

updated_at

is_deleted
```

---

# 13. Partial Indexes

Example

```sql
CREATE INDEX idx_active_users
ON users(id)
WHERE is_deleted = FALSE;
```

Another example

```sql
CREATE INDEX idx_active_sessions
ON user_sessions(user_id)
WHERE status = 'ACTIVE';
```

These indexes improve query performance while reducing index size.

---

# 14. Prisma Examples

```prisma
@@index([email])

@@index([username])

@@index([status])

@@index([createdAt])

@@index([isDeleted])

@@index([userId, status])

@@index([userId, expiresAt])
```

---

# 15. Performance Considerations

Monitor:

- Slow queries
- Sequential scans
- Index usage
- Index size
- Write overhead
- Query execution plans

Use `EXPLAIN ANALYZE` when tuning queries.

---

# 16. Maintenance

Perform regularly:

- VACUUM
- ANALYZE
- REINDEX (when required)
- Statistics updates

Monitor unused indexes and remove them if no longer beneficial.

---

# 17. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Foreign key indexes | Faster joins |
| Composite indexes | Common query optimization |
| Partial indexes | Reduced storage |
| UUID indexing | Efficient lookups |
| Audit indexes | Reporting support |

---

# 18. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Too many indexes | Review periodically |
| Slow writes | Avoid unnecessary indexes |
| Unused indexes | Monitor usage |
| Missing indexes | Query analysis |

---

# 19. Related Documents

- 05 Prisma Schema
- 06 Relationships
- 07 Constraints
- Enterprise Indexing Strategy

---

# 20. Conclusion

The Auth Service Index Strategy ensures efficient query execution for authentication, authorization, session management, and auditing. By combining primary, unique, foreign key, composite, and partial indexes, the database is optimized for high performance while remaining scalable and maintainable.