


## Purpose

This document maps applicable PCI DSS v4.0.1 requirements to planned AWS security controls, NovaPay implementation activities, and compliance evidence.

The control mapping is intended to demonstrate how NovaPay would translate PCI DSS requirements into technical and administrative controls within an AWS cloud environment.

## Control Mapping Methodology

Each PCI DSS requirement is evaluated using the following structure:

- **PCI DSS Requirement:** The applicable PCI DSS security requirement.
- **Control Objective:** The security or compliance outcome NovaPay must achieve.
- **AWS Service or Control:** The AWS service or security capability supporting the requirement.
- **NovaPay Implementation:** How NovaPay plans to implement the control.
- **Compliance Evidence:** Documentation, configurations, logs, or screenshots retained to demonstrate control operation.

## PCI DSS Requirement 1 — Install and Maintain Network Security Controls

### Control Objective

NovaPay must implement network security controls to protect the Cardholder Data Environment (CDE) and restrict unauthorized network traffic.

### AWS Services and Controls

- Amazon VPC
- Security Groups
- Network Access Control Lists (NACLs)
- Public and private subnets
- VPC Flow Logs

### NovaPay Implementation

NovaPay will deploy the payment-processing environment within a dedicated Amazon VPC.

The network architecture will separate internet-facing resources from systems operating within the Cardholder Data Environment.

Public subnets will contain approved internet-facing resources, while payment-processing systems will operate within private subnets.

Security Groups will restrict inbound and outbound traffic based on business requirements and the principle of least privilege.

Network ACLs will provide an additional subnet-level network security control.

VPC Flow Logs will capture network traffic metadata to support monitoring, investigations, and compliance reviews.

### Compliance Evidence

NovaPay will retain the following evidence:

- AWS VPC architecture diagram.
- VPC configuration screenshots.
- Public and private subnet configurations.
- Security Group rules.
- Network ACL configurations.
- VPC Flow Log configuration.
- Terraform network configuration files.
- Network security review documentation.

### Control Status

**Status:** Planned

**Control Owner:** Cloud Security / Compliance

**Review Frequency:** At least every six months and following significant network changes.
---

## PCI DSS Requirement 2 — Apply Secure Configurations to All System Components

### Control Objective

NovaPay must establish and maintain secure configuration standards for all AWS resources and system components within the Cardholder Data Environment (CDE).

Default configurations, unnecessary services, excessive permissions, and insecure settings must be identified and remediated.

### AWS Services and Controls

- AWS Config
- AWS Systems Manager
- AWS IAM
- AWS Security Hub
- Amazon EC2
- Amazon S3
- AWS Organizations Service Control Policies (SCPs)
- Infrastructure as Code (Terraform)

### NovaPay Implementation

NovaPay will establish documented secure configuration standards for AWS resources supporting the Cardholder Data Environment.

AWS Config will monitor resource configurations and identify deviations from approved security requirements.

AWS Security Hub will be used to evaluate the AWS environment against applicable security best practices and identify configuration weaknesses.

IAM policies and roles will be reviewed to reduce excessive permissions and enforce least-privilege access.

Amazon EC2 instances will use approved configurations and unnecessary services, ports, and software will be restricted.

Amazon S3 Block Public Access will be enabled for compliance evidence and logging buckets unless a documented business requirement and security review authorizes an exception.

Terraform will be used to define standardized infrastructure configurations and reduce manual configuration inconsistencies.

Configuration exceptions must be documented, reviewed, approved, and retained as compliance evidence.

### Compliance Evidence

NovaPay will retain the following evidence:

- Secure configuration standards.
- AWS Config rule configurations.
- AWS Config compliance reports.
- AWS Security Hub findings.
- IAM policy review documentation.
- EC2 configuration documentation.
- S3 Block Public Access configuration screenshots.
- Terraform configuration files.
- Configuration exception records.
- Remediation tracking documentation.

### Control Status

**Status:** Planned

**Control Owner:** Cloud Security / Compliance

**Review Frequency:** At least every six months and following significant system or configuration changes.

---

# PCI DSS Requirement 3 — Protect Stored Account Data

## Control Objective

NovaPay must protect stored account data by minimizing data retention, implementing strong encryption, securing cryptographic keys, restricting unauthorized access, and securely disposing of cardholder data when no longer required.

Failure to properly protect stored account data may result in unauthorized disclosure of Primary Account Numbers (PANs), regulatory penalties, financial fraud, reputational damage, and non-compliance with PCI DSS v4.0.1.

---

## AWS Services and Controls

NovaPay uses the following AWS services to protect stored cardholder data:

- AWS Key Management Service (AWS KMS)
- Amazon RDS
- Amazon S3
- Amazon Elastic Block Store (Amazon EBS)
- AWS Backup
- AWS Secrets Manager
- AWS Identity and Access Management (IAM)
- AWS CloudTrail
- Amazon CloudWatch

---

## NovaPay Implementation

NovaPay protects stored cardholder data throughout the Cardholder Data Environment (CDE) using layered encryption controls, centralized cryptographic key management, least-privilege access, continuous monitoring, and documented governance procedures.

Only the minimum amount of cardholder data necessary for legitimate business operations is retained.

Sensitive Authentication Data (SAD), including full magnetic stripe data, Card Verification Values (CVV/CVC), PINs, and PIN blocks, is never retained following authorization.

Stored Primary Account Numbers (PANs) remain encrypted using AWS Key Management Service (AWS KMS) Customer Managed Keys.

Access to encrypted data and cryptographic keys follows the Principle of Least Privilege using AWS Identity and Access Management (IAM).

AWS CloudTrail continuously records cryptographic key operations while Amazon CloudWatch monitors security events supporting ongoing compliance.

---

## Encryption Strategy

NovaPay implements a defense-in-depth encryption strategy to protect stored cardholder data throughout its lifecycle.

### Encryption at Rest

All stored cardholder data is encrypted using Advanced Encryption Standard (AES-256).

| AWS Service | Encryption Method |
|--------------|-------------------|
| Amazon RDS | AWS KMS Customer Managed Keys |
| Amazon S3 | Server-Side Encryption using AWS KMS (SSE-KMS) |
| Amazon EBS | AWS KMS Encryption |
| AWS Backup | AWS KMS Encryption |
| AWS Secrets Manager | AWS KMS Encryption |

Encryption is enabled by default for all newly deployed storage resources supporting the Cardholder Data Environment.

### Encryption in Transit

Cardholder data transmitted between users, applications, databases, and AWS services is protected using Transport Layer Security (TLS) version 1.2 or higher.

NovaPay prohibits the use of deprecated or insecure encryption protocols.

---

## AWS Key Management Strategy

NovaPay centrally manages cryptographic keys using AWS Key Management Service (AWS KMS) Customer Managed Keys.

Customer Managed Keys are selected instead of AWS-managed keys because they provide:

- Greater administrative control
- Detailed audit logging
- Fine-grained IAM permissions
- Automatic key rotation
- Stronger alignment with PCI DSS v4.0.1 requirements

### Key Management Objectives

NovaPay's AWS KMS implementation is designed to:

- Protect cryptographic keys throughout their lifecycle.
- Enforce least-privilege access through AWS IAM.
- Record all key usage using AWS CloudTrail.
- Support automatic annual key rotation where supported.
- Prevent unauthorized disclosure, modification, or deletion of cryptographic keys.
- Maintain centralized management of encryption keys protecting the Cardholder Data Environment.

### AWS Resources Protected by AWS KMS

| AWS Resource | Encryption Method |
|---------------|-------------------|
| Amazon RDS | Customer Managed Key |
| Amazon S3 | SSE-KMS |
| Amazon EBS | Customer Managed Key |
| AWS Backup | Customer Managed Key |
| AWS Secrets Manager | Customer Managed Key |

### Key Rotation

Automatic annual key rotation is enabled whenever supported.

Key rotation reduces long-term cryptographic risk while maintaining continuous protection of encrypted cardholder data.

### Key Access Controls

Access to encryption keys is restricted using AWS Identity and Access Management (IAM) policies implementing the Principle of Least Privilege.

Only authorized security administrators may:

- Create encryption keys
- Rotate encryption keys
- Disable encryption keys
- Schedule key deletion
- Modify key policies

Application workloads receive only the minimum permissions required to encrypt and decrypt data during normal business operations.

