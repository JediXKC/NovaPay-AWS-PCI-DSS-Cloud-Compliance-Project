# NovaPay PCI DSS Cloud Compliance Project Scope

## Purpose

The purpose of this project is to design and document a secure AWS cloud environment for NovaPay, a fictional FinTech payment-processing company, aligned with PCI DSS v4.0 requirements.

## Business Context

NovaPay processes online payment transactions and operates systems that interact with cardholder data. The organization must protect sensitive payment information, restrict unauthorized access, monitor security events, and maintain audit-ready compliance evidence.

## Project Scope

The project focuses on the design and documentation of a PCI DSS-aligned AWS Cardholder Data Environment (CDE).

### In-Scope Components

- AWS cloud infrastructure supporting payment-processing systems.
- Amazon VPC network architecture.
- Public and private subnet segmentation.
- IAM users, roles, and least-privilege access controls.
- EC2-based payment application infrastructure.
- S3 logging and compliance evidence storage.
- KMS encryption and key management.
- CloudTrail audit logging.
- AWS Config compliance monitoring.
- GuardDuty threat detection.
- Security Hub security posture management.
- CloudWatch monitoring and alerting.
- Incident response procedures.
- PCI DSS v4.0 control mapping.

## Out-of-Scope Components

- Real cardholder data.
- Production payment transactions.
- Physical payment terminals.
- Third-party payment processors.
- Real customer information.
- Production banking systems.

## Security and Compliance Objectives

- Protect cardholder data from unauthorized access.
- Implement network segmentation around the CDE.
- Apply least-privilege access controls.
- Encrypt sensitive data at rest and in transit.
- Maintain centralized audit logging.
- Monitor security events and configuration changes.
- Document incident response procedures.
- Maintain compliance evidence for PCI DSS assessments.

## Project Deliverables

- AWS cloud architecture diagram.
- PCI DSS v4.0 control mapping.
- IAM access control policy.
- Logging and monitoring plan.
- Encryption and key management documentation.
- Incident response plan.
- Terraform infrastructure code.
- Security configuration evidence and screenshots.
- Final project summary and lessons learned.

## Current Deployment Status

AWS infrastructure deployment is temporarily paused while AWS account billing and access issues are resolved. Planning, compliance documentation, architecture design, and Terraform development will continue locally and through GitHub.
