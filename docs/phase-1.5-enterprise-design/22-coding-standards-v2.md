# Coding Standards

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 1.5 – Enterprise Solution Design |
| Document | Coding Standards |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the coding standards for the Enterprise Hospital Management System (EHMS).

The standards ensure that all developers write clean, maintainable, secure, and consistent code across backend services, frontend applications, infrastructure, and automation scripts.

---

# 1. Purpose

This document aims to:

- Improve code readability.
- Standardize development practices.
- Reduce bugs.
- Improve maintainability.
- Support team collaboration.
- Enable automated quality checks.

---

# 2. General Principles

EHMS follows:

- Clean Code
- SOLID Principles
- DRY (Don't Repeat Yourself)
- KISS (Keep It Simple)
- YAGNI (You Aren't Gonna Need It)
- Separation of Concerns
- Single Responsibility Principle

---

# 3. Technology Stack

| Layer | Technology |
|--------|------------|
| Backend | FastAPI |
| Language | Python 3.13+ |
| Frontend | React + TypeScript |
| Database | PostgreSQL |
| ORM | Prisma |
| Messaging | RabbitMQ |
| Cache | Redis |
| Containerization | Docker |

---

# 4. Project Structure

Backend

```
backend/

gateway/

services/

shared/

workers/
```

Frontend

```
apps/

web-admin/

web-doctor/

web-patient/

mobile-doctor/
```

---

# 5. Python Coding Standards

Use:

- Type hints
- Meaningful names
- Small functions
- Docstrings for public APIs
- f-strings
- Constants for magic values

Example

```python
def get_patient(patient_id: UUID) -> Patient:
    """Retrieve a patient by ID."""
```

Avoid:

- Global variables
- Long functions
- Deep nesting
- Duplicate logic

---

# 6. FastAPI Standards

Each service should contain:

```
app/

api/

models/

schemas/

services/

repositories/

core/

dependencies/

middlewares/

tests/
```

Use dependency injection for shared services.

---

# 7. Naming Conventions

| Item | Convention |
|------|------------|
| Class | PascalCase |
| Function | snake_case |
| Variable | snake_case |
| Constant | UPPER_CASE |
| File | snake_case.py |
| Package | lowercase |

Examples

```
PatientService

create_patient()

patient_id

MAX_LOGIN_ATTEMPTS
```

---

# 8. Error Handling

Use centralized exception handling.

Never expose:

- Stack traces
- SQL errors
- Internal implementation details

Return standardized API errors.

---

# 9. Logging Standards

Every service logs:

- Startup
- Shutdown
- Authentication
- Errors
- Warnings
- Business Events

Use structured logging (JSON).

Never log:

- Passwords
- JWT tokens
- Secrets
- Sensitive medical information

---

# 10. Dependency Injection

Business logic must not directly instantiate repositories.

Correct

```
API

↓

Service

↓

Repository

↓

Database
```

---

# 11. Testing Standards

Minimum coverage target:

80%

Testing types:

- Unit
- Integration
- API
- End-to-End

Every new feature should include tests.

---

# 12. Code Formatting

Python

- Ruff
- Black
- isort

Frontend

- ESLint
- Prettier

Formatting runs automatically in CI.

---

# 13. Git Standards

Branch names

```
feature/patient-registration

feature/opd-module

fix/login-bug

docs/api-design
```

Commit format

```
feat:

fix:

docs:

refactor:

test:

ci:

build:

style:

perf:

chore:
```

Examples

```
feat: add patient registration API

fix: resolve appointment validation

docs: update architecture diagrams
```

---

# 14. Pull Request Standards

Every PR must include:

- Description
- Related Issue
- Test Evidence
- Screenshots (UI changes)
- Checklist

At least one approval is recommended before merging in a team environment.

---

# 15. Code Review Checklist

Review:

- Naming
- Readability
- Security
- Performance
- Error Handling
- Tests
- Documentation

---

# 16. Documentation Standards

Public APIs require:

- Docstrings
- OpenAPI documentation
- Examples
- Parameter descriptions

Complex business logic should include explanatory comments where helpful.

---

# 17. Security Guidelines

Never:

- Hardcode secrets
- Trust user input
- Disable authentication
- Commit .env files

Always:

- Validate input
- Sanitize output where appropriate
- Use parameterized queries
- Verify authorization

---

# 18. Performance Guidelines

Prefer:

- Pagination
- Lazy loading
- Efficient indexing
- Caching
- Async I/O

Avoid:

- N+1 queries
- Unnecessary loops
- Blocking operations

---

# 19. CI/CD Quality Gates

Every commit must pass:

- Linting
- Formatting
- Unit Tests
- Security Scan
- Dependency Check

Merges to the main branch require successful pipeline execution.

---

# 20. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Clean Architecture | Maintainability |
| Dependency Injection | Testability |
| Structured Logging | Observability |
| Automated Formatting | Consistency |
| CI Quality Gates | Reliability |

---

# 21. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Inconsistent code | Coding standards |
| Bugs | Testing |
| Security issues | Secure coding practices |
| Merge conflicts | Git workflow |

---

# 22. Future Enhancements

Future improvements include:

- AI-assisted code review
- Automated architecture validation
- Mutation testing
- Performance regression testing
- Static architecture analysis

---

# 23. Related Documents

- 20 API Design Standards
- 21 Database Design Standards
- 23 Observability Architecture
- 24 Deployment Architecture

---

# 24. Conclusion

The Coding Standards establish a common engineering approach for EHMS development. By following these standards, developers can build secure, maintainable, consistent, and high-quality software that supports the long-term evolution of the platform.