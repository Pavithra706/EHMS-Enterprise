# Auth Service Events Consumed

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Events Consumed |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service subscribes to domain events published by other EHMS microservices.

These events allow the Auth Service to synchronize authentication identities, account status, and security information without requiring synchronous API calls.

The Auth Service processes incoming events asynchronously through RabbitMQ.

---

# 1. Purpose

This document defines:

- Consumed events
- Event sources
- Event handling
- Retry strategy
- Failure handling
- Security considerations

---

# 2. Event Consumption Principles

The Auth Service follows:

- Consume business events only
- Idempotent event processing
- Versioned event payloads
- At-least-once delivery
- Automatic retries
- Dead Letter Queue support

---

# 3. RabbitMQ Configuration

Exchange

```
ehms.events.exchange
```

Exchange Type

```
topic
```

Queue

```
auth-service.queue
```

---

# 4. Events Consumed

| Event | Source Service |
|---------|----------------|
| UserCreated | User Service |
| UserUpdated | User Service |
| UserDeleted | User Service |
| EmployeeActivated | HR Service |
| EmployeeDeactivated | HR Service |
| DoctorActivated | Doctor Service |
| DoctorDeactivated | Doctor Service |
| NurseActivated | Nurse Service |
| NurseDeactivated | Nurse Service |
| PatientRegistered | Patient Service |

---

# 5. UserCreated

Published By

```
User Service
```

Purpose

Create authentication identity.

Payload

```json
{
  "userId": "uuid",
  "email": "user@example.com",
  "username": "doctor01"
}
```

Action

- Create authentication record
- Initialize account
- Await password setup

---

# 6. UserUpdated

Purpose

Synchronize authentication data.

Updates

- Email
- Username
- Account status

---

# 7. UserDeleted

Purpose

Disable authentication.

Action

- Revoke sessions
- Revoke refresh tokens
- Disable login
- Preserve audit history

---

# 8. EmployeeActivated

Purpose

Enable authentication.

Action

```
status = ACTIVE
```

---

# 9. EmployeeDeactivated

Purpose

Prevent login.

Action

- Revoke sessions
- Disable account

---

# 10. Doctor/Nurse Events

Purpose

Synchronize employment status.

Example

```
DoctorActivated

↓

Enable Authentication
```

```
DoctorDeactivated

↓

Disable Authentication
```

---

# 11. PatientRegistered

Purpose

Initialize patient authentication.

Action

- Create patient login
- Send verification email
- Create default role assignment

---

# 12. Event Processing Flow

```mermaid
flowchart LR

RabbitMQ

↓

Receive Event

↓

Validate Event

↓

Check Version

↓

Execute Business Logic

↓

Acknowledge Message
```

---

# 13. Error Handling

If processing fails:

1. Retry
2. Log error
3. Retry with backoff
4. Send to Dead Letter Queue
5. Notify operations if required

---

# 14. Idempotency

Each event includes:

```
eventId
```

Processed event IDs should be tracked to prevent duplicate processing.

---

# 15. Security

Validate:

- Event source
- Event schema
- Event version
- Message integrity

Reject malformed or unauthorized events.

---

# 16. Monitoring

Monitor:

- Event throughput
- Processing latency
- Retry count
- Failed events
- Dead Letter Queue size
- Consumer availability

---

# 17. Architecture Decisions

| Decision | Reason |
|----------|--------|
| RabbitMQ | Loose coupling |
| Idempotent consumers | Safe retries |
| Dead Letter Queue | Failure recovery |
| Event versioning | Compatibility |
| Async processing | Scalability |

---

# 18. Related Documents

- 13 API Dependencies
- 14 Events Published
- RabbitMQ Architecture (Phase 1.5)
- Event Driven Architecture (Phase 1.5)

---

# 19. Conclusion

The Auth Service consumes business events from other EHMS services to maintain synchronized authentication data while preserving service independence. Event-driven communication improves scalability, resilience, and reduces direct service dependencies.