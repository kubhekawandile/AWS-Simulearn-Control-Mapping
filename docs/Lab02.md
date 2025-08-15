# Lab 02: Cloud First Steps

## Problem Statement

Zap Gigabyte  

I'm managing our city's web portal team and facing challenges with our beach wave size prediction webpage. Our current system isn't reliable enough for residents who depend on this information for safe beach activities. We need a reliable, scalable hosting solution that can store daily prediction files, an HTML file for displaying data in tables, plus JavaScript and CSS files – all relatively small in size – and perform consistently even during high traffic periods.

## Solution Approach

To address the problem, we deployed **EC2 instances across multiple Availability Zones (AZs)** with **Elastic Block Store (EBS) volumes** attached, along with **auto-scaling and load balancing**:

1. **EC2 Deployment Across Multiple AZs:**  
   - Multiple EC2 instances were launched across at least two AZs to ensure fault tolerance.  
   - Auto Scaling Groups (ASGs) automatically adjust the number of instances based on workload.  

2. **EBS Volumes for Persistent Storage:**  
   - Each EC2 instance has an attached **EBS volume** for persistent block storage.  
   - **Snapshots** are taken regularly to allow recovery in case of volume failure or AZ disruption.  
   - EBS volumes are **encrypted at rest and in transit** to protect sensitive stabilization data.  

3. **Elastic Load Balancer (ELB):**  
   - ELB distributes workload between EC2 instances across AZs, ensuring **high availability** and **reducing performance bottlenecks**.  

4. **Outcome:**  
   - High availability and fault tolerance are ensured.  
   - System workloads automatically shift to healthy instances in case of failure.  
   - Sensitive data is protected, and backups allow fast recovery.  
## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Diagram)

| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Diagram |
|------------------|--------------------------------|-------------------------|
| A.5.15 – Access control | Unauthorized upload or change of prediction files causing misinformation. Accidental file deletion causing loss of availability. Public write access risk. | S3 bucket policy to allow only `s3:GetObject` for public, IAM access for authorized staff. |
| A.5.29 – Information security in supplier relationships | Misunderstanding of AWS’s shared responsibility model leading to misconfiguration. Failure to secure data in AWS S3 causing service trust issues. | AWS S3 service with correctly configured access controls per shared responsibility guidance. |
| A.8.3 – Information classification and handling | Integrity loss of critical public safety data. Inability to trace file changes for accountability. Public access to unprotected or corrupted files. | Amazon S3 with server-side encryption (SSE-S3) and versioning enabled. |
| A.5.30 – ICT readiness for business continuity (Suggested addition) | Website downtime during peak traffic season if storage can’t scale. Delays in residents receiving safety-critical wave data. No rapid recovery if storage fails. | Amazon S3 provides high availability (99.99%) and scales automatically to meet traffic demand. |

---

## Evidence & Files

- Screenshot(s) in `evidence/lab01/`  
- Architecture diagram above shows the S3 bucket as the web portal source

---

## Lessons Learned & Notes

### S3 for Static Website Hosting
- Amazon S3 can host static websites (HTML, CSS, JS, data files) with high reliability.  
- Server-side encryption (SSE) is available by default but must be configured by the bucket owner to meet security requirements.

### Importance of the Shared Responsibility Model
- AWS manages the physical infrastructure, but the organization remains responsible for:
  - Configuring SSE correctly  
  - Managing access controls and bucket policies  
  - Ensuring compliance with applicable regulations  
- Compliance is achieved through proper configuration, not automatically applied.

### Risk Mitigation via Access Policies
- Correctly implemented S3 bucket policies mitigate risks such as:  
  - Unauthorized access  
  - Accidental or malicious modification/deletion of files  
- Access controls are a direct implementation of ISO 27001 Annex A.5.15 (Access Control).

### High Availability & Business Continuity
- S3 offers built-in high availability (99.99%) and automatic scaling to handle variable or seasonal demand.  
- This reduces the risk of downtime during peak usage periods, supporting business continuity.  
- Some AWS services, like S3, come with embedded risk mitigation features (availability, scalability) by default.
