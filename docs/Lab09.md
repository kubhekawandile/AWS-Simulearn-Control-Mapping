# Lab 09: Core Security Concepts
## Problem Statement

**Morgana Key – Security Analyst**

We have a growing Support Engineering team, and we need to give all team members the same access permissions. Can AWS help us manage this efficiently?  
My support engineers need access to both the AWS Management Console and developer tools. I also want to add them to the Support Engineering team when I create their accounts.

## Solution Approach

To address the problem, we implemented centralized identity and access management using AWS IAM:

1. **IAM Group for Support Engineers**  
  Provides a single place to manage access permissions for all support engineers.

2. **IAM Managed Policy – AmazonEC2ReadOnlyAccess**  
  Grants engineers read-only access to EC2 resources, applying the principle of least privilege.

3. **IAM Users**  
  Individual IAM users are created and attached to the group, enabling consistent, auditable access.

4. **Group-Based Access Management**  
  Simplifies onboarding by allowing new users to inherit permissions automatically upon being added to the group.

5. **Architecture Diagram**  
  ![Architecture Diagram](../evidence/lab09/Architecture-Diagram.png)

6. **Outcome**  
  Ensures efficient, secure, and scalable access management for the growing Support Engineering team.

AWS Services Used: **AWS IAM** (Groups, Users, Policies).

## ISO 27001:2022 Control–Risk Mapping (Using Only Services in Solution)
| ISO 27001 Control | Risk Mitigated in the Scenario | AWS Feature from Solution |
|---|---|---|
| A.5.2 – Information security roles and responsibilities | Lack of clarity in access permissions | IAM groups define clear responsibilities |
| A.5.3 – Segregation of duties | Risk of unauthorized infrastructure changes | Read-only policies prevent write/admin actions |
| A.5.15 – Access control | Unauthorized access to cloud resources | Group policy enforces least privilege |
| A.5.16 – Identity management | Inconsistent identity handling | Centralized IAM user and group management |
| A.5.18 – Access rights | Inappropriate access assignment | Standardized group permissions ensure consistency |
| A.5.20 – Authentication information | Weak or unmanaged authentication | IAM credentials (optionally MFA) strengthen authentication |
| A.5.30 – Use of privileged utility programs | Misuse of AWS console/CLI with admin rights | Read-only permissions limit exposure |

## Evidence & Files
- Screenshot(s) in `evidence/lab09/` showing:
  - IAM group creation for Support Engineers.
  - Managed EC2 ReadOnly policy attached to the group.
  - User created and added to the Support Engineers group.
  - Group membership verification in the AWS Console.
  - **Architecture diagram** depicting Users → Group → Managed Policy → EC2 (read-only).

## Lessons Learned & Notes
**Centralized Access Management**  
- IAM groups simplify administration and reduce human error in assigning permissions.

**Principle of Least Privilege**  
- Read-only policies ensure engineers can access what they need without risk of modification.

**Scalability and Onboarding**  
- New users can be quickly added to the group and inherit permissions automatically.

**Audit and Compliance**  
- IAM structures support clear evidence trails for access reviews and audits.

## Future Improvements
- **Enable MFA for All Users**  
  Strengthen authentication security for IAM users in the Support Engineers group.
- **Adopt AWS IAM Identity Center (SSO)**  
  Simplify large-scale user management by integrating with identity providers (e.g., Okta, Azure AD).
- **Attribute-Based Access Control (ABAC)**  
  Use tags and attributes to dynamically assign permissions as teams grow.
- **Enable AWS CloudTrail and CloudWatch**  
  Track and alert on login attempts, unauthorized access, or unusual user activity.
- **Regular Access Reviews**  
  Periodically audit group membership and policies to ensure they remain aligned with business needs.
