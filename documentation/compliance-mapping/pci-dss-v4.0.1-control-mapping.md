


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

PCI DSS Requirement 3 — Protect Stored Account Data

Control Objective

NovaPay must protect stored account data by minimizing data retention, implementing strong encryption, securing cryptographic keys, restricting unauthorized access, and securely disposing of cardholder data when no longer required.

Failure to properly protect stored account data may result in unauthorized disclosure of Primary Account Numbers (PANs), regulatory penalties, financial fraud, reputational damage, and PCI DSS non-compliance.

AWS Services and Controls

AWS Key Management Service (AWS KMS)

Amazon RDS

Amazon S3

Amazon Elastic Block Store (Amazon EBS)

AWS Backup

AWS Secrets Manager

AWS Identity and Access Management (IAM)

AWS CloudTrail

Amazon CloudWatch

NovaPay Implementation

NovaPay will implement encryption and data protection controls throughout the Cardholder Data Environment (CDE).

Only the minimum amount of cardholder data necessary for business operations will be retained.

Sensitive Authentication Data (SAD), including full magnetic stripe data, Card Verification Values (CVV/CVC), PINs, and PIN blocks, will never be retained following authorization.

Stored Primary Account Numbers (PANs) will remain encrypted using AWS Key Management Service (AWS KMS) Customer Managed Keys.

Access to encrypted data and cryptographic keys will follow the principle of least privilege using AWS Identity and Access Management (IAM).

All cryptographic key usage will be logged through AWS CloudTrail and continuously monitored as part of NovaPay's security monitoring program.

Encryption Strategy

NovaPay implements a defense-in-depth encryption strategy to protect stored cardholder data throughout its lifecycle.

Encryption at Rest

All stored cardholder data is encrypted using Advanced Encryption Standard (AES) with 256-bit encryption (AES-256).

AWS Service

Encryption Method

Amazon RDS

AWS KMS Customer Managed Key

Amazon S3

Server-Side Encryption with AWS KMS (SSE-KMS)

Amazon EBS

AWS KMS Encryption

AWS Backup

AWS KMS Encryption

AWS Secrets Manager

AWS KMS Encryption

Encryption is enabled by default for all newly deployed storage resources within the Cardholder Data Environment (CDE).

Encryption in Transit

Cardholder data transmitted between users, applications, and AWS services is protected using Transport Layer Security (TLS) version 1.2 or higher.

NovaPay prohibits the use of insecure or deprecated encryption protocols for systems within the Cardholder Data Environment.

AWS Key Management Strategy

NovaPay uses AWS Key Management Service (AWS KMS) Customer Managed Keys to centrally manage the cryptographic keys protecting cardholder data throughout the AWS environment.

Customer Managed Keys are selected over AWS-managed keys to provide greater administrative control, detailed auditing, fine-grained access permissions, and stronger alignment with PCI DSS v4.0.1 requirements.

Key Management Objectives

NovaPay's AWS KMS implementation is designed to:

Protect cryptographic keys throughout their lifecycle.

Enforce least-privilege access through AWS Identity and Access Management (IAM).

Record all key usage using AWS CloudTrail.

Support automatic annual key rotation where applicable.

Prevent unauthorized disclosure, modification, or deletion of encryption keys.

Maintain centralized management of encryption keys supporting the Cardholder Data Environment (CDE).

AWS Resources Protected by AWS KMS

AWS Resource

Encryption Method

Amazon RDS

Customer Managed Key

Amazon S3

SSE-KMS

Amazon EBS

Customer Managed Key

AWS Backup

Customer Managed Key

AWS Secrets Manager

Customer Managed Key

Key Rotation

Automatic annual key rotation is enabled for AWS KMS Customer Managed Keys whenever supported.

Key rotation reduces long-term cryptographic risk while maintaining continuous protection of encrypted cardholder data.

Key Access Controls

Access to cryptographic keys is restricted through IAM policies implementing the principle of least privilege.

Only authorized security administrators may:

Create encryption keys

Rotate encryption keys

Disable encryption keys

Schedule key deletion

Modify key policies

Application workloads receive only the minimum permissions necessary to encrypt and decrypt data during normal business operations.

Cryptographic Key Lifecycle

NovaPay manages cryptographic keys throughout their lifecycle in accordance with PCI DSS v4.0.1 requirements and AWS security best practices.

Key Creation

Customer Managed Keys are created within AWS Key Management Service (AWS KMS) and protected by AWS Hardware Security Modules (HSMs).

Key Storage

Cryptographic keys remain securely stored within AWS KMS and are never stored in application code, configuration files, source repositories, or database records.

Key Usage

Encryption keys are used exclusively to encrypt and decrypt approved cardholder data supporting the Cardholder Data Environment (CDE).

Application workloads access encryption keys through AWS Identity and Access Management (IAM) permissions and AWS KMS API operations.

Key Rotation

Automatic annual key rotation is enabled whenever supported.

Manual key rotation procedures are documented for services requiring administrator-managed rotation.

Key Monitoring

AWS CloudTrail records all cryptographic key operations, including:

Encrypt

Decrypt

GenerateDataKey

DisableKey

ScheduleKeyDeletion

PutKeyPolicy

Security administrators review key activity as part of continuous security monitoring.

Key Deletion

Cryptographic keys are scheduled for deletion only after:

Formal management approval

Verification that encrypted data is no longer required

Completion of the AWS KMS mandatory waiting period

NovaPay prohibits exporting cryptographic key material outside AWS KMS.

Separation of Duties

NovaPay implements separation of duties to reduce the risk of unauthorized access to encrypted cardholder data and cryptographic keys.

Role

Primary Responsibility

Security Administrator

AWS KMS administration and key management

Cloud Administrator

AWS infrastructure administration

Database Administrator

Database administration without AWS KMS administrative privileges

Application Administrator

Secure application deployment and encryption integration

Compliance Officer

PCI DSS compliance oversight and evidence review

Internal Auditor

Independent validation of control effectiveness

No single individual maintains unrestricted administrative control over both encrypted cardholder data and the cryptographic keys protecting that data.

Data Retention Policy

NovaPay retains cardholder data only for legitimate business, legal, financial, and regulatory purposes.

Cardholder data may be retained for:

Payment processing

Fraud investigations

Chargeback support

Financial reconciliation

Regulatory compliance

Legal record retention

Data Type

Retention Requirement

Cardholder Data

Business and regulatory requirements

Transaction Records

Financial record retention policy

Audit Logs

Security and compliance policy

CloudTrail Logs

Security monitoring policy

AWS Config History

Configuration management policy

Retention schedules are reviewed at least annually and updated whenever regulatory or business requirements change.

Secure Data Disposal

When cardholder data is no longer required, NovaPay securely disposes of the data in accordance with PCI DSS v4.0.1 requirements.

Secure disposal methods include:

Cryptographic erasure through AWS KMS key destruction when appropriate

Secure deletion of encrypted storage resources

Secure removal of Amazon S3 objects

Secure deletion of Amazon EBS snapshots

Removal of obsolete AWS Backup recovery points

Disposal activities require management approval and are documented as part of NovaPay's security governance program.

Evidence of secure disposal activities is retained for compliance and audit purposes.

Compliance Evidence

Configuration Evidence

AWS KMS key configuration and policies

Amazon RDS encryption settings

Amazon S3 SSE-KMS configuration

Amazon EBS encryption configuration

AWS Backup encryption configuration

Monitoring Evidence

AWS CloudTrail logs for cryptographic key operations

AWS Config compliance evaluations

Security monitoring and alerting records

Governance Evidence

AWS IAM policies controlling access to encryption keys

Data retention and disposal records

Internal compliance review documentation

Control Summary

Item

Value

Control Status

Implemented

Control Owner

Cloud Security Manager / Information Security Team

Review Frequency

At least annually and following significant changes to encryption, key management, storage architecture, or PCI DSS requirements.

Lessons Learned

Strong encryption depends on effective cryptographic key management.

Governance is as important as technical implementation for protecting cardholder data.

Data minimization reduces both organizational risk and compliance obligations.

Separation of duties strengthens accountability and reduces insider threats.

Continuous monitoring and documented evidence are essential for demonstrating PCI DSS compliance.

Interview Talking Points

After completing this requirement, I can explain:

Why AWS KMS Customer Managed Keys were selected

Encryption at rest versus encryption in transit

How cryptographic key rotation reduces risk

How IAM enforces least privilege for encryption keys

How PCI DSS Requirement 3 maps to AWS services

What evidence an auditor would request during a PCI DSS assessment

How data retention and secure disposal support compliance

Risk Statement

Failure to properly protect stored account data may result in unauthorized disclosure of cardholder information, regulatory penalties, financial loss, reputational damage, and non-compliance with PCI DSS requirements.

The controls documented in this requirement mitigate these risks through encryption, centralized cryptographic key management, least-privilege access controls, documented data retention procedures, secure disposal practices, and continuous monitoring.

References

PCI Security Standards Council. Payment Card Industry Data Security Standard (PCI DSS) v4.0.1.

Amazon Web Services. AWS Key Management Service (AWS KMS) Developer Guide.

Amazon Web Services. AWS Identity and Access Management (IAM) User Guide.

Amazon Web Services. AWS CloudTrail User Guide.

Amazon Web Services. AWS Config Developer Guide.

Amazon Web Services. AWS Well-Architected Framework – Security Pillar.

Amazon Web Services. AWS Security Best Practices.
