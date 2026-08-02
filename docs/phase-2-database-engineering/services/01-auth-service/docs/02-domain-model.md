# Auth Service Domain Model

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Domain Model |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service Domain Model defines the business entities responsible for authentication, authorization, identity verification, session management, and security.

These entities form the foundation of the Auth Service database and will be implemented using PostgreSQL and Prisma ORM.

---

# 1. Domain Overview

The Auth Service is responsible for:

- Authentication
- Authorization
- Identity
- Session Management
- Security Policies

It owns only authentication-related data and references business entities using UUIDs.

---

# 2. Aggregate Roots

The following entities are Aggregate Roots.

| Entity | Description |
|----------|-------------|
| User | Authentication identity |
| Role | User role |
| Permission | System permission |
| RefreshToken | Refresh token |
| UserSession | Active session |
| LoginHistory | Login audit |

---

# 3. Domain Entities

## User

Represents the authentication identity.

Responsibilities

- Login
- Password
- Status
- Email verification
- MFA

Owns

- Sessions
- Refresh Tokens
- Login History

---

## Role

Represents a security role.

Examples

- Super Admin
- Hospital Admin
- Doctor
- Nurse
- Receptionist
- Pharmacist
- Laboratory Technician
- Radiologist
- Cashier
- Patient

---

## Permission

Represents a single permission.

Examples

```
patient.read

patient.create

patient.update

billing.create

ehr.view

lab.result.update
```

---

## UserRole

Maps users to roles.

Supports multiple roles per user.

Example

```
Doctor

↓

Doctor

Research Coordinator
```

---

## RolePermission

Maps roles to permissions.

Example

```
Doctor

↓

ehr.view

ehr.update

prescription.create
```

---

## RefreshToken

Stores long-lived authentication tokens.

Tracks

- expiration
- revocation
- device

---

## UserSession

Represents an active login session.

Stores

- login time
- device
- IP
- browser
- logout time

---

## LoginHistory

Stores all login attempts.

Tracks

- successful login
- failed login
- lockouts
- MFA verification

---

## PasswordResetToken

Temporary token.

Purpose

Password reset.

Expires automatically.

---

## EmailVerificationToken

Temporary token.

Purpose

Email verification.

Expires automatically.

---

## MFAConfiguration

Stores

- MFA enabled
- secret
- recovery codes

---

# 4. Entity Relationships

```
User

├── UserRole

├── RefreshToken

├── UserSession

├── LoginHistory

├── PasswordResetToken

└── EmailVerificationToken


Role

└── RolePermission


Permission

└── RolePermission
```

---

# 5. Cardinality

| Relationship | Cardinality |
|---------------|-------------|
| User → UserRole | One-to-Many |
| Role → UserRole | One-to-Many |
| Role → RolePermission | One-to-Many |
| Permission → RolePermission | One-to-Many |
| User → RefreshToken | One-to-Many |
| User → UserSession | One-to-Many |
| User → LoginHistory | One-to-Many |
| User → PasswordResetToken | One-to-Many |
| User → EmailVerificationToken | One-to-Many |
| User → MFAConfiguration | One-to-One |

---

# 6. Value Objects

The domain includes the following value objects.

- Email Address
- Password Hash
- JWT Token
- Refresh Token
- IP Address
- Device Information
- Browser Information

These objects encapsulate validation rules and should not exist independently.

---

# 7. Enumerations

## User Status

```
ACTIVE

INACTIVE

LOCKED

SUSPENDED

PENDING_VERIFICATION
```

---

## Session Status

```
ACTIVE

EXPIRED

LOGGED_OUT

REVOKED
```

---

## Login Result

```
SUCCESS

FAILED

LOCKED

MFA_REQUIRED
```

---

# 8. Business Rules

- One email belongs to one authentication identity.
- A user may have multiple active sessions.
- A user may have multiple refresh tokens.
- A role may contain multiple permissions.
- A permission may belong to multiple roles.
- Password reset tokens expire automatically.
- Email verification tokens expire automatically.
- MFA configuration is optional.
- Passwords are stored only as secure hashes.
- Authentication identities reference business profiles using UUIDs.

---

# 9. Domain Events

The Auth Service publishes:

- UserLoggedIn
- UserLoggedOut
- PasswordChanged
- PasswordResetRequested
- PasswordResetCompleted
- RoleAssigned
- PermissionGranted
- PermissionRevoked
- AccountLocked
- AccountUnlocked
- EmailVerified
- MFAEnabled
- MFADisabled

---

# 10. External References

The User entity stores references only.

```
employee_id

doctor_id

patient_id

nurse_id
```

These UUIDs point to entities owned by other services.

---

# 11. Domain Boundaries

The Auth Service owns:

- Authentication
- Authorization
- Identity
- Sessions
- Tokens

The Auth Service does not own:

- Employee Profile
- Patient Profile
- Doctor Profile
- HR Data
- Clinical Data

---

# 12. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Separate UserRole entity | Many-to-many relationship |
| Separate RolePermission entity | Flexible RBAC |
| Refresh tokens stored | Secure session management |
| Login history retained | Auditing |
| MFA as separate entity | Optional feature |

---

# 13. Related Documents

- 00 Overview
- 01 Business Responsibilities
- 03 ER Diagram
- Authentication Architecture (Phase 1.5)
- Authorization (RBAC)

---

# 14. Conclusion

The Auth Service Domain Model defines the entities, relationships, business rules, and boundaries required for authentication and authorization in EHMS. This model serves as the blueprint for the ER diagram, Prisma schema, and database implementation while maintaining clear ownership within the microservice architecture.