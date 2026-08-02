# Auth Service Database Overview

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Database Overview |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service is responsible for identity management, authentication, authorization, session management, and security within the Enterprise Hospital Management System (EHMS).

It provides secure access to all applications and services by issuing JWT access tokens, managing refresh tokens, enforcing Role-Based Access Control (RBAC), supporting Multi-Factor Authentication (MFA), maintaining user sessions, and recording security-related activities.

The Auth Service owns all authentication and authorization data and exposes secure APIs consumed by the API Gateway and other microservices.

---

# 1. Purpose

The Auth Service provides:

- User authentication
- JWT token generation
- Refresh token management
- Role-Based Access Control (RBAC)
- Permission management
- Session management
- Multi-Factor Authentication (MFA)
- Password reset
- Email verification
- Account locking
- Security audit support

---

# 2. Responsibilities

The Auth Service is responsible for:

- Authenticating users
- Issuing JWT access tokens
- Managing refresh tokens
- Validating credentials
- Managing roles
- Managing permissions
- Managing role-permission mappings
- Managing active user sessions
- Recording login history
- Enforcing account security policies

---

# 3. Out of Scope

The Auth Service does not manage:

- Patient records
- Doctor profiles
- Employee information
- Department data
- Appointments
- Billing
- Medical records

Those belong to their respective services.

---

# 4. Database Ownership

The Auth Service exclusively owns:

- Users (authentication identity only)
- Roles
- Permissions
- Role Permissions
- User Roles
- Refresh Tokens
- User Sessions
- Login History
- Password Reset Tokens
- Email Verification Tokens
- MFA Configuration

No other service may directly modify these tables.

---

# 5. Primary Consumers

The following components interact with the Auth Service:

- API Gateway
- Web Admin Portal
- Doctor Portal
- Nurse Portal
- Patient Portal
- Mobile Applications
- Internal Microservices

---

# 6. External Dependencies

The Auth Service communicates with:

- User Service
- Notification Service
- Audit Service
- API Gateway

---

# 7. Core Entities

The Auth Service database contains:

- User
- Role
- Permission
- UserRole
- RolePermission
- RefreshToken
- UserSession
- LoginHistory
- PasswordResetToken
- EmailVerificationToken
- MFAConfiguration

---

# 8. Security Objectives

The service enforces:

- Secure password storage
- JWT authentication
- Refresh token rotation
- RBAC authorization
- MFA
- Session expiration
- Account lockout
- Audit logging

---

# 9. High-Level Architecture

```mermaid
graph TD

User --> API Gateway

API Gateway --> Auth Service

Auth Service --> PostgreSQL

Auth Service --> Notification Service

Auth Service --> Audit Service

Auth Service --> User Service
```

---

# 10. Database Scope

The Auth Service stores only authentication and authorization data.

Business profile information is maintained by the User Service.

---

# 11. Service Boundaries

Owns:

- Identity
- Authentication
- Authorization
- Sessions
- Tokens

References:

- User UUID
- Employee UUID
- Patient UUID

No business data is duplicated.

---

# 12. Availability Requirements

Target:

- Availability: 99.9%
- Login Response: <300 ms
- Token Validation: <100 ms

---

# 13. Related Documents

- Authentication Architecture (Phase 1.5)
- Authorization (RBAC)
- Security Architecture
- PostgreSQL Architecture
- UUID Strategy

---

# 14. Conclusion

The Auth Service Database provides the security foundation of EHMS. By centralizing authentication, authorization, token management, and session control, it enables secure communication between users, applications, and microservices while maintaining a clear separation between identity management and business domains.