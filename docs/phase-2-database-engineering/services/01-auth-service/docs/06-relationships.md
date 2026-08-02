# Auth Service Relationships

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Relationships |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines all relationships between entities in the Auth Service database.

It specifies relationship types, foreign keys, cascade rules, ownership, and referential integrity requirements that will be implemented in PostgreSQL and Prisma ORM.

---

# 1. Relationship Overview

| Parent | Child | Type |
|---------|-------|------|
| User | UserRole | 1:N |
| Role | UserRole | 1:N |
| Role | RolePermission | 1:N |
| Permission | RolePermission | 1:N |
| User | RefreshToken | 1:N |
| User | UserSession | 1:N |
| User | LoginHistory | 1:N |
| User | PasswordResetToken | 1:N |
| User | EmailVerificationToken | 1:N |
| User | MFAConfiguration | 1:1 |

---

# 2. User → UserRole

Purpose

Assign multiple roles to one user.

Cardinality

```
One User

↓

Many User Roles
```

Foreign Key

```
user_roles.user_id

↓

users.id
```

Delete Rule

```
CASCADE
```

---

# 3. Role → UserRole

Purpose

Assign one role to many users.

Foreign Key

```
user_roles.role_id

↓

roles.id
```

Delete Rule

```
RESTRICT
```

System roles cannot be deleted while assigned.

---

# 4. Role → RolePermission

Purpose

Associate permissions with roles.

Foreign Key

```
role_permissions.role_id

↓

roles.id
```

Delete Rule

```
CASCADE
```

---

# 5. Permission → RolePermission

Purpose

Associate permissions with roles.

Foreign Key

```
role_permissions.permission_id

↓

permissions.id
```

Delete Rule

```
RESTRICT
```

Permissions should not be deleted while in use.

---

# 6. User → RefreshToken

Purpose

Support multiple logged-in devices.

Cardinality

```
One User

↓

Many Refresh Tokens
```

Delete Rule

```
CASCADE
```

All refresh tokens are removed when a user is deleted.

---

# 7. User → UserSession

Purpose

Track active sessions.

Cardinality

```
One User

↓

Many Sessions
```

Delete Rule

```
CASCADE
```

---

# 8. User → LoginHistory

Purpose

Maintain security audit history.

Cardinality

```
One User

↓

Many Login Records
```

Delete Rule

```
RESTRICT
```

Historical login records should be preserved.

---

# 9. User → PasswordResetToken

Purpose

Password recovery.

Delete Rule

```
CASCADE
```

Expired tokens may be cleaned up automatically.

---

# 10. User → EmailVerificationToken

Purpose

Email verification workflow.

Delete Rule

```
CASCADE
```

---

# 11. User → MFAConfiguration

Purpose

Store MFA settings.

Cardinality

```
One User

↓

One MFA Configuration
```

Delete Rule

```
CASCADE
```

---

# 12. External References

The User entity references external identities only by UUID.

| Reference | Owner |
|-----------|-------|
| employee_id | HR Service |
| doctor_id | Doctor Service |
| nurse_id | Nurse Service |
| patient_id | Patient Service |

The Auth Service never stores profile information owned by these services.

---

# 13. Cascade Strategy

| Relationship | Action |
|--------------|--------|
| User → RefreshToken | CASCADE |
| User → UserSession | CASCADE |
| User → PasswordResetToken | CASCADE |
| User → EmailVerificationToken | CASCADE |
| User → MFAConfiguration | CASCADE |
| User → LoginHistory | RESTRICT |
| Role → UserRole | RESTRICT |
| Permission → RolePermission | RESTRICT |

---

# 14. Referential Integrity

All foreign keys enforce:

- Valid parent records
- No orphan records
- Consistent relationships
- Controlled deletion

Foreign key constraints must be enabled in every environment.

---

# 15. Prisma Relation Example

```prisma
model User {

  id String @id @default(uuid()) @db.Uuid

  roles UserRole[]

  sessions UserSession[]

  refreshTokens RefreshToken[]

}
```

---

# 16. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Junction tables | Normalize many-to-many relationships |
| UUID foreign keys | Microservice consistency |
| Cascade on tokens | Simplify cleanup |
| Restrict login history deletion | Preserve audit trail |
| One MFA configuration | Simpler security model |

---

# 17. Related Documents

- 03 ER Diagram
- 04 Entity Definitions
- 05 Prisma Schema
- 07 Constraints

---

# 18. Conclusion

The Auth Service relationship model provides a normalized, secure, and maintainable structure for authentication and authorization data. Clearly defined foreign keys, cardinality, and deletion rules ensure data integrity while supporting scalable enterprise authentication.