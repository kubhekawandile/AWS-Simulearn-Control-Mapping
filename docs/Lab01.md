# Lab 01: [Cloud Computing Essentials]

## Problem Statement

     Jack Mayers
     City Mayor

I'm managing our city's web portal team and facing challenges with our beach wave size prediction webpage. Our current system isn't reliable enough for residents who depend on this information for safe beach activities. I need help finding a reliable and scalable hosting solution for our wave prediction webpage that won't crash during peak seasons. We need to store daily prediction files, an HTML file that displays the data in tables, plus JavaScript and CSS files - all relatively small in size. How can we set this up to ensure consistent performance even during high traffic periods?

The city's web portal team wants a solution that will make their beach wave size prediction webpage more reliable.

## Solution Approach
- **AWS Services Used:** [S3 encryption + bucket policies, IAM roles & least privilege, and S3 encryption]
- **Architecture Diagram:** [Insert or link to image in evidence/lab01/]

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Diagram)

| **ISO 27001:2022 Control** | **Risk Mitigated in the Scenario** | **AWS Feature from Diagram** |
|----------------------------|------------------------------------|------------------------------|
| **A.5.15 – Access control** | • Unauthorized upload or change of prediction files causing **misinformation**.<br>• Accidental file deletion causing **loss of availability**.<br>• Public write access risk. | **S3 bucket policy** to allow only `s3:GetObject` for public, IAM access for authorized staff. |
| **A.5.29 – Information security in supplier relationships** | • Misunderstanding of AWS’s shared responsibility model leading to misconfiguration.<br>• Failure to secure data in AWS S3 causing service trust issues. | AWS S3 service with correctly configured access controls per shared responsibility guidance. |
| **A.8.3 – Information classification and handling** | • Integrity loss of critical public safety data.<br>• Inability to trace file changes for accountability.<br>• Public access to unprotected or corrupted files. | **Amazon S3** with server-side encryption (SSE-S3) and versioning enabled. |
| **A.5.30 – ICT readiness for business continuity** *(Suggested addition)* | • Website downtime during peak traffic season if storage can’t scale.<br>• Delays in residents receiving safety-critical wave data.<br>• No rapid recovery if storage fails. | **Amazon S3** provides high availability (99.99%) and scales automatically to meet traffic demand. |



## Evidence & Files
- [Screenshot](../evidence/lab01/screenshot1.png)


## Lessons Learned & Notes

1. **S3 for Static Website Hosting**  
   - Amazon S3 can host static websites (HTML, CSS, JS, data files) with high reliability.  
   - Server-side encryption (SSE) is available by default but **must be configured by the bucket owner** to meet security requirements.

2. **Importance of the Shared Responsibility Model**  
   - While AWS manages and maintains the physical infrastructure, **organizations remain responsible** for:  
     - Configuring SSE correctly.  
     - Managing access controls and bucket policies.  
     - Ensuring compliance with applicable regulations.  
   - Compliance is **built in through proper configuration**, not automatically applied.

3. **Risk Mitigation via Access Policies**  
   - Correctly implemented S3 bucket policies mitigate risks such as:  
     - Unauthorized access.  
     - Accidental or malicious modification/deletion of files.  
   - Access controls are a direct implementation of ISO 27001 Annex A.5.15 (Access Control).

4. **High Availability & Business Continuity**  
   - S3 offers **built-in high availability (99.99%)** and automatic scaling to handle variable or seasonal demand.  
   - This reduces the risk of downtime during peak usage periods, supporting **business continuity**.  
   - Some AWS services, like S3, come with embedded risk mitigation features (availability, scalability) by default.

---
