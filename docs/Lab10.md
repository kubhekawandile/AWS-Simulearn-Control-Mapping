# Lab 10: Auto-Healing and Scaling Applications  

## Problem Statement  

**Rusty Ketchum – Chief Game Officer**  

Our gaming café is trending, and customers can host their own game servers. However, we face several challenges:  

1. If an **EC2 instance crashes**, we cannot automatically replace it.  
2. Customers have a **daily server limit**, but we cannot enforce it automatically.  
3. Every **Tuesday from 8:00 PM to 1:00 AM**, we host a large gaming party, but we have no way to automatically schedule when servers should scale up and scale down.  

## Solution Approach  

To solve the problem, we implemented **Amazon EC2 Auto Scaling with scheduled scaling**:  

1. **Auto Scaling Group with Launch Configurations:**  
   - Ensures crashed instances are automatically replaced (self-healing).  
   - Defines minimum and maximum EC2 instance limits to enforce provisioning caps.  

2. **Scheduled Scaling:**  
   - Configures servers to scale up before the Tuesday event (7:45 PM).  
   - Scales servers back down after the event ends (1:15 AM).  

3. **Architecture Diagram:**  
   ![Architecture Diagram](../evidence/lab10/architecture-diagram10.png)  

4. **Outcome:**  
   - Game servers are resilient and self-heal when failures occur.  
   - Provisioning limits prevent resource abuse and ensure fair usage.  
   - Scheduled scaling reduces costs while meeting predictable demand.  

**AWS Services Used:** EC2 Auto Scaling, Launch Configurations, Scheduled Scaling, CloudWatch

---

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Diagram)  

| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Diagram |  
|-------------------|--------------------------------|--------------------------|  
| A.5.10 – Acceptable use of information and assets | Customers exceeding server limits and misusing resources | Auto Scaling instance limits |  
| A.5.21 – Configuration management | Inconsistent or misconfigured server instances | Launch configuration enforces standardized setup |  
| A.5.22 – Change management | Errors from manual provisioning and scaling changes | Auto Scaling automates changes safely |  
| A.5.23 – Information security in use of cloud services | Risks from unmanaged scaling and cloud resource misuse | Secure, controlled Auto Scaling implementation |  
| A.5.29 – Capacity management | Servers unavailable during peak gaming hours | Scheduled scaling ensures capacity when needed |  
| A.8.6 – Capacity management for information processing | Overload during high demand events | Dynamic scaling prevents service disruption |  
| A.8.14 – Redundancy of information processing facilities | Game downtime if a server crashes | Auto-healing replaces failed EC2 instances |  

---

## Evidence & Files  

- Screenshot(s) in `evidence/lab10/`:  
  - Auto Scaling Group creation with launch configuration  
  - Scheduled scaling policy for Tuesday event  
  - Termination of an instance showing auto-healing replacement  
  - CloudWatch metrics demonstrating scaling actions  

---

## Lessons Learned & Notes  

### Self-Healing Systems  
- Auto Scaling automatically replaces failed instances, reducing downtime and manual intervention.  

### Enforcing Resource Limits  
- Defining min/max instance limits enforces fair resource usage per customer.  

### Cost Optimization with Scheduling  
- Scheduled scaling provisions resources only when needed, optimizing operating costs.  

### Business Continuity  
- Auto Scaling enhances resiliency and availability, directly supporting ISO 27001 continuity requirements.  

---

## Future Improvements  

While the solution meets requirements, additional enhancements could strengthen it further:  

1. **Target Tracking Scaling Policies**  
   - Scale dynamically based on CPU utilization or network traffic.  

2. **AWS Lambda + EventBridge**  
   - Enforce daily provisioning limits with serverless automation.  

3. **AWS Systems Manager**  
   - Standardize patching, updates, and compliance across EC2 instances.  

4. **Multi-AZ Deployment**  
   - Increase fault tolerance by distributing servers across multiple Availability Zones.  

5. **CloudWatch Alarms**  
   - Proactively alert administrators of scaling failures or threshold breaches.  
