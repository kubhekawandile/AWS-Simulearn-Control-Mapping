# Lab 06: Cloud Economics

## Problem Statement

**Penny Singleton – Cost Optimization Analyst**  

I want to set up my surf shop in the cloud, and I need some help. My biggest concern is cost. I notice my online store gets much more traffic during the day than at night. I think I could reduce my servers from four to two during nighttime hours. I need to figure out the costs, but I don't know where to start. Should I just copy my current setup? How do I find AWS hardware that matches what I'm using now?

## Solution Approach

To address the problem, we used the **AWS Pricing Calculator** to explore services and estimate the cost of running the surf shop in the cloud:  

1. **Logical Pricing Groups:**  
   - Create pricing groups for different workloads (daytime vs. nighttime traffic).  
   - Helps clearly visualize scaling strategies and associated costs.  

2. **Amazon EC2 Estimate:**  
   - Built an estimate for EC2 usage, showing costs for 4 instances during the day and 2 instances at night.  
   - Provides transparency and confidence before provisioning cloud resources.  

3. **Architecture Diagram**  
   ![Architecture Diagram](../evidence/lab06/Architecture-Diagram.png)  

4. **Outcome:**  
   - A clear cost model that shows expected charges before deployment.  
   - Ability to adjust instance types, storage, and scaling strategies to optimize expenses.  
   - Informed decision-making for right-sizing infrastructure.  

**AWS Services Used:** AWS Pricing Calculator, Amazon EC2.  

---

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Solution)

> Note: This scenario was not primarily risk-driven, but focused on **cost transparency and planning**. Relevant controls help ensure financial governance and responsible resource use.  

| ISO 27001 Control | Risk / Concern Addressed | AWS Feature from Solution |
|------------------|---------------------------|---------------------------|
| A.8.6 – Capacity management | Overspending due to overprovisioning or underutilization | Pricing Calculator models daytime vs. nighttime capacity |
| A.5.23 – Information security for use of cloud services | Unmanaged/ungoverned adoption of cloud services | Calculator-driven planning and documented assumptions before contracting |
| A.5.9 – Inventory of information and other associated assets | Misalignment between current hardware and AWS right-sizing | Use existing asset inventory to pick equivalent EC2 families/volumes in estimates |
| A.5.8 – Information security in project management | Lack of security/cost governance in cloud migration planning | Apply IS controls to estimation and planning project |

---

## Evidence & Files

- Screenshot(s) in `evidence/lab06/` showing:  
- AWS Pricing Calculator estimates for Amazon EC2.  
- Logical pricing groups (day vs. night usage).  
- Architecture diagram showing pricing groups and EC2 estimates linked to workloads.  

---

## Lessons Learned & Notes

### Importance of Cost Transparency
- Using the **AWS Pricing Calculator** provides a clear view of costs **before provisioning resources**.  

### Align Infrastructure to Workload
- Match **daytime vs. nighttime workloads** to EC2 instance counts, avoiding waste from overprovisioning.  

### Responsible Cloud Adoption
- Financial governance is just as important as technical security.  
- Cost visibility supports **informed decision-making** for cloud deployments.  

---

## Future Improvements

1. **Enable Auto Scaling**  
   - Implement **Amazon EC2 Auto Scaling** to automatically adjust instance counts based on real-time demand.  

2. **Consider Spot Instances for Cost Savings**  
   - Use **Amazon EC2 Spot Instances** for non-critical workloads to reduce costs further.  

3. **Integrate AWS Budgets and Cost Explorer**  
   - Monitor ongoing usage with **Cost Explorer**.  
   - Set **budget alerts** to avoid overspending.  

4. **Use Savings Plans or Reserved Instances**  
   - For predictable workloads, purchase **Savings Plans** or **Reserved Instances** to reduce long-term costs.  
