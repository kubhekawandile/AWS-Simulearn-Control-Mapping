# Lab 11: Highly Available Web Applications
## Problem Statement  

**Owen Stack – Cloud Infrastructure Engineer**  

Our travel agency recently held a promotional event that dramatically increased web traffic, overloading our web application. All requests were timing out. Worse, our Amazon EC2 instances were hosted in a single Availability Zone that was affected by severe storms, leaving us offline for hours.  

We need a highly available, scalable solution that can handle sudden spikes in traffic and ensure redundancy across multiple Availability Zones.  

---

## Solution Approach  

To address the problem, we implemented **AWS Auto Scaling and Load Balancing**:  

1. **Auto Scaling Group Across Multiple AZs**  
   - Launch EC2 instances in multiple Availability Zones.  
   - Define minimum, maximum, and desired instance counts.  
   - Ensure redundancy and resilience against AZ-specific failures.  

2. **Application Load Balancer (ALB)**  
   - Distributes incoming traffic evenly across EC2 instances.  
   - Ensures no single instance or AZ becomes a bottleneck.  

3. **Attach Auto Scaling Group to Load Balancer**  
   - Automatically registers new instances with the load balancer.  
   - Ensures all traffic is directed to healthy instances.  

4. **Load Balancer Health Check**  
   - Monitors EC2 instance health.  
   - Replaces unhealthy instances automatically to maintain service availability.  

5. **CloudWatch Metrics**  
   - Monitors traffic, CPU, and memory utilization.  
   - Triggers Auto Scaling policies based on thresholds.  

6. **Architecture Diagram**  
   ![Architecture Diagram](../evidence/lab11/Architecture-Diagram.png)  

7. **Outcome**  
   - Application can handle spikes in traffic without downtime.  
   - Multi-AZ deployment increases availability and resilience.  
   - Automatic scaling optimizes resource usage and cost.  

**AWS Services Used:** Amazon EC2, Auto Scaling, Application Load Balancer (ALB), CloudWatch.  

---

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Solution)  

| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Solution |  
|-------------------|--------------------------------|---------------------------|  
| A.5.23 – Information security in project management | Poor planning or misconfiguration of cloud infrastructure | Auto Scaling and ALB deployment across multiple AZs |  
| A.5.24 – Information security in supplier relationships | Risk from cloud provider outages or mismanagement | AWS-managed infrastructure with shared responsibility model |  
| A.5.29 – Information security in business continuity management | Downtime due to traffic spikes or AZ failure | Multi-AZ Auto Scaling ensures continuity |  
| A.8.6 – Technical vulnerability management | Application unavailable due to instance failure | Auto Scaling replaces unhealthy EC2 instances |  
| A.8.8 – Exchange of information security responsibilities | Misunderstanding shared responsibilities | Clear delineation: AWS manages physical controls, user manages configurations |  
| A.8.13 – Backup and restoration | Data loss during instance failures | Optionally use AMIs or snapshots for recovery |  
| A.8.14 – Logging and monitoring | Lack of visibility into traffic and instance behavior | ELB access logs provide monitoring and traceability |  
| A.8.15 – Event logging | Untracked events may prevent incident detection | CloudWatch metrics trigger alerts and scaling events |  
| A.8.16 – Availability of information processing facilities | Single point of failure or capacity overload | ALB and Auto Scaling maintain service availability |  

---

## Evidence & Files  

- Screenshot(s) in `evidence/lab11/` showing:  
  - Auto Scaling group creation across multiple AZs.  
  - Load balancer setup and target group attachment.  
  - Health check configuration for EC2 instances.  
  - CloudWatch metric alarms configuration.  
  - Architecture diagram illustrating Multi-AZ deployment with Auto Scaling, ALB, and CloudWatch.  

---

## Lessons Learned & Notes  

### High Availability  
- Multi-AZ deployment ensures continued service even if one AZ fails.  

### Auto Scaling Benefits  
- Dynamically adjusts capacity based on traffic, optimizing costs and performance.  

### Load Balancing  
- Distributes traffic evenly to prevent bottlenecks and single points of failure.  

### Monitoring and Event Logging  
- CloudWatch metrics and ELB logs provide actionable insights and automated event-driven scaling.  

### Shared Responsibility Awareness  
- Physical security and infrastructure are AWS-managed; configuration and access remain user responsibility.  

---

## Future Improvements  

1. **Enable Cross-Region Load Balancing**  
   - Improve disaster recovery by routing traffic across multiple regions.  

2. **Integrate CloudWatch Metrics & Alarms**  
   - Automatically trigger scaling based on traffic patterns or instance health.  

3. **Implement Auto Scaling Policies for Cost Optimization**  
   - Scale in/out based on CPU, memory, or custom metrics.  

4. **Add Application-Level Monitoring**  
   - Use AWS X-Ray or ELB access logs for performance insights.  

5. **Periodic Failover Testing**  
   - Simulate AZ failures to validate resiliency and recovery procedures.  
