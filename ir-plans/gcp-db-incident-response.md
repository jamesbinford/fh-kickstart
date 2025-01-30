# GCP Database Incident Response Plan

## 1. Database Infrastructure Overview
- Primary: Production database instance (high-availability configuration)
- Replicas: Read replicas across multiple zones
- Backup: Automated backups and point-in-time recovery
- Monitoring: Cloud Monitoring with custom metrics

## 2. Incident Detection & Initial Assessment

### Monitoring Systems
- Primary: Cloud Monitoring (formerly Stackdriver)
- Secondary: Custom Prometheus metrics
- Alert channels: PagerDuty, Slack (#db-incidents)

### Initial Assessment Checklist
1. Check GCP Cloud SQL/MongoDB Atlas status
2. Review Cloud Monitoring alerts
3. Verify database connectivity
4. Check database metrics and logs
5. Determine incident severity (P1-P4)

## 3. Database-Specific Response Actions

### Connectivity Issues
1. Check network connectivity and VPC settings
2. Verify firewall rules and authorized networks
3. Review SSL certificate status
4. Test connection from different sources
5. Verify IAM permissions and service accounts

### Performance Issues
1. Review current connections and thread usage
2. Check query performance and slow query logs
3. Monitor storage capacity and IOPS
4. Analyze memory usage and buffer pool stats
5. Review recent configuration changes

### Data Integrity Issues
1. Check replication status and lag
2. Verify backup integrity
3. Review transaction logs
4. Check for corruption indicators
5. Monitor data consistency metrics

## 4. Escalation Protocol

### P1 (Critical) - Complete Database Outage
- Immediate escalation to Database Admin team
- Page on-call SRE
- Notify: Engineering Manager, CTO
- Updates every 15 minutes

### P2 (High) - Severe Performance Degradation
- Escalate to Database team
- Notify: Application team leads
- Updates every 30 minutes

### P3/P4 (Medium/Low)
- Handle within Database team
- Escalate if not resolved within SLA
- Document in incident tracking system

## 5. Recovery Procedures

### Immediate Actions
1. Failover to standby instance if needed
2. Scale compute resources
3. Kill problematic queries/connections
4. Reset replication if necessary
5. Restore from backup if required

### Recovery Verification
1. Verify database connectivity
2. Check data consistency
3. Monitor replication status
4. Test application connectivity
5. Verify backup systems

## 6. Communication Plan

### Internal Updates
- Use Slack #db-incidents channel
- Update status page every 15 minutes
- Send email updates to stakeholders
- Document all actions in incident log

### External Communication
- Notify affected application teams
- Update status page for customer-facing issues
- Coordinate with PR for major incidents

## 7. Post-Incident Requirements

### Documentation
1. Detailed incident timeline
2. Root cause analysis
3. Performance impact assessment
4. Data loss assessment (if any)
5. Prevention recommendations

### Follow-up Actions
1. Schedule post-mortem within 24 hours
2. Update monitoring thresholds
3. Review and update backup strategies
4. Create tickets for identified improvements
5. Update disaster recovery procedures

## 8. Emergency Contacts

### Primary
- Database Admin Team: [Contact Details]
- SRE Team: [Contact Details]
- Security Team: [Contact Details]
- Application Teams: [Contact Details]

### Secondary
- GCP Support
- Database vendor support
- Network team
- Security incident response team

## 9. Database-Specific Commands

### MongoDB
```
db.serverStatus()
db.currentOp()
db.killOp()
rs.status()
```

### PostgreSQL
```
SELECT * FROM pg_stat_activity;
SELECT * FROM pg_locks;
SELECT pg_terminate_backend(pid);
SELECT * FROM pg_replication_slots;
```

### MySQL
```
SHOW PROCESSLIST;
SHOW SLAVE STATUS;
SHOW ENGINE INNODB STATUS;
KILL CONNECTION thread_id;
```

## 10. Reference Documentation
- GCP Cloud SQL Documentation
- Database-specific documentation
- Internal runbooks and playbooks
- Backup and recovery procedures
- High Availability configuration guide