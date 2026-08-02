# Auth Service Migration Plan

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Migration Plan |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the migration strategy for the Auth Service database.

Database schema changes are managed using Prisma Migrate, ensuring consistent, version-controlled, and repeatable deployments across all environments.

---

# 1. Purpose

This document defines:

- Migration workflow
- Migration sequence
- Deployment process
- Rollback strategy
- Environment-specific execution
- Best practices

---

# 2. Migration Principles

EHMS follows:

- Version-controlled migrations
- Incremental schema evolution
- One logical change per migration
- Forward-only migrations
- Automated validation
- Production-safe deployments

---

# 3. Migration Lifecycle

```mermaid
flowchart LR

Schema Update

↓

Generate Migration

↓

Review

↓

Test

↓

Commit

↓

CI Validation

↓

Deploy
```

---

# 4. Migration Sequence

The Auth Service database should be created in the following order:

| Order | Table |
|--------|-------|
| 1 | users |
| 2 | roles |
| 3 | permissions |
| 4 | user_roles |
| 5 | role_permissions |
| 6 | refresh_tokens |
| 7 | user_sessions |
| 8 | login_history |
| 9 | password_reset_tokens |
| 10 | email_verification_tokens |
| 11 | mfa_configurations |

This sequence ensures that foreign key dependencies are satisfied.

---

# 5. Migration Naming

Examples

```text
001_initial_schema

002_create_users

003_create_roles

004_create_permissions

005_create_user_roles

006_create_role_permissions

007_create_refresh_tokens

008_create_user_sessions

009_create_login_history

010_create_password_reset_tokens

011_create_email_verification_tokens

012_create_mfa_configurations

013_add_indexes
```

Migration names should clearly describe the schema change.

---

# 6. Prisma Commands

Generate migration

```bash
pnpm prisma migrate dev --name create_users
```

Deploy migrations

```bash
pnpm prisma migrate deploy
```

Check migration status

```bash
pnpm prisma migrate status
```

Reset development database

```bash
pnpm prisma migrate reset
```

---

# 7. Environment Strategy

| Environment | Strategy |
|-------------|----------|
| Development | prisma migrate dev |
| Testing | prisma migrate deploy |
| Staging | prisma migrate deploy |
| Production | prisma migrate deploy |

**Do not use `prisma db push` in production.**

---

# 8. Rollback Strategy

If a migration fails:

1. Stop deployment
2. Investigate the issue
3. Restore from backup if required
4. Apply a corrective migration
5. Re-run deployment

Avoid editing previously applied migrations.

---

# 9. Migration Validation

Before deployment verify:

- Schema compiles
- Foreign keys are valid
- Indexes are created
- Constraints exist
- Seed data executes successfully
- Application tests pass

---

# 10. Seed Integration

Migration order:

```text
Run Migrations

↓

Execute Seed Scripts

↓

Start Application
```

Seed execution must occur only after successful migrations.

---

# 11. CI/CD Integration

Pipeline

```mermaid
flowchart LR

Git Push

↓

GitHub Actions

↓

Validate Prisma Schema

↓

Run Tests

↓

Validate Migration

↓

Deploy
```

---

# 12. Production Checklist

Before production deployment:

- Backup database
- Review migration
- Verify rollback plan
- Validate schema
- Confirm seed compatibility
- Monitor deployment

---

# 13. Migration History

Migration history is maintained by Prisma in the `_prisma_migrations` table.

This table must never be modified manually.

---

# 14. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Prisma Migrate | Version control |
| Forward-only migrations | Safer production |
| Incremental changes | Easier review |
| CI validation | Prevent deployment failures |
| Backup before deployment | Data protection |

---

# 15. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Failed migration | Backup & recovery |
| Schema drift | Migration validation |
| Data loss | Automated backups |
| Dependency issues | Ordered migrations |

---

# 16. Related Documents

- 05 Prisma Schema
- 09 Seed Data
- Enterprise Migration Strategy
- Deployment Architecture

---

# 17. Conclusion

The Auth Service Migration Plan provides a structured process for managing schema evolution throughout the project lifecycle. By using version-controlled Prisma migrations, validated deployment pipelines, and disciplined rollout procedures, the Auth Service database remains reliable, maintainable, and production-ready.