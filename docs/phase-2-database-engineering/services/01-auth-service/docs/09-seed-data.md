# Auth Service Seed Data

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Seed Data |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document defines the initial seed data required by the Auth Service.

Seed data initializes the authentication system with default roles, permissions, administrative accounts, and security configurations required for EHMS to function after deployment.

All seed scripts must be idempotent and safe to execute multiple times.

---

# 1. Purpose

This document defines:

- Default roles
- Default permissions
- Role-permission mappings
- Default administrator account
- System configuration
- Seed execution order

---

# 2. Seed Principles

The Auth Service follows:

- Idempotent execution
- Version-controlled seed scripts
- Reference data only
- No business transaction data
- Secure password initialization
- Environment-aware configuration

---

# 3. Default Roles

The following roles are seeded.

| Role | Description |
|------|-------------|
| Super Admin | Full system access |
| Hospital Admin | Hospital administration |
| Doctor | Clinical operations |
| Nurse | Nursing operations |
| Receptionist | Patient registration |
| Laboratory Technician | Laboratory operations |
| Radiologist | Radiology operations |
| Pharmacist | Pharmacy operations |
| Cashier | Billing operations |
| Patient | Patient portal access |

---

# 4. Default Permissions

Permission naming convention:

```
<resource>.<action>
```

Examples

```
patient.read

patient.create

patient.update

patient.delete

doctor.read

doctor.update

appointment.create

appointment.cancel

ehr.read

ehr.update

billing.create

billing.read

pharmacy.dispense

lab.result.update

radiology.report.view

user.manage

role.manage

permission.manage
```

---

# 5. Role-Permission Mapping

## Super Admin

Receives every permission.

---

## Doctor

Examples

```
patient.read

appointment.read

appointment.update

ehr.read

ehr.update

prescription.create
```

---

## Nurse

Examples

```
patient.read

appointment.read

vitals.update

medication.administer
```

---

## Receptionist

Examples

```
patient.create

patient.update

appointment.create

appointment.cancel
```

---

## Patient

Examples

```
profile.read

profile.update

appointment.read

appointment.create

lab.result.read

billing.read
```

---

# 6. Default Administrator

Initial administrator account

| Field | Value |
|--------|--------|
| Username | admin |
| Email | admin@ehms.local |
| Password | Generated securely during deployment |
| Role | Super Admin |

**The initial password must be changed immediately after first login.**

---

# 7. Password Policy

Seeded configuration:

- Minimum length: 12 characters
- Uppercase required
- Lowercase required
- Numeric required
- Special character required
- Password history: 5 passwords
- Expiration: Configurable by policy

---

# 8. MFA Defaults

Default configuration:

- Disabled by default
- Available for all users
- Mandatory for administrators (recommended)

---

# 9. Seed Execution Order

Execute in the following order:

1. Roles
2. Permissions
3. RolePermissions
4. Administrator User
5. UserRole
6. Security Configuration

Dependencies must always be respected.

---

# 10. Seed File Structure

```
prisma/

├── seed.ts

└── seeds/

    ├── roles.ts

    ├── permissions.ts

    ├── role_permissions.ts

    ├── admin_user.ts

    └── security_config.ts
```

---

# 11. Prisma Seed Command

Run

```bash
pnpm prisma db seed
```

Database reset

```bash
pnpm prisma migrate reset
```

---

# 12. Validation Checklist

After seeding verify:

- Super Admin role exists
- Default permissions exist
- Role-permission mappings exist
- Administrator account exists
- Administrator assigned Super Admin role
- No duplicate records

---

# 13. Security Considerations

- Never commit production passwords.
- Store passwords as secure hashes.
- Rotate default credentials after deployment.
- Protect seed scripts from unauthorized modification.
- Use environment variables for sensitive values.

---

# 14. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Seed roles | Required for RBAC |
| Seed permissions | Standard authorization |
| Seed admin | Initial access |
| Idempotent scripts | Safe repeated execution |
| Secure password generation | Better security |

---

# 15. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Duplicate records | Idempotent logic |
| Weak default password | Force password change |
| Missing permissions | Validation checks |
| Incorrect role mappings | Automated testing |

---

# 16. Related Documents

- 05 Prisma Schema
- 07 Constraints
- Enterprise Seed Data Strategy
- Authorization (RBAC)

---

# 17. Conclusion

The Auth Service Seed Data provides the minimum security configuration required to initialize EHMS. Through predefined roles, permissions, administrator access, and secure initialization practices, the system is ready for controlled deployment while maintaining enterprise security standards.