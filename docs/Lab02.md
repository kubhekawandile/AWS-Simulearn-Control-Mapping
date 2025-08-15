# Lab 02: Cloud First Steps

## Problem Statement

**Zap Gigabyte -  Cloud Infrastructure Manager** 

I'm managing our city's web portal team and facing challenges with our beach wave size prediction webpage. Our current system isn't reliable enough for residents who depend on this information for safe beach activities. We need a reliable, scalable hosting solution that can store daily prediction files, an HTML file for displaying data in tables, plus JavaScript and CSS files – all relatively small in size – and perform consistently even during high traffic periods.

## Solution Approach

To address the problem, we deployed **EC2 instances across multiple Availability Zones (AZs)** with **Elastic Block Store (EBS) volumes** attached, along with **auto-scaling**:

1. **EC2 Deployment Across Multiple AZs:**  
   - Multiple EC2 instances were launched across at least two AZs to ensure fault tolerance.  
   - Auto Scaling Groups (ASGs) automatically adjust the number of instances based on workload.  

2. **EBS Volumes for Persistent Storage:**  
   - Each EC2 instance has an attached **EBS volume** for persistent block storage.  
   - **Snapshots** are taken regularly to allow recovery in case of volume failure or AZ disruption.  
   - EBS volumes are **encrypted at rest and in transit** to protect sensitive stabilization data.  

3. **Architecture Diagram**
   ![Architecture Diagram](../evidence/lab02/architecture-diagram.png)  
   
4. **Outcome:**  
   - High availability and fault tolerance are ensured.  
   - System workloads automatically shift to healthy instances in case of failure.  
   - Sensitive data is protected, and backups allow fast recovery.
    
**AWS Services Used:** EC2, Auto Scaling Groups, EBS with encryption & snapshots  

---

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Solution)

| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Solution |
|------------------|--------------------------------|---------------------------|
| A.5.33 – Protection of records | Unauthorized access to block storage data or tampering with critical stabilization information | EBS encryption (at rest & in transit) |
| A.8.12 – Data leakage prevention | Leakage of sensitive computational data that could destabilize the island | IAM roles & least privilege for EC2 and EBS access |
| A.8.13 – Backup | Loss of critical data due to AZ failure, volume corruption, or accidental deletion | EBS snapshots stored in S3 for recovery |
| A.8.14 – Redundancy of information processing facilities | Single point of failure in one AZ leading to system downtime | Multi-AZ EC2 deployment, Auto Scaling Groups |
| A.5.29 – Information security during disruption | Continuity of stabilization system during failures or high load | Auto Scaling ensuring workloads shift to healthy instances |

---

## Evidence & Files

- Screenshot(s) in `evidence/lab02/`  
- Architecture diagram showing EC2 instances and EBS volumes across multiple AZs

---

## Lessons Learned & Notes

### Multi-AZ EC2 Deployment & Auto Scaling
- Deploying EC2 instances in multiple AZs with auto-scaling improves **fault tolerance, redundancy, and availability**.  
- Workloads automatically shift to healthy instances if an AZ fails or instances are overloaded.  

### EBS for Persistent Block Storage
- EBS provides reliable storage with **snapshots** for recovery in case of failure.  
- Encryption protects sensitive data from unauthorized access and ensures integrity.  

### Shared Responsibility Model
- AWS secures the underlying infrastructure, but the user is responsible for:  
  - Configuring EBS encryption  
  - Managing IAM roles and access policies  
  - Implementing backup and recovery procedures  

### Risk Mitigation & High Availability
- Multi-AZ EC2 deployment reduces **single points of failure**.  
- EBS snapshots provide a **reliable backup and recovery mechanism**.  
- Auto Scaling ensures the system can **handle varying workloads** without disruption.
