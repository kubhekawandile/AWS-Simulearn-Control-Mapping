# Lab 03: Automated EC2 Management

## Problem Statement

**Elias Gateway -  Systems Administrator** 


Our school's class scheduling system running on an Amazon EC2 instance is struggling to keep up with our growing needs, causing delays during peak registration periods. I need to find a way to develop a script that will let us access our machines, retrieve their metadata and status, and if necessary, change the instance type to enhance computing capacity. Is there a unified tool we could use to manage our AWS services, run commands, and automate these tasks through scripts?


## Solution Approach

To address the problem, we implemented **AWS Systems Manager (SSM)** with **AWS CLI** and automation scripts:

1. **AWS Systems Manager for Centralized Management**
- Session Manager provides secure shell access to EC2 instances without opening inbound ports.
- Run Command allows execution of scripts across multiple EC2 instances to retrieve metadata, system status, or perform updates.
- Automation Documents (SSM Documents)** automate instance type changes and other repetitive administrative tasks.

2. **AWS CLI Integration**
- Scripts use AWS CLI to query instance metadata, check CPU/memory usage, and trigger SSM automation workflows.
- Enables a **single toolchain** for monitoring and managing multiple EC2 instances at scale.

3. **Architecture Diagram**
*(Insert diagram showing EC2 instances managed via SSM, with CLI and automation workflows.)*


4. **Outcome**
- Centralized management of EC2 instances with automated metadata retrieval.
- Dynamic scaling of instance types during peak registration periods.
- Secure access and auditability of all administrative actions.
- Reduced operational overhead and improved system performance during high loads.


## AWS Services Used
- **EC2**
- **AWS Systems Manager (Session Manager, Run Command, Automation)**
- **AWS CLI**

---

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Solution)

| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Solution |
|------------------|--------------------------------|---------------------------|
| A.5.3 – Governance of information security | Mismanagement of instance scaling or metadata retrieval processes | SSM Automation with defined workflows ensures standardized, governed operations |
| A.5.15 – Roles & responsibilities | Unauthorized or inconsistent execution of administrative tasks | IAM roles for SSM and EC2 define clear responsibilities |
| A.5.17 – Access rights for users and systems | Unauthorized access to EC2 instances and scripts | Session Manager enforces secure access per IAM roles |
| A.5.18 – Authentication information | Exposure of credentials or API keys in scripts | AWS CLI uses temporary credentials via IAM roles; secure token management |
| A.5.29 – Access control for information systems | Unauthorized execution of automation or scripts | SSM enforces permissions and limits commands to authorized instances/users |
| A.8.2 – Inventory of assets | Lack of visibility into EC2 instances and configurations | SSM Inventory tracks all managed instances, metadata, and status |

---

## Evidence & Files

- Screenshot(s) in `evidence/lab03/` showing:
    - SSM session connections
    - Run Command executions
    - Automation workflow results
- Architecture diagram showing EC2 instances managed via SSM and CLI

---

## Lessons Learned & Notes

### Centralized Management with SSM
- AWS Systems Manager allows secure, scalable management of multiple EC2 instances without opening SSH ports.
- Run Command and Automation streamline administrative tasks and reduce manual effort.

### Secure Access & Role Definition
- Clearly defined IAM roles prevent unauthorized access to sensitive scripts and instance management.
- Session Manager and CLI credentials follow best practices for authentication and authorization.

### Automation & Scalability
- Automation Documents (SSM Documents) allow scripts to scale instances dynamically during peak periods.
- Metadata retrieval and status checks can be performed reliably across all instances.

### Shared Responsibility Model
- AWS secures the underlying infrastructure.
- Users are responsible for:
    - Configuring IAM roles and permissions
    - Implementing automation scripts securely
    - Maintaining inventory of EC2 instances

### Risk Mitigation & High Availability
- Automation reduces the chance of human error during instance management.
- Centralized monitoring and controlled access prevent unauthorized changes.
- Inventory tracking ensures visibility of all managed assets.

---

## Future Improvements

1. **Implement Monitoring & Alerts**
   - Integrate **CloudWatch** to track CPU, memory, and disk usage.
   - Configure alerts for high utilization to proactively trigger scaling automation.

2. **Integrate Auto Scaling Policies**
   - Connect SSM automation with **Auto Scaling Groups** for fully automated instance type adjustments based on predefined metrics.

3. **Use Infrastructure as Code (IaC)**
   - Deploy EC2, IAM roles, and SSM automation using **CloudFormation** or **Terraform**.
   - Ensures repeatable, version-controlled deployments and reduces manual errors.
