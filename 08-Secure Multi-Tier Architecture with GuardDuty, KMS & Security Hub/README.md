# Secure Multi-Tier Architecture with GuardDuty, KMS & Security Hub

## Overview

This project demonstrates a secure three-tier AWS architecture following the AWS Well-Architected Security Pillar. It implements defense-in-depth by combining encryption, identity management, threat detection, compliance monitoring, and automated incident response.

---

## Architecture

You will find the diagram attached 

---

## Architecture Components

### Network

- Amazon VPC
- Public Subnet
- Private Web Subnet
- Private App Subnet
- Private Database Subnet
- Application Load Balancer
- Security Groups
- Network ACLs

### Compute

- EC2 Auto Scaling Group (Web Tier)
- EC2 Auto Scaling Group (Application Tier)

### Database

- Amazon RDS (Multi-AZ)
- KMS Encryption

---

## Security Services

### AWS KMS

- Customer Managed Keys (CMKs)
- Encrypts RDS
- Encrypts EBS
- Encrypts S3
- Encrypts Secrets Manager

### AWS Secrets Manager

- Stores database credentials
- Automatic secret rotation
- Secure application access

### IAM

- Least privilege access
- IAM Roles
- Permission Boundaries
- MFA
- Service Control Policies (SCPs)

### AWS CloudTrail

- Records API activity
- Multi-region logging
- Log integrity validation

### AWS Config

- Detects non-compliant resources
- Config Rules
- Automatic remediation using SSM

### Amazon GuardDuty

- Threat detection
- Crypto mining detection
- Reconnaissance detection
- Unauthorized API activity

### AWS Security Hub

- Centralized security dashboard
- Aggregates GuardDuty findings
- CIS Benchmark compliance
- PCI DSS compliance

### AWS WAF

- SQL Injection protection
- Cross-site scripting (XSS) protection
- Rate limiting

### AWS Shield Standard

- DDoS protection

---

## Automation

### EventBridge

Detects security events and invokes Lambda.

### Lambda

Automated incident response:

- Send SNS notification
- Tag affected resource
- Isolate EC2 instance
- Stop compromised instance (optional)

---

## Encryption

### At Rest

- Amazon RDS
- Amazon EBS
- Amazon S3
- AWS Secrets Manager

### In Transit

- HTTPS
- TLS
- ACM Certificates

---

## Monitoring

- CloudTrail
- GuardDuty
- Security Hub
- AWS Config
- CloudWatch Logs

---


## AWS Services Used

- Amazon VPC
- EC2
- Auto Scaling
- Application Load Balancer
- Amazon RDS
- AWS KMS
- AWS Secrets Manager
- IAM
- AWS Config
- AWS CloudTrail
- Amazon GuardDuty
- AWS Security Hub
- Amazon EventBridge
- AWS Lambda
- Amazon SNS
- AWS WAF
- AWS Shield Standard
