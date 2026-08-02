# Coding Standards

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 00 – Project Initiation |
| Document | Coding Standards |
| Version | 1.0 |
| Status | Draft |
| Author | Pavithra K V |
| Date | 2026-08-03 |

---

# Version History

| Version | Date | Description | Author |
|----------|------|-------------|--------|
| 1.0 | 2026-08-03 | Initial Version | Pavithra K V |

---

# Table of Contents

1. Purpose
2. General Principles
3. Python Coding Standards
4. React & TypeScript Standards
5. API Standards
6. Database Standards
7. Git Commit Standards
8. Documentation Standards
9. Code Review Checklist
10. Approval Status
11. References

---

# 1. Purpose

This document defines the coding standards for the Enterprise Hospital Management System (EHMS). Following a common standard improves readability, maintainability, collaboration, and software quality.

---

# 2. General Principles

All code should be:

- Readable
- Maintainable
- Modular
- Reusable
- Secure
- Well documented
- Properly tested

Avoid duplicated code wherever possible.

---

# 3. Python Coding Standards

The backend follows the Python style guide (PEP 8).

Guidelines:

- Use meaningful variable names.
- Use snake_case for variables and functions.
- Use PascalCase for classes.
- Keep functions focused on a single responsibility.
- Add type hints where appropriate.
- Write docstrings for public functions and classes.
- Handle exceptions gracefully.
- Avoid hard-coded values; use configuration files or constants.

Example:

```python
def get_patient_by_id(patient_id: int) -> Patient:
    """Retrieve a patient by unique identifier."""
```

---

# 4. React & TypeScript Standards

Frontend guidelines:

- Use functional components.
- Use PascalCase for component names.
- Use camelCase for variables and functions.
- Keep components small and reusable.
- Store shared logic in hooks or utilities.
- Define interfaces for props and API responses.
- Avoid inline styles where Tailwind utilities are sufficient.

---

# 5. API Standards

REST APIs should:

- Use nouns for resource names.
- Follow consistent endpoint naming.
- Return appropriate HTTP status codes.
- Validate all request data.
- Return structured JSON responses.
- Include meaningful error messages.

Example:

GET /api/v1/patients/{patientId}

POST /api/v1/patients

PUT /api/v1/patients/{patientId}

DELETE /api/v1/patients/{patientId}

---

# 6. Database Standards

- Use PostgreSQL naming conventions.
- Table names should be singular.
- Primary key: id
- Foreign keys should clearly reference parent tables.
- Avoid duplicated data.
- Use indexes where appropriate.
- Maintain referential integrity.

---

# 7. Git Commit Standards

Commit messages should follow the format:

type: short description

Examples:

docs: add technology stack

feat: implement patient registration

fix: resolve login validation issue

refactor: optimize appointment service

test: add unit tests for billing module

Supported commit types:

- feat
- fix
- docs
- refactor
- test
- chore
- ci
- style

---

# 8. Documentation Standards

Every major feature should include:

- Requirement
- Design
- API changes
- Database changes
- Testing notes

Documentation must be updated whenever functionality changes.

---

# 9. Code Review Checklist

Before merging code:

- Code compiles successfully.
- Tests pass.
- Documentation updated.
- No unnecessary code.
- No hard-coded secrets.
- Error handling implemented.
- Naming conventions followed.
- Security considerations reviewed.

---

# Approval Status

| Role | Status |
|------|--------|
| Project Owner | Pending |
| System Architect | Pending |
| Development Team | Pending |

---

# References

- PEP 8 – Python Style Guide
- FastAPI Best Practices
- React Documentation
- TypeScript Handbook
- REST API Design Guidelines