# Auth Service Performance Notes

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 2.2 – Service Database Engineering |
| Service | Auth Service |
| Document | Performance Notes |
| Version | 1.0 |
| Status | Approved |
| Author | Pavithra K V |

---

# Executive Summary

The Auth Service is one of the highest-traffic services in EHMS. Every login, token validation, permission check, session validation, and logout request passes through this service.

This document defines performance strategies that ensure the Auth Service remains responsive, scalable, and highly available under enterprise workloads.

---

# 1. Performance Objectives

| Metric | Target |
|---------|--------|
| Login Response Time | < 300 ms |
| JWT Validation | < 100 ms |
| Token Refresh | < 200 ms |
| Authorization Check | < 100 ms |
| Database Query Time | < 50 ms |
| Availability | 99.9% |

---

# 2. Expected Workload

Typical operations include:

- User login
- User logout
- Token refresh
- JWT validation
- Session validation
- Permission lookup
- Role lookup
- Login history recording
- MFA verification

These operations are read-heavy with frequent writes to audit tables.

---

# 3. Database Optimization

Recommended practices:

- Proper indexing
- Composite indexes
- Query optimization
- Prepared statements
- Connection pooling
- Efficient joins

Avoid:

- Full table scans
- Unnecessary joins
- SELECT *
- N+1 query problems

---

# 4. Connection Pooling

Use a connection pool between the application and PostgreSQL.

Recommended settings:

| Parameter | Value |
|-----------|-------|
| Min Connections | 5 |
| Max Connections | 30 |
| Idle Timeout | 300 seconds |
| Connection Timeout | 10 seconds |

Adjust values based on deployment size.

---

# 5. Query Optimization

Frequently executed queries:

- Find user by email
- Find user by username
- Validate refresh token
- Load user roles
- Load permissions
- Check active sessions

These queries should always use indexed columns.

---

# 6. Caching Strategy

Frequently accessed data may be cached using Redis.

Recommended cache candidates:

- Role definitions
- Permission definitions
- Role-permission mappings
- JWT public keys (if applicable)
- Security configuration

Do **not** cache:

- Password hashes
- Refresh tokens
- Active login sessions (unless the architecture explicitly supports distributed session caching)

---

# 7. Authentication Optimization

JWT validation should be performed without database access whenever possible.

Database access should occur only when:

- Refreshing tokens
- Revoking sessions
- Validating revoked tokens
- Checking account status (if required)

---

# 8. Session Management

Optimize session queries using indexes on:

- user_id
- status
- expires_at

Automatically clean expired sessions through scheduled background jobs.

---

# 9. Login History

Login history grows rapidly.

Recommendations:

- Archive old records
- Partition very large tables (future)
- Retain according to organizational policy

---

# 10. Monitoring

Monitor:

- Slow queries
- Authentication latency
- Database CPU usage
- Connection pool utilization
- Lock contention
- Failed login rates
- Cache hit ratio

---

# 11. Horizontal Scaling

The Auth Service should support:

- Multiple application instances
- Shared PostgreSQL database
- Redis cache
- RabbitMQ event broker
- Stateless JWT authentication

This allows the service to scale horizontally behind a load balancer.

---

# 12. Resource Optimization

Recommendations:

- Use pagination for audit history
- Limit returned columns
- Avoid unnecessary transactions
- Batch background cleanup tasks
- Archive historical data

---

# 13. Maintenance

Perform regularly:

- VACUUM
- ANALYZE
- REINDEX (when necessary)
- Remove expired tokens
- Remove expired password reset tokens
- Remove expired email verification tokens

---

# 14. Capacity Planning

Expected growth areas:

- Login history
- Refresh tokens
- User sessions
- Audit records

Monitor storage usage and plan database expansion proactively.

---

# 15. Performance Testing

Recommended testing includes:

- Load testing
- Stress testing
- Spike testing
- Endurance testing
- Concurrent login testing
- Token validation benchmarking

---

# 16. Architecture Decisions

| Decision | Reason |
|----------|--------|
| Redis caching | Reduce database load |
| Connection pooling | Improve throughput |
| Stateless JWT | Minimize database access |
| Background cleanup | Reduce operational overhead |
| Horizontal scaling | High availability |

---

# 17. Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Slow authentication | Proper indexing & caching |
| Database bottlenecks | Connection pooling |
| Large audit tables | Archiving strategy |
| Cache inconsistency | Clear cache invalidation rules |
| Connection exhaustion | Pool monitoring |

---

# 18. Related Documents

- 08 Index Strategy
- 11 Sample Queries
- 13 API Dependencies
- Enterprise Performance & Scalability Strategy

---

# 19. Conclusion

The Auth Service Performance Strategy ensures that authentication remains fast, reliable, and scalable as EHMS grows. By combining efficient indexing, Redis caching, connection pooling, monitoring, and proactive maintenance, the service can support enterprise-scale workloads while maintaining high availability and security.