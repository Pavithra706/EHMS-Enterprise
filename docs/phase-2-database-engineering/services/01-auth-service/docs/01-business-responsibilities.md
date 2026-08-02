# Auth Service Business Responsibilities

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Business Responsibilities |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service is responsible for identity verification, authentication, authorization, and access control within EHMS.

Its responsibility is limited to verifying identities, issuing and validating tokens, managing security credentials, and enforcing authorization policies. It does not own business profile information or healthcare data.

Clearly defined responsibilities ensure loose coupling between microservices and maintain a clean Domain-Driven Design (DDD) architecture.

---

# 1. Core Responsibilities

The Auth Service is responsible for:

- User authentication
- Password management
- Password hashing
- JWT generation
- Refresh token management
- User session management
- Login history
- Role management
- Permission management
- Role-permission mapping
- User-role mapping
- Multi-Factor Authentication (MFA)
- Email verification
- Password reset
- Account locking
- Token revocation
- Security policy enforcement

---

# 2. Authentication Responsibilities

The Auth Service performs:

- Login
- Logout
- Token generation
- Token validation
- Token refresh
- Session validation
- Credential verification

Supported authentication methods:

- Username & Password
- Email & Password
- MFA (OTP/TOTP)
- Service-to-Service JWT Authentication

---

# 3. Authorization Responsibilities

The Auth Service manages:

- Roles
- Permissions
- Access policies
- RBAC evaluation
- Permission assignment
- Role assignment

Authorization decisions are based on JWT claims and stored role-permission mappings.

---

# 4. Session Management

The Auth Service maintains:

- Active sessions
- Refresh tokens
- Device information
- Login timestamps
- Logout timestamps
- Session expiration
- Token revocation

---

# 5. Security Responsibilities

The Auth Service enforces:

- Password complexity
- Password hashing
- Account lockout
- Failed login tracking
- MFA
- Secure token storage
- Session timeout
- Refresh token rotation

---

# 6. Data Ownership

The Auth Service owns:

| Entity | Ownership |
|---------|-----------|
| User (Authentication Identity) | Full |
| Role | Full |
| Permission | Full |
| UserRole | Full |
| RolePermission | Full |
| RefreshToken | Full |
| UserSession | Full |
| LoginHistory | Full |
| PasswordResetToken | Full |
| EmailVerificationToken | Full |
| MFAConfiguration | Full |

---

# 7. Referenced Data

The Auth Service references, but does not own:

| Entity | Owner Service |
|----------|---------------|
| User Profile | User Service |
| Patient | Patient Service |
| Doctor | Doctor Service |
| Nurse | Nurse Service |
| Employee | HR Service |

References use UUIDs only.

---

# 8. Out of Scope

The Auth Service must never manage:

- Patient registration
- Doctor profiles
- Employee records
- Departments
- Billing
- Laboratory data
- Pharmacy data
- Appointments
- Medical records

These belong to their respective domain services.

---

# 9. Published Events

The Auth Service publishes:

- UserLoggedIn
- UserLoggedOut
- PasswordChanged
- PasswordResetRequested
- PasswordResetCompleted
- RoleAssigned
- PermissionUpdated
- AccountLocked
- AccountUnlocked
- EmailVerified

---

# 10. Consumed Events

The Auth Service consumes:

- UserCreated
- UserUpdated
- UserDeleted
- EmployeeActivated
- EmployeeDeactivated

These events keep authentication identities synchronized with other services.

---

# 11. Business Rules

The Auth Service enforces:

- Every authentication identity has a unique UUID.
- Email addresses must be unique.
- Usernames must be unique.
- Passwords are never stored in plain text.
- Refresh tokens expire.
- Access tokens are short-lived.
- Locked accounts cannot authenticate.
- Disabled accounts cannot receive new tokens.

---

# 12. Service Boundaries

```mermaid
graph TD

AuthService

--> Authentication

--> Authorization

--> Sessions

--> Tokens

--> MFA

UserService

--> User Profile

PatientService

--> Patient Data

HRService

--> Employee Data
```

---

# 13. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Separate authentication from user profiles | Clear service boundaries |
| JWT-based authentication | Stateless architecture |
| RBAC | Fine-grained authorization |
| Refresh tokens | Improved security |
| UUID references | Loose coupling |

---

# 14. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Service overlap | Clear ownership |
| Duplicate user data | Reference by UUID |
| Unauthorized access | RBAC & JWT |
| Session hijacking | Token rotation & expiration |

---

# 15. Related Documents

- 00 Overview
- Authentication Architecture (Phase 1.5)
- Authorization (RBAC)
- Security Architecture
- UUID Strategy

---

# 16. Conclusion

The Auth Service is the central authority for authentication and authorization within EHMS. By clearly defining its responsibilities and boundaries, it enables secure identity management while allowing other microservices to focus exclusively on their own business domains.