# Auth Service Prisma Schema

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Prisma Schema |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the Prisma ORM schema for the Auth Service.

The schema implements authentication, authorization, session management, token management, Role-Based Access Control (RBAC), and security while following the enterprise database standards established in Phase 2.

---

# Prisma Generator

```prisma
generator client {
  provider = "prisma-client-py"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```

> **Note:** Since your backend is **FastAPI + Python**, `prisma-client-py` is the correct client generator. If you later migrate to the official Prisma Python ecosystem or another ORM, this section can be updated.

---

# Enumerations

## UserStatus

```prisma
enum UserStatus {
  ACTIVE
  INACTIVE
  LOCKED
  SUSPENDED
  PENDING_VERIFICATION
}
```

---

## SessionStatus

```prisma
enum SessionStatus {
  ACTIVE
  EXPIRED
  LOGGED_OUT
  REVOKED
}
```

---

## LoginResult

```prisma
enum LoginResult {
  SUCCESS
  FAILED
  LOCKED
  MFA_REQUIRED
}
```

---

# Entity Summary

| Model | Purpose |
|---------|----------|
| User | Authentication identity |
| Role | Security role |
| Permission | Permission catalog |
| UserRole | User-role mapping |
| RolePermission | Role-permission mapping |
| RefreshToken | Refresh tokens |
| UserSession | Active sessions |
| LoginHistory | Login audit |
| PasswordResetToken | Password reset |
| EmailVerificationToken | Email verification |
| MFAConfiguration | MFA settings |

---

# Shared Standards

Every model follows:

- UUID primary key
- Audit columns
- Soft delete columns
- `@@map()` for snake_case tables
- `@map()` for snake_case database fields
- PostgreSQL UUID type
- Foreign key relations
- Required indexes
- Unique constraints where applicable

---

# User Model Overview

The User model contains:

Authentication:

- username
- email
- password_hash

Security:

- status
- email_verified
- failed_login_attempts
- last_login_at

Relationships:

- Roles
- Sessions
- Tokens
- Login History
- MFA

---

# Role Model Overview

Contains:

- role name
- description
- system role flag

Relationships:

- UserRole
- RolePermission

---

# Permission Model Overview

Contains:

- permission name
- resource
- action
- description

Relationships:

- RolePermission

---

# Junction Tables

The schema contains two many-to-many mapping tables.

## UserRole

```
User

↓

UserRole

↓

Role
```

Unique constraint

```
user_id + role_id
```

---

## RolePermission

```
Role

↓

RolePermission

↓

Permission
```

Unique constraint

```
role_id + permission_id
```

---

# Security Models

Additional models:

- RefreshToken
- UserSession
- LoginHistory
- PasswordResetToken
- EmailVerificationToken
- MFAConfiguration

Each model references the User entity using UUID foreign keys.

---

# Common Audit Fields

Every model includes:

```text
created_at

updated_at

created_by

updated_by
```

---

# Common Soft Delete Fields

Every model includes:

```text
is_deleted

deleted_at

deleted_by
```

---

# Common Indexes

Examples

```prisma
@@index([email])

@@index([username])

@@index([status])

@@index([isDeleted])

@@index([createdAt])
```

---

# Common Unique Constraints

```prisma
@@unique([email])

@@unique([username])

@@unique([roleId, permissionId])

@@unique([userId, roleId])
```

---

# Naming Standards

Prisma Model

```prisma
model User
```

Database Table

```sql
users
```

Mapping

```prisma
@@map("users")
```

---

# Migration Notes

Migration order

1. User
2. Role
3. Permission
4. UserRole
5. RolePermission
6. RefreshToken
7. UserSession
8. LoginHistory
9. PasswordResetToken
10. EmailVerificationToken
11. MFAConfiguration

---

# Performance Considerations

The following columns should be indexed:

- email
- username
- user_id
- role_id
- permission_id
- expires_at
- status
- created_at

Composite indexes:

- user_id + status
- user_id + expires_at
- role_id + permission_id

---

# Related Documents

- 03 ER Diagram
- 04 Entity Definitions
- 06 Relationships
- PostgreSQL Architecture
- Indexing Strategy

---

# Conclusion

The Auth Service Prisma schema follows the enterprise database standards defined for EHMS. It provides a secure, normalized, and scalable data model that supports authentication, authorization, session management, and RBAC while remaining implementation-ready for PostgreSQL and FastAPI.