


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
