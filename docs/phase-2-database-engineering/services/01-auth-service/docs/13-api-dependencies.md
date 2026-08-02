# Auth Service API Dependencies

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | API Dependencies |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service acts as the Identity and Access Management (IAM) service for EHMS.

It exposes APIs for authentication, authorization, token management, session management, password recovery, and email verification while consuming selected APIs from supporting services.

All external requests pass through the API Gateway before reaching the Auth Service.

---

# 1. Responsibilities

The Auth Service exposes APIs for:

- Login
- Logout
- Token Refresh
- Token Validation
- Password Reset
- Email Verification
- MFA Management
- Role Management
- Permission Management
- Session Management

---

# 2. API Consumers

The following applications consume the Auth Service APIs.

| Consumer | Purpose |
|----------|---------|
| Web Admin Portal | Administrator authentication |
| Doctor Portal | Doctor login |
| Nurse Portal | Nurse login |
| Patient Portal | Patient login |
| Reception Portal | Reception authentication |
| Mobile Applications | Mobile authentication |
| API Gateway | Token validation |
| Internal Microservices | Authorization verification |

---

# 3. APIs Exposed

## Authentication

| Method | Endpoint | Purpose |
|----------|----------|---------|
| POST | /auth/login | User login |
| POST | /auth/logout | User logout |
| POST | /auth/refresh | Refresh access token |
| GET | /auth/validate | Validate JWT |

---

## Password Management

| Method | Endpoint |
|----------|----------|
| POST | /auth/password/forgot |
| POST | /auth/password/reset |
| POST | /auth/password/change |

---

## Email Verification

| Method | Endpoint |
|----------|----------|
| POST | /auth/email/send |
| POST | /auth/email/verify |

---

## MFA

| Method | Endpoint |
|----------|----------|
| POST | /auth/mfa/enable |
| POST | /auth/mfa/disable |
| POST | /auth/mfa/verify |

---

## Session Management

| Method | Endpoint |
|----------|----------|
| GET | /sessions |
| DELETE | /sessions/{id} |
| DELETE | /sessions |

---

## Role Management

| Method | Endpoint |
|----------|----------|
| GET | /roles |
| POST | /roles |
| PUT | /roles/{id} |
| DELETE | /roles/{id} |

---

## Permission Management

| Method | Endpoint |
|----------|----------|
| GET | /permissions |
| POST | /permissions |
| PUT | /permissions/{id} |
| DELETE | /permissions/{id} |

---

# 4. APIs Consumed

The Auth Service consumes the following APIs.

---

## User Service

Purpose

Synchronize authentication identities.

Example

```
GET /users/{id}

GET /users/profile

PATCH /users/status
```

---

## Notification Service

Purpose

Send:

- Password reset emails
- Email verification
- MFA notifications
- Security alerts

---

## Audit Service

Purpose

Store:

- Login events
- Logout events
- Password changes
- Role assignments
- Permission updates

---

## File Service

Purpose

Future support for:

- User security certificates
- Security documents

---

# 5. API Gateway Integration

All external requests follow:

```
Client

↓

API Gateway

↓

Authentication Middleware

↓

Auth Service

↓

Response
```

Internal service-to-service communication should use secure service authentication.

---

# 6. Authentication Flow

```
Client

↓

POST /auth/login

↓

Validate Credentials

↓

Generate JWT

↓

Generate Refresh Token

↓

Store Session

↓

Return Tokens
```

---

# 7. Authorization Flow

```
Incoming Request

↓

JWT Validation

↓

Load Roles

↓

Load Permissions

↓

Authorization Decision

↓

Forward Request
```

---

# 8. Error Responses

Standard HTTP status codes:

| Code | Meaning |
|------|---------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 500 | Internal Server Error |

---

# 9. Versioning

API version pattern:

```
/api/v1/auth
```

Future versions:

```
/api/v2/auth
```

Breaking changes require a new API version.

---

# 10. Security

All APIs require:

- HTTPS
- JWT Authentication (except login and password recovery)
- RBAC authorization
- Rate limiting
- Request validation
- Audit logging

---

# 11. Architecture Decisions

| Decision | Reason |
|----------|--------|
| REST APIs | Standard integration |
| JWT Authentication | Stateless security |
| API Gateway | Centralized routing |
| Versioned APIs | Backward compatibility |
| RBAC | Fine-grained authorization |

---

# 12. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Unauthorized access | JWT + RBAC |
| API abuse | Rate limiting |
| Breaking API changes | Versioning |
| Service unavailability | Retry & circuit breaker |

---

# 13. Related Documents

- 05 Prisma Schema
- 14 Events Published
- 15 Events Consumed
- API Gateway Architecture (Phase 1.5)
- Authentication Architecture (Phase 1.5)

---

# 14. Conclusion

The Auth Service API dependency model establishes clear contracts between the authentication system and the rest of the EHMS platform. Standardized APIs, centralized authentication, and secure communication ensure that every application and microservice can rely on a consistent and scalable identity infrastructure.