# Git Workflow

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 00 – Project Initiation |
| Document | Git Workflow |
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
2. Branching Strategy
3. Branch Naming Convention
4. Commit Message Convention
5. Development Workflow
6. Pull Request Guidelines
7. Release Strategy
8. Repository Rules
9. Approval Status
10. References

---

# 1. Purpose

This document defines the Git workflow used for the Enterprise Hospital Management System (EHMS). A consistent workflow helps maintain code quality, simplifies collaboration, and ensures a clear project history.

---

# 2. Branching Strategy

The repository follows a simplified Git Flow model.

## Main Branches

### main

- Stable production-ready code
- Protected branch
- Release versions only

### develop

- Primary development branch
- All completed features are merged here

## Feature Branches

Feature branches are created from the `develop` branch.

Examples:

- feature/authentication
- feature/patient-management
- feature/appointment-module
- feature/pharmacy-module
- feature/laboratory-module

---

# 3. Branch Naming Convention

| Branch Type | Example |
|-------------|---------|
| Feature | feature/patient-registration |
| Bug Fix | bugfix/login-validation |
| Hotfix | hotfix/security-patch |
| Documentation | docs/api-update |
| Refactor | refactor/auth-service |

---

# 4. Commit Message Convention

Every commit message should follow this format:

```
type: short description
```

Examples:

```
docs: add hospital study

feat: implement patient registration

fix: resolve appointment validation

refactor: simplify authentication service

test: add unit tests for pharmacy

ci: update GitHub Actions workflow
```

### Supported Types

- feat
- fix
- docs
- refactor
- test
- style
- ci
- chore

---

# 5. Development Workflow

The development process follows these steps:

1. Create a feature branch from `develop`.
2. Implement the feature.
3. Test the changes locally.
4. Update documentation if required.
5. Commit changes using the standard format.
6. Merge into `develop` after review.
7. Merge `develop` into `main` during a release.

---

# 6. Pull Request Guidelines

Every Pull Request should include:

- Summary of changes
- Related issue (if applicable)
- Testing completed
- Documentation updated
- Screenshots (for UI changes)

The Pull Request should be reviewed before merging.

---

# 7. Release Strategy

Releases will use Git tags.

Examples:

- v0.1.0
- v0.2.0
- v1.0.0

Major milestones, such as the completion of each project phase, may also be tagged.

---

# 8. Repository Rules

- Never commit secrets or passwords.
- Keep commits focused on a single task.
- Write meaningful commit messages.
- Update documentation when functionality changes.
- Ensure the project builds successfully before committing.
- Review code before merging.

---

# Approval Status

| Role | Status |
|------|--------|
| Project Owner | Pending |
| System Architect | Pending |
| Development Team | Pending |

---

# References

- Git Documentation
- GitHub Flow
- Git Flow Workflow