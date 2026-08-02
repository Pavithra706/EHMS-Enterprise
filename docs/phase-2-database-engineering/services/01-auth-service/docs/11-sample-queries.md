# Auth Service Sample Queries

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Sample Queries |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

This document provides representative SQL and Prisma queries commonly executed by the Auth Service.

These examples support authentication, authorization, RBAC, session management, auditing, and security workflows.

---

# 1. Find User by Email

## SQL

```sql
SELECT *
FROM users
WHERE email = $1
AND is_deleted = FALSE;
```

## Prisma

```typescript
const user = await prisma.user.findUnique({
  where: {
    email: email
  }
})
```

---

# 2. Find User by Username

## SQL

```sql
SELECT *
FROM users
WHERE username = $1
AND is_deleted = FALSE;
```

---

# 3. Validate Login Credentials

```sql
SELECT id,
       email,
       password_hash,
       status
FROM users
WHERE email = $1
AND is_deleted = FALSE;
```

Password verification is performed by the application using Argon2 or bcrypt.

---

# 4. Get User Roles

```sql
SELECT r.name
FROM roles r
JOIN user_roles ur
ON r.id = ur.role_id
WHERE ur.user_id = $1;
```

---

# 5. Get User Permissions

```sql
SELECT DISTINCT p.name
FROM permissions p
JOIN role_permissions rp
ON p.id = rp.permission_id
JOIN user_roles ur
ON rp.role_id = ur.role_id
WHERE ur.user_id = $1;
```

---

# 6. Create Refresh Token

```sql
INSERT INTO refresh_tokens
(
user_id,
token_hash,
expires_at
)
VALUES
(
$1,
$2,
$3
);
```

---

# 7. Revoke Refresh Token

```sql
UPDATE refresh_tokens
SET revoked_at = NOW()
WHERE id = $1;
```

---

# 8. Create Login Session

```sql
INSERT INTO user_sessions
(
user_id,
ip_address,
device_name,
browser,
login_at,
status
)
VALUES
(
$1,
$2,
$3,
$4,
NOW(),
'ACTIVE'
);
```

---

# 9. Logout Session

```sql
UPDATE user_sessions
SET
logout_at = NOW(),
status = 'LOGGED_OUT'
WHERE id = $1;
```

---

# 10. Record Login Attempt

```sql
INSERT INTO login_history
(
user_id,
login_time,
ip_address,
login_result
)
VALUES
(
$1,
NOW(),
$2,
$3
);
```

---

# 11. Lock User Account

```sql
UPDATE users
SET
status = 'LOCKED'
WHERE id = $1;
```

---

# 12. Reset Failed Login Attempts

```sql
UPDATE users
SET
failed_login_attempts = 0
WHERE id = $1;
```

---

# 13. Assign Role

```sql
INSERT INTO user_roles
(
user_id,
role_id
)
VALUES
(
$1,
$2
);
```

---

# 14. Remove Role

```sql
DELETE
FROM user_roles
WHERE
user_id = $1
AND role_id = $2;
```

---

# 15. Active Sessions

```sql
SELECT *
FROM user_sessions
WHERE
user_id = $1
AND status = 'ACTIVE';
```

---

# 16. Expired Refresh Tokens

```sql
SELECT *
FROM refresh_tokens
WHERE
expires_at < NOW();
```

These records may be cleaned up by scheduled maintenance jobs.

---

# 17. Email Verification

```sql
UPDATE users
SET
email_verified = TRUE
WHERE id = $1;
```

---

# 18. Enable MFA

```sql
UPDATE mfa_configurations
SET enabled = TRUE
WHERE user_id = $1;
```

---

# 19. Audit Report

```sql
SELECT
login_time,
ip_address,
login_result
FROM login_history
WHERE user_id = $1
ORDER BY login_time DESC;
```

---

# 20. Performance Notes

Frequently executed queries should utilize indexes on:

- email
- username
- status
- user_id
- expires_at
- login_time

Review execution plans periodically using PostgreSQL's `EXPLAIN ANALYZE`.

---

# 21. Related Documents

- 05 Prisma Schema
- 07 Constraints
- 08 Index Strategy
- 12 Performance Notes

---

# 22. Conclusion

These sample queries represent the core operations performed by the Auth Service. They provide a practical reference for implementing authentication, authorization, session management, and auditing while following the indexing and constraint strategies defined for EHMS.