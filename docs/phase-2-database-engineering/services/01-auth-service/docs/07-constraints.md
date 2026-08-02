# Auth Service Constraints

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Database Constraints |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the database constraints implemented by the Auth Service.

Constraints ensure data integrity, prevent invalid records, enforce business rules, and maintain referential consistency across all authentication entities.

---

# 1. Purpose

This document defines:

- Primary keys
- Foreign keys
- Unique constraints
- Check constraints
- NOT NULL constraints
- Default values
- Business validation rules

---

# 2. Primary Key Constraints

Every table uses UUID as the primary key.

| Table | Primary Key |
|---------|-------------|
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

# 3. Foreign Key Constraints

| Child Table | Column | Parent Table |
|--------------|--------|--------------|
| user_roles | user_id | users |
| user_roles | role_id | roles |
| role_permissions | role_id | roles |
| role_permissions | permission_id | permissions |
| refresh_tokens | user_id | users |
| user_sessions | user_id | users |
| login_history | user_id | users |
| password_reset_tokens | user_id | users |
| email_verification_tokens | user_id | users |
| mfa_configurations | user_id | users |

---

# 4. Unique Constraints

## Users

```text
username

email
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

Composite unique constraint

```text
user_id + role_id
```

---

## Role Permissions

Composite unique constraint

```text
role_id + permission_id
```

---

## MFA Configuration

```text
user_id
```

Only one MFA configuration is allowed per user.

---

# 5. NOT NULL Constraints

The following columns are mandatory.

## User

- username
- email
- password_hash
- status
- created_at
- updated_at

---

## Role

- name

---

## Permission

- name
- resource
- action

---

## Refresh Token

- user_id
- token_hash
- expires_at

---

## Session

- user_id
- login_at
- status

---

# 6. Default Values

| Column | Default |
|----------|----------|
| created_at | CURRENT_TIMESTAMP |
| updated_at | CURRENT_TIMESTAMP |
| email_verified | FALSE |
| failed_login_attempts | 0 |
| is_deleted | FALSE |
| enabled (MFA) | FALSE |

---

# 7. Check Constraints

## Failed Login Attempts

```text
failed_login_attempts >= 0
```

---

## Expiration

```text
expires_at > created_at
```

---

## Email

Email format validation should occur primarily in the application layer. Database checks may be added if appropriate.

---

## Status

Values must match defined enums.

---

# 8. Business Constraints

## User

- Username must be unique.
- Email must be unique.
- Password must be stored as a secure hash.
- Locked users cannot authenticate.
- Suspended users cannot receive tokens.

---

## Refresh Token

- Token must be hashed.
- Token cannot be reused after revocation.
- Expired token is invalid.

---

## User Session

- Logout time cannot be earlier than login time.
- Session status must be valid.

---

## Password Reset

- Single-use token.
- Automatically expires.

---

## Email Verification

- Single-use token.
- Automatically expires.

---

## MFA

- One configuration per user.
- Secret stored encrypted.
- Recovery codes stored securely.

---

# 9. Referential Integrity Rules

| Parent Deleted | Action |
|----------------|--------|
| User | Cascade dependent security records, preserve login history where required |
| Role | Restrict if assigned |
| Permission | Restrict if assigned |

---

# 10. Prisma Constraint Examples

```prisma
@@unique([email])

@@unique([username])

@@unique([userId, roleId])

@@unique([roleId, permissionId])
```

---

# 11. Validation Responsibility

| Validation | Layer |
|------------|-------|
| Email format | Application |
| Password strength | Application |
| Username uniqueness | Database |
| Foreign key integrity | Database |
| Enum validation | Database |
| JWT validation | Application |

---

# 12. Architecture Decisions

| Decision | Reason |
|----------|--------|
| UUID primary keys | Distributed architecture |
| Composite unique constraints | Prevent duplicate mappings |
| Database foreign keys | Strong integrity |
| Enum constraints | Consistent values |
| Application-layer validation | Better user experience |

---

# 13. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Duplicate users | Unique constraints |
| Invalid relationships | Foreign keys |
| Weak passwords | Application validation |
| Invalid enum values | Database enums |

---

# 14. Related Documents

- 04 Entity Definitions
- 05 Prisma Schema
- 06 Relationships
- 08 Index Strategy

---

# 15. Conclusion

The Auth Service constraint strategy ensures that authentication data remains accurate, secure, and consistent throughout the EHMS platform. By combining database constraints with application-level validation, the system maintains strong data integrity while providing flexibility for future enhancements.