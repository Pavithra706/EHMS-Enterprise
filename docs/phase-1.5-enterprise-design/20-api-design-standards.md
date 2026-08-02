# API Design Standards

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | API Design Standards |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the API design standards for the Enterprise Hospital Management System (EHMS).

The standards ensure that all APIs are consistent, secure, maintainable, versioned, and easy to consume across web applications, mobile applications, third-party integrations, and internal microservices.

---

# 1. Purpose

This document aims to:

- Standardize REST APIs.
- Improve consistency.
- Simplify frontend integration.
- Improve maintainability.
- Support future API versions.
- Improve developer experience.

---

# 2. API Design Principles

EHMS follows:

- RESTful Architecture
- Resource-Oriented Design
- Stateless Communication
- Versioned APIs
- Consistent Responses
- Idempotent Operations
- Secure by Default

---

# 3. Base URL Structure

```
https://api.ehms.com/api/v1/
```

Examples:

```
GET /api/v1/patients
GET /api/v1/doctors
GET /api/v1/appointments
POST /api/v1/billing
```

---

# 4. HTTP Methods

| Method | Purpose |
|---------|----------|
| GET | Retrieve data |
| POST | Create resource |
| PUT | Replace resource |
| PATCH | Partial update |
| DELETE | Delete resource |

---

# 5. Resource Naming

Use:

- Plural nouns
- Lowercase
- Hyphen-separated when necessary

Examples

```
/patients
/doctors
/laboratory-orders
/appointments
/invoices
```

Avoid:

```
/getPatient
/createDoctor
```

---

# 6. Request Headers

Standard headers:

```
Authorization: Bearer <JWT>

Content-Type: application/json

Accept: application/json

X-Correlation-ID: UUID
```

---

# 7. Standard Response Format

Success

```json
{
  "success": true,
  "message": "Patient created successfully",
  "data": {},
  "metadata": {},
  "timestamp": "2026-01-01T10:30:00Z"
}
```

---

Error

```json
{
  "success": false,
  "error": {
    "code": "PATIENT_NOT_FOUND",
    "message": "Patient not found"
  },
  "timestamp": "2026-01-01T10:30:00Z",
  "traceId": "UUID"
}
```

---

# 8. HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

---

# 9. Pagination

Query Parameters

```
?page=1

?pageSize=20
```

Response

```json
{
  "data": [],
  "pagination": {
    "page": 1,
    "pageSize": 20,
    "totalRecords": 250,
    "totalPages": 13
  }
}
```

---

# 10. Filtering

Examples

```
GET /patients?gender=Female

GET /appointments?doctorId=DR001

GET /billing?status=PAID
```

---

# 11. Sorting

```
GET /patients?sort=firstName

GET /patients?sort=-createdAt
```

"-" indicates descending order.

---

# 12. Searching

```
GET /patients?search=John

GET /doctors?search=Cardiology
```

---

# 13. API Versioning

```
/api/v1/

/api/v2/
```

Rules:

- No breaking changes within a version.
- New major versions for incompatible changes.
- Deprecation notices before removal.

---

# 14. Validation Standards

Validate:

- Required fields
- String length
- Email format
- Phone numbers
- Date formats
- Business rules

Return HTTP **422** for validation failures.

---

# 15. Idempotency

The following operations must be idempotent:

- PUT
- DELETE

POST operations for payment or critical transactions should support an **Idempotency-Key** header to prevent duplicate processing.

---

# 16. Error Codes

Examples:

```
PATIENT_NOT_FOUND

INVALID_CREDENTIALS

APPOINTMENT_CONFLICT

PAYMENT_FAILED

LAB_ORDER_NOT_FOUND
```

---

# 17. Security Standards

Every API requires:

- HTTPS
- JWT Authentication
- RBAC Authorization
- Input Validation
- Output Encoding
- Audit Logging

---

# 18. Documentation Standards

All APIs must include:

- OpenAPI 3 Specification
- Request Examples
- Response Examples
- Error Responses
- Authentication Requirements
- Rate Limits

---

# 19. Performance Guidelines

Target Response Times:

| Endpoint Type | Target |
|--------------|--------|
| Authentication | <300 ms |
| Patient Search | <500 ms |
| Appointment Booking | <800 ms |
| Dashboard APIs | <1 second |
| Reports | <5 seconds |

---

# 20. Rate Limiting

| Client | Limit |
|---------|-------|
| Patient Portal | 100 req/min |
| Doctor Portal | 500 req/min |
| Admin Portal | 1000 req/min |
| External APIs | 50 req/min |

---

# 21. Architecture Decisions

| Decision | Reason |
|----------|--------|
| REST APIs | Simplicity |
| Versioning | Compatibility |
| Standard responses | Consistency |
| JWT | Stateless authentication |
| OpenAPI | Documentation |

---

# 22. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Inconsistent APIs | API standards |
| Breaking changes | Versioning |
| Duplicate requests | Idempotency |
| Invalid input | Validation |

---

# 23. Future Enhancements

Future improvements include:

- GraphQL Gateway
- gRPC for internal communication
- API Developer Portal
- SDK Generation
- API Analytics

---

# 24. Related Documents

- 09 API Gateway Design
- 17 Authentication Architecture
- 18 Authorization (RBAC)
- 21 Database Design Standards

---

# 25. Conclusion

The API Design Standards ensure that every EHMS API follows a consistent, secure, and maintainable design. By standardizing endpoints, request/response formats, validation, versioning, and documentation, the platform provides a reliable foundation for frontend applications, mobile clients, and third-party integrations.