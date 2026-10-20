# Project 1 — Scalable Web Application with ALB and Auto Scaling

> **Project status:** Architecture and documentation starter. This repository does not claim that AWS resources have been deployed or tested.

## 1. Overview

Deploy a web application that can distribute incoming traffic across multiple application instances, scale as demand changes, and keep its database in a protected network tier.

## 2. Architecture

- Editable diagram: [`architecture/architecture.drawio`](architecture/architecture.drawio)
- Preview: [`architecture/architecture.svg`](architecture/architecture.svg)

The diagram is a conceptual design, not a deployment screenshot. It shows the main request/data flow and supporting operational/security paths. Review the service connections and assumptions before any implementation.

### Architecture rationale

Request path: users → Route 53 → CloudFront/WAF → ALB → EC2 Auto Scaling. The application tier accesses a private Multi-AZ database. Systems Manager and monitoring are supporting operational paths.

## 3. AWS services and their roles

- VPC: public/private subnets, route tables, NAT Gateway, Security Groups, NACLs
- EC2 + Auto Scaling Group: launch template and target-tracking scaling
- Application Load Balancer + AWS WAF: Layer 7 routing, health checks, managed rules
- CloudFront: cache static assets
- Amazon RDS Multi-AZ: MySQL or PostgreSQL with failover
- Route 53: DNS alias to ALB and health checks
- Systems Manager Session Manager: access without a bastion host
- CloudWatch + SNS: dashboards, alarms, notifications

## 4. Proposed implementation plan

1. Confirm requirements, region, constraints, and expected outcome.
2. Draw and review the architecture before creating resources.
3. Estimate costs and identify services that may incur charges.
4. Configure networking and IAM permissions with least privilege.
5. Implement the minimum viable flow using small test data or minimal capacity.
6. Test the success path, failure path, access controls, and monitoring.
7. Capture evidence of actual tests and record any limitations.
8. Delete temporary resources when testing is complete, then verify billing.

## 5. Validation checklist

- [ ] ALB target group reports healthy targets
- [ ] Application is reachable through the ALB DNS name
- [ ] Scaling configuration and health checks are documented
- [ ] Database is not publicly accessible
- [ ] CloudWatch alarm and notification path is documented

## 6. Learning outcomes

- Design subnets, routes, and NAT Gateway configuration
- Explain high availability across Availability Zones
- Configure ALB listeners and target group health checks
- Configure Auto Scaling policies
- Apply security groups, private subnets, and WAF rules
- Use Session Manager for secure instance access

## 7. Cost and safety notes

Potentially expensive: NAT Gateway, ALB, EC2, and Multi-AZ RDS can incur charges. Do not deploy before estimating cost; remove resources after any approved test.

Do not commit access keys, passwords, tokens, private keys, or real customer data to GitHub. Use IAM roles and placeholders in examples.

## 8. Evidence to add after implementation

- [ ] Screenshot or logs from a real successful test (redact account IDs and sensitive information).
- [ ] Test cases and actual results.
- [ ] Any deployment limitations or deviations from the diagram.
- [ ] Cost cleanup confirmation if AWS resources were created.

## 9. Attribution

This project is based on the project idea and service outline in the Manara Tech *AWS Solutions Architect – Associate Graduation Project Ideas* brief. Any external starter material used during implementation should be credited here. Document your own changes and actual tests accurately.
