# Lab 08: Databases in Practice 
## Problem Statement  

**Dr. Dee Tah – Data Scientist**  

Our database administrators have recently complained that they spend too much time with operational tasks, such as patching and managing database infrastructure, instead of innovating for our customers. We heard that AWS might have a solution that will protect us from data loss and make sure our systems are resilient in case of a disaster.  

In addition, our Data Analytics team is constantly running real-time queries and big data analytics. Data performance is impacted with each large read load.  

---

## Solution Approach  

To address the problem, we implemented **Amazon RDS** with features for resilience, backup, and performance:  

1. **Amazon RDS for Managed Database**  
   - Offloads patching, backups, and infrastructure management to AWS.  
   - Reduces operational burden for database administrators.  

2. **Automated Backups**  
   - Daily backups with **point-in-time recovery** protect against data loss.  
   - Snapshots can be retained for disaster recovery scenarios.  

3. **Multi-AZ Deployment**  
   - Provides **high availability** with synchronous replication to a standby in another Availability Zone.  
   - Ensures automatic failover in case of primary DB failure.  

4. **Read Replica for Performance**  
   - Offloads **read-heavy workloads** (analytics, BI queries) to replicas.  
   - Improves performance and reduces latency for real-time queries.  

5. **Architecture Diagram**  
   ![Architecture Diagram](../evidence/lab08/Architecture-Diagram.png)  

6. **Outcome**  
   - Frees DBAs from routine maintenance tasks.  
   - Protects data through automated backups and recovery options.  
   - Ensures resilience and high availability with Multi-AZ.  
   - Enhances performance for big data analytics with read replicas.  

**AWS Services Used:** Amazon RDS, AWS IAM.  

---

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Solution)  

| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Solution |  
|-------------------|--------------------------------|---------------------------|  
| A.5.15 – Access control | Unauthorized access to the database | IAM roles and RDS authentication manage access to the DB instance |  
| A.8.13 – Data backup | Data loss due to accidental deletion or corruption | Automated RDS backups and point-in-time recovery |  
| A.5.30 – ICT readiness for business continuity | Database outage due to AZ failure | Multi-AZ deployment ensures automatic failover and resilience |  
| A.5.23 – Information security in use of cloud services | Performance and availability risks in cloud-based services | RDS Read Replicas offload read traffic and support service continuity |  

---

## Evidence & Files  

- Screenshot(s) in `evidence/lab08/` showing:  
  - RDS instance creation with Multi-AZ enabled.  
  - Backup configuration and automated snapshot.  
  - Read replica setup for performance scaling.  
  - Architecture diagram of RDS with Multi-AZ and read replica.  

---

## Lessons Learned & Notes  

### Offload Operations with Managed Services  
- Amazon RDS automates tasks like patching and backups, reducing DBA workload.  

### Prioritize High Availability  
- Multi-AZ ensures database resiliency and disaster recovery capabilities.  

### Optimize for Performance  
- Read replicas improve read scalability for analytics teams.  

### Protect Against Data Loss  
- Automated backups and snapshots safeguard critical business data.  

---

## Future Improvements  

1. **Explore Amazon Aurora**  
   - Use Aurora for improved scalability and performance beyond standard RDS engines.  

2. **Enable Cross-Region Read Replicas**  
   - Improve disaster recovery and support global analytics teams.  

3. **Integrate AWS Backup**  
   - Centralize and automate RDS backup management for compliance.  

4. **Enhance Security with KMS**  
   - Encrypt RDS data with **AWS Key Management Service** for stronger protection.  

5. **Add Monitoring and Alerts with CloudWatch**  
   - Use **Amazon CloudWatch** to monitor RDS performance metrics (CPU, connections, latency).  
   - Set up alerts for anomalies or unusual activity to strengthen operational oversight.  

