# Seed Data Strategy

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2 – Database Engineering |
| Document | Seed Data Strategy |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Seed Data Strategy defines how reference and master data are initialized across EHMS databases.

Seed data ensures that every environment starts with the required foundational information while preventing duplication and preserving data consistency.

Business transaction data is never seeded.

---

# 1. Purpose

This document defines:

- Seed data categories
- Seed execution process
- Environment strategy
- Seed ownership
- Versioning
- Best practices

---

# 2. Seed Principles

EHMS follows:

- Seed only reference data
- Idempotent seed execution
- Version-controlled seeds
- Environment-independent seeds
- Service-owned seed data
- Repeatable execution

---

# 3. Seed Categories

## Master Data

Examples:

- Departments
- Blood Groups
- Genders
- Countries
- States
- Cities

---

## Security Data

Examples:

- Roles
- Permissions
- Default Administrator
- System Users

---

## Configuration Data

Examples:

- Appointment Status
- Billing Status
- Payment Methods
- Notification Types

---

## Lookup Data

Examples:

- Marital Status
- Nationality
- Languages
- Insurance Types

---

# 4. Data That Must NOT Be Seeded

Never seed:

- Patients
- Doctors
- Employees
- Appointments
- Prescriptions
- Laboratory Results
- Billing Transactions
- Medical Records

These are created during normal application usage.

---

# 5. Seed Execution Flow

```mermaid
flowchart LR

Database Created

↓

Run Migrations

↓

Execute Seed Scripts

↓

Validate Seed Data

↓

Application Startup
```

---

# 6. Seed Structure

Example

```text
prisma/

├── schema.prisma

├── migrations/

├── seed.ts

└── seeds/

    ├── departments.ts

    ├── roles.ts

    ├── permissions.ts

    ├── statuses.ts

    └── payment_methods.ts
```

---

# 7. Prisma Seed Configuration

Example

```json
{
  "prisma": {
    "seed": "tsx prisma/seed.ts"
  }
}
```

---

# 8. Seed Execution

Development

```bash
pnpm prisma db seed
```

Reset database

```bash
pnpm prisma migrate reset
```

This recreates the database, applies migrations, and executes seed scripts.

---

# 9. Seed Ordering

Execute in the following order:

1. Roles
2. Permissions
3. Departments
4. Users
5. Configuration
6. Lookup Tables

Dependencies should always be respected.

---

# 10. Idempotency

Seed scripts must be safe to execute multiple times.

Preferred approach:

- Check existence
- Insert if missing
- Update only when appropriate

Avoid duplicate records.

---

# 11. Environment Strategy

| Environment | Seed Data |
|-------------|-----------|
| Development | Full reference data |
| Testing | Test reference data |
| Staging | Production-like reference data |
| Production | Approved reference data only |

---

# 12. Validation

After execution verify:

- Required records exist
- Relationships are valid
- No duplicates
- Foreign keys resolve correctly

Seed execution should fail if validation does not pass.

---

# 13. Security

Protect:

- Default credentials
- API keys
- Secrets

Default administrator passwords must be changed immediately after initial deployment.

Production secrets must never be included in seed files.

---

# 14. Monitoring

Track:

- Seed execution time
- Failed seeds
- Duplicate attempts
- Validation errors

Maintain logs for troubleshooting.

---

# 15. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Separate seed files | Maintainability |
| Idempotent execution | Safe reruns |
| Version control | Traceability |
| Reference data only | Protect business data |
| Validation | Reliable startup |

---

# 16. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Duplicate records | Idempotent logic |
| Missing lookup data | Validation |
| Wrong execution order | Dependency ordering |
| Default credential exposure | Password rotation |

---

# 17. Future Enhancements

Future improvements include:

- Seed version tracking
- Environment-specific seed packages
- Dynamic configuration loading
- Automated seed verification
- Seed reporting dashboards

---

# 18. Related Documents

- 08 Migration Strategy
- 13 Canonical Data Model (Phase 1.5)
- 14 Master Data Management (Phase 1.5)
- 21 Database Design Standards (Phase 1.5)

---

# 19. Conclusion

The Seed Data Strategy provides a standardized and repeatable process for initializing EHMS databases with essential reference information. Through idempotent execution, validation, and version control, seed data remains reliable across all environments while supporting consistent application behavior.