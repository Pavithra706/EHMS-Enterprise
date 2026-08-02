# Auth Service Entity Definitions

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Entity Definitions |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines every entity owned by the Auth Service. It specifies each table's purpose, primary fields, relationships, constraints, and business rules before implementation using Prisma ORM.

---

# 1. User

## Purpose

Represents an authentication identity.

This entity stores only authentication-related information.

Business profile information belongs to the User Service.

---

### Primary Fields

| Field | Type | Required |
|---------|------|----------|
| id | UUID | Yes |
| username | String | Yes |
| email | String | Yes |
| password_hash | String | Yes |
| status | Enum | Yes |
| email_verified | Boolean | Yes |
| last_login_at | Timestamp | No |
| failed_login_attempts | Integer | Yes |

---

### Relationships

- One User → Many UserRoles
- One User → Many Sessions
- One User → Many Refresh Tokens
- One User → Many Login History
- One User → One MFA Configuration

---

### Business Rules

- Username must be unique.
- Email must be unique.
- Password stored only as a secure hash.
- Email verification required before full access.
- Failed logins may lock the account.

---

# 2. Role

## Purpose

Represents a security role.

Examples

- Super Admin
- Doctor
- Nurse
- Receptionist
- Pharmacist
- Patient

---

### Primary Fields

| Field | Type |
|---------|------|
| id | UUID |
| name | String |
| description | String |
| is_system_role | Boolean |

---

### Relationships

- One Role → Many UserRoles
- One Role → Many RolePermissions

---

### Business Rules

- Role names must be unique.
- System roles cannot be deleted.

---

# 3. Permission

## Purpose

Represents a single application permission.

Examples

```
patient.read

patient.update

ehr.view

billing.create
```

---

### Primary Fields

| Field | Type |
|---------|------|
| id | UUID |
| name | String |
| resource | String |
| action | String |
| description | String |

---

### Relationships

- One Permission → Many RolePermissions

---

### Business Rules

- Permission names must be unique.

---

# 4. UserRole

## Purpose

Associates users with roles.

Supports multiple roles per user.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| role_id | UUID |
| assigned_at | Timestamp |

---

### Constraints

Unique combination

```
user_id + role_id
```

---

# 5. RolePermission

## Purpose

Associates roles with permissions.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| role_id | UUID |
| permission_id | UUID |

---

### Constraints

Unique combination

```
role_id + permission_id
```

---

# 6. RefreshToken

## Purpose

Stores refresh tokens.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| token_hash | String |
| expires_at | Timestamp |
| revoked_at | Timestamp |
| device_name | String |

---

### Business Rules

- Store hashed tokens only.
- Expired tokens cannot be reused.
- Revoked tokens are permanently invalid.

---

# 7. UserSession

## Purpose

Tracks active login sessions.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| ip_address | String |
| device_name | String |
| browser | String |
| login_at | Timestamp |
| logout_at | Timestamp |
| status | Enum |

---

### Business Rules

- Multiple active sessions are allowed unless restricted by policy.
- Session expiration is configurable.

---

# 8. LoginHistory

## Purpose

Stores all authentication attempts.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| login_time | Timestamp |
| ip_address | String |
| login_result | Enum |
| failure_reason | String |

---

### Business Rules

- Login history is immutable.
- Failed logins are retained for auditing.

---

# 9. PasswordResetToken

## Purpose

Temporary password reset requests.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| token_hash | String |
| expires_at | Timestamp |
| used_at | Timestamp |

---

### Business Rules

- Token expires automatically.
- Single use only.

---

# 10. EmailVerificationToken

## Purpose

Email verification workflow.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| token_hash | String |
| expires_at | Timestamp |
| verified_at | Timestamp |

---

### Business Rules

- Token expires automatically.
- Single use only.

---

# 11. MFAConfiguration

## Purpose

Stores Multi-Factor Authentication settings.

---

### Fields

| Field | Type |
|---------|------|
| id | UUID |
| user_id | UUID |
| secret | String |
| recovery_codes | JSON |
| enabled | Boolean |

---

### Relationships

One User → One MFAConfiguration

---

### Business Rules

- Secret stored encrypted.
- Recovery codes stored hashed.
- One MFA configuration per user.

---

# 12. Common Columns

Every table includes:

| Column |
|----------|
| created_at |
| updated_at |
| created_by |
| updated_by |
| is_deleted |
| deleted_at |
| deleted_by |

Following the enterprise Audit Strategy and Soft Delete Strategy.

---

# 13. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Separate token tables | Better security |
| Junction tables | Flexible RBAC |
| UUID keys | Microservice consistency |
| Audit columns | Traceability |
| Soft delete | Data recovery |

---

# 14. Related Documents

- 02 Domain Model
- 03 ER Diagram
- 05 Prisma Schema
- Audit Strategy
- Soft Delete Strategy

---

# 15. Conclusion

The Auth Service entity definitions establish the complete logical structure of the authentication database. These definitions provide the foundation for implementing the Prisma schema, indexes, constraints, and migrations while maintaining consistency with the enterprise architecture.