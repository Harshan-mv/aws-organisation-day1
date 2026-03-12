# AWS Multi-Account Architecture with IAM Identity Center

## Overview

This project demonstrates how to design and implement a **secure AWS multi-account architecture** using:

- AWS Organizations
- AWS IAM Identity Center (SSO)
- IAM Permission Sets
- Role-Based Access Control (RBAC)

Instead of using a single AWS account, organizations commonly separate workloads into multiple accounts to improve **security, governance, and operational control**.

This repository documents the setup of a **multi-account AWS environment with centralized authentication and role-based permissions**.

---

## Architecture

AWS Organization Structure:

Root
│
├── Infrastructure OU
│   ├── Log Archive Account
│   ├── Network Account
│   └── Security Account
│
├── Security OU
│   ├── CloudTrail Administrator
│   └── Aggregator Account
│
├── Workloads OU
│   ├── Production Account
│   └── Developer Account
│
└── Management Account (Root)

This structure follows AWS **enterprise landing zone best practices**.

---

## AWS Services Used

- AWS Organizations
- AWS IAM Identity Center (SSO)
- AWS IAM
- AWS CloudTrail

---

## Step 1: Create AWS Organization

1. Navigate to **AWS Organizations**
2. Enable **All Features**
3. Create organizational units (OUs)
4. Add multiple AWS member accounts

Benefits:

- Account isolation
- Security boundaries
- Central governance

---

## Step 2: Create Organizational Units

The following OUs were created to logically group accounts:

| OU | Purpose |
|----|--------|
| Infrastructure OU | Shared infrastructure |
| Security OU | Security monitoring and audit |
| Workloads OU | Application environments |
| Sandbox OU | Testing and experiments |

---

## Step 3: Create AWS Accounts

Multiple AWS accounts were provisioned inside the organization.

| Account Name | Purpose |
|--------------|---------|
| Log Archive Account | Central log storage |
| Network Account | Shared networking |
| Security Account | Security monitoring |
| CloudTrail Administrator | Organization trail management |
| Aggregator Account | Security findings aggregation |
| Production Account | Production workloads |
| Developer Account | Development environment |

This separation improves **fault isolation and security management**.

---

## Step 4: Configure IAM Identity Center

IAM Identity Center was enabled for centralized authentication.

Configuration:

Identity Source:  

Users authenticate through the **AWS Access Portal** instead of logging into individual accounts.

---

## Step 5: Create Permission Sets

Different permission sets were created to enforce **least privilege access**.

| Permission Set | Purpose |
|---------------|--------|
| NetworkAdmin-access | Manage networking resources |
| LogAuditAccess-access | Read logs and perform audits |
| PowerUserAccess-DeveloperAccess | Developer access to deploy services |
| SecurityAdmin | Manage security services |
| ProdOperator | Operate production workloads |
| AdministratorAccess | Full administrative access |

These permission sets create **IAM roles automatically inside AWS accounts**.

---

## Step 6: Assign Permission Sets to Accounts

Each account was assigned a **specific permission set** according to its role.

| AWS Account | Permission Set |
|-------------|---------------|
| Security Account | SecurityAdmin |
| Dev Account | PowerUserAccess-DeveloperAccess |
| CloudTrail Administrator | LogAuditAccess-access |
| Log Archive Account | LogAuditAccess-access |
| Developer Account | PowerUserAccess-DeveloperAccess |
| Network Account | NetworkAdmin-access |
| Aggregator Account | LogAuditAccess-access |
| Production Account | ProdOperator |

This enforces **role-based access control (RBAC)**.

---

## How Access Works

Users log in via the **AWS Access Portal**:

After login they can select:

- AWS Account
- Assigned role

Example:

Developer Account → DeveloperAccess  
Network Account → NetworkAdmin  
Production Account → ProdOperator  

---

## Security Best Practices Implemented

- Avoided root account usage
- Centralized identity management
- Role-based access control
- Least privilege permissions
- Separation of workloads and infrastructure

---

## Learning Outcomes

Through this project I learned how to:

- Design a **multi-account AWS environment**
- Configure **IAM Identity Center for SSO**
- Implement **role-based access control across accounts**
- Apply **enterprise cloud governance practices**

---

## Author
Harshan MV
DevOps / Cloud Learning Project
