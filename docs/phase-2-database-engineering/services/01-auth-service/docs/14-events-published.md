# Auth Service Events Published

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Events Published |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service publishes domain events whenever significant authentication or authorization activities occur.

These events are delivered asynchronously through RabbitMQ, enabling other services to react without introducing direct dependencies.

---

# 1. Purpose

This document defines:

- Published events
- Event payloads
- Event routing
- Event versioning
- Delivery guarantees
- Best practices

---

# 2. Event Publishing Principles

The Auth Service follows:

- Publish only business events
- Publish after successful database transaction
- Immutable event payloads
- Versioned events
- At-least-once delivery
- Idempotent consumers

---

# 3. RabbitMQ Exchange

Exchange

```
ehms.auth.exchange
```

Type

```
topic
```

Routing Key Pattern

```
auth.<entity>.<action>
```

Examples

```
auth.user.login

auth.user.logout

auth.role.assigned

auth.password.changed
```

---

# 4. Published Events

| Event | Routing Key |
|---------|-------------|
| UserLoggedIn | auth.user.login |
| UserLoggedOut | auth.user.logout |
| PasswordChanged | auth.password.changed |
| PasswordResetRequested | auth.password.reset.requested |
| PasswordResetCompleted | auth.password.reset.completed |
| EmailVerified | auth.email.verified |
| MFAEnabled | auth.mfa.enabled |
| MFADisabled | auth.mfa.disabled |
| RoleAssigned | auth.role.assigned |
| RoleRemoved | auth.role.removed |
| PermissionGranted | auth.permission.granted |
| PermissionRevoked | auth.permission.revoked |
| AccountLocked | auth.account.locked |
| AccountUnlocked | auth.account.unlocked |

---

# 5. Standard Event Structure

Every event follows:

```json
{
  "eventId": "uuid",
  "eventType": "UserLoggedIn",
  "eventVersion": "1.0",
  "timestamp": "2026-08-03T10:15:00Z",
  "service": "auth-service",
  "correlationId": "uuid",
  "data": {}
}
```

---

# 6. UserLoggedIn Event

Published when:

- Login succeeds

Payload

```json
{
  "userId": "uuid",
  "username": "doctor01",
  "sessionId": "uuid",
  "loginTime": "timestamp",
  "ipAddress": "192.168.1.10"
}
```

Consumers

- Audit Service
- Notification Service
- Analytics Service

---

# 7. PasswordChanged Event

Published after:

- Successful password update

Payload

```json
{
  "userId": "uuid",
  "changedAt": "timestamp"
}
```

Consumers

- Audit Service
- Notification Service

---

# 8. AccountLocked Event

Published when:

- Failed login threshold exceeded
- Administrator locks account

Consumers

- Notification Service
- Audit Service

---

# 9. RoleAssigned Event

Payload

```json
{
  "userId": "uuid",
  "roleId": "uuid",
  "assignedBy": "uuid"
}
```

Consumers

- Audit Service
- Analytics Service

---

# 10. Delivery Guarantees

Events are published:

- After transaction commit
- At least once
- In JSON format
- With retry support
- Through durable queues

Consumers must be idempotent.

---

# 11. Error Handling

If publishing fails:

1. Retry publish
2. Log failure
3. Store in Outbox (recommended)
4. Retry through background worker
5. Send to Dead Letter Queue if necessary

---

# 12. Event Versioning

Pattern

```
eventVersion

1.0

↓

2.0
```

Breaking payload changes require a new event version.

---

# 13. Security

Events must never contain:

- Passwords
- Password hashes
- JWT tokens
- Refresh tokens
- MFA secrets

Sensitive data should always be excluded or masked.

---

# 14. Monitoring

Track:

- Published events
- Failed publications
- Retry attempts
- Queue depth
- Dead Letter Queue messages
- Consumer acknowledgements

---

# 15. Architecture Decisions

| Decision | Reason |
|----------|--------|
| RabbitMQ Topic Exchange | Flexible routing |
| JSON payloads | Interoperability |
| Versioned events | Backward compatibility |
| Outbox Pattern | Reliable delivery |
| Idempotent consumers | Safe retries |

---

# 16. Related Documents

- 13 API Dependencies
- 15 Events Consumed
- Event Driven Architecture (Phase 1.5)
- RabbitMQ Architecture (Phase 1.5)

---

# 17. Conclusion

The Auth Service publishes authentication and authorization events that allow other EHMS microservices to react asynchronously without direct coupling. Standardized event structures, reliable delivery, and versioned payloads ensure a scalable and maintainable event-driven architecture.