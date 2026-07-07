# NovaPay PCI DSS v4.0.1 Control Mapping

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
