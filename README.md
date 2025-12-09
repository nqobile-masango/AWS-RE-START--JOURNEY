# nqobile-masango — AWS re:START Journey
Welcome — this repository documents my learning journey through the AWS re:Start programme. It contains notes, labs, projects, and a weekly journal showing how I progressed from cloud fundamentals to hands-on AWS services and Linux essentials.

---

## About me
- I’m a cloud-curious learner participating in the AWS re:Start programme. I’m focusing on foundational AWS services, Linux basics, infrastructure as code, and small hands-on projects that demonstrate real-world cloud skills.

- Role I’m targeting: Cloud Engineer / Junior DevOps / Cloud Support

---

## Quick summary

- Learning programme: AWS re:Start
- Focus areas: AWS Core Services, Linux, Networking fundamentals, Databases, Serverless
- Current status: (e.g., In progress — Week X) — update as you progress

---

## Skills & Technologies
- Cloud & AWS: EC2, S3, IAM, VPC, Lambda, RDS, DynamoDB, CloudFormation
- DevOps basics: Infrastructure as Code (CloudFormation), CI/CD concepts
- OS & CLI: Linux command line, shell scripting, file & process management
- Databases: RDS (MySQL/Postgres), DynamoDB
- Tools: AWS Management Console, AWS CLI, Git, VS Code

---

## Highlights & Projects
Each project folder contains README notes, steps I followed, and screenshots where applicable.

- Lab: EC2 launch & SSH configuration — steps to provision, secure, and connect to an instance
- Lab: S3 static website — hosting a demo static site with public/secure buckets
- Project: Simple serverless function — Lambda function (Node.js/Python) triggered by S3 or API Gateway
- Project: RDS setup — provisioning an RDS instance and connecting from an EC2 bastion host
- Infrastructure: CloudFormation templates used to provision small stacks

(See the /labs and /projects folders for details.)

---

## Weekly Journal 
This section captures weekly learning goals, labs, and topics covered across the programme. I update this regularly as I complete labs and projects.

### Week 1 — Cloud fundamentals & orientation
- Topics: Cloud concepts, service models (IaaS, PaaS, SaaS), public/private/hybrid clouds, benefits of cloud.
- Labs: AWS console tour, setting up an AWS sandbox account, billing basics and cost-awareness.
- Deliverables: Account setup, list of free-tier limits, simple architecture diagram.

### Week 2 — AWS core services (compute & storage)
- Topics: EC2 instance types, EBS volumes, S3 storage classes, S3 security and lifecycle policies.
- Labs: Launch EC2, attach EBS, create and configure S3 buckets, set bucket policies and object ACLs.
- Deliverables: Bootstrapped EC2 instance with SSH access and a public S3 bucket used for a demo asset.

### Week 3 — Identity, Access & Security basics
- Topics: IAM users, groups, roles, policies, least-privilege principle, MFA, security best practices.
- Labs: Create IAM users and groups, attach policies, create a role for EC2, test temporary credentials.
- Deliverables: Minimal-privilege IAM policy examples and a secure user setup.

### Week 4 — Networking fundamentals & VPCs
- Topics: VPC, subnets, route tables, internet gateway, NAT gateway, security groups, NACLs.
- Labs: Build a custom VPC with public and private subnets, configure routing and security groups.
- Deliverables: Diagram of VPC architecture and a working bastion host to access private instances.

### Week 5 — Linux essentials & automation
- Topics: Linux CLI, file system, users and permissions, process management, shell scripting basics.
- Labs: SSH into EC2, manage files, write basic bash scripts to automate tasks.
- Deliverables: Collection of small scripts (backups, log rotation, monitoring checks).

### Week 6 — Databases & storage services
- Topics: RDS (MySQL/Postgres), DynamoDB basics, backups, snapshots, connection best practices.
- Labs: Provision RDS instance, connect from EC2, create a basic DynamoDB table and run CRUD operations.
- Deliverables: Working RDS-backed demo app and a DynamoDB table with example code.

### Week 7 — Serverless & event-driven architectures
- Topics: AWS Lambda, API Gateway, S3 triggers, IAM roles for Lambda, cold starts and best practices.
- Labs: Create a Lambda function triggered by S3 or API Gateway, test end-to-end flow.
- Deliverables: Serverless function with README and test events.

### Week 8 — Infrastructure as Code (IaC)
- Topics: CloudFormation fundamentals, templates, stacks, parameterization, basic drift detection.
- Labs: Write CloudFormation templates to provision an EC2 + security group + S3 bucket stack.
- Deliverables: Reusable CloudFormation template with documented parameters.

### Week 9 — Monitoring, logging & observability
- Topics: CloudWatch metrics/logs/alarms, CloudTrail auditing, AWS X-Ray basics.
- Labs: Configure CloudWatch alarms, send logs from EC2 to CloudWatch, enable CloudTrail.
- Deliverables: Alerting playbook and a dashboard snapshot.

### Week 10 — CI/CD, automation & deployment patterns
- Topics: CI/CD concepts, CodeCommit/CodeBuild/CodeDeploy basics (or GitHub Actions), deployment strategies (blue/green, rolling).
- Labs: Simple CI pipeline for deploying a static site to S3 or deploying a Lambda via CI.
- Deliverables: Example pipeline config and deployment notes.

### Week 11 — Containers & orchestration basics
- Topics: Docker fundamentals, ECS vs EKS overview, container registries (ECR), container security basics.
- Labs: Containerize a small app locally, push to ECR, run on ECS Fargate (demo).
- Deliverables: Dockerfile and deployment notes for running a containerized app.

### Week 12 — Security, compliance & cost optimization
- Topics: Encryption (at-rest/in-transit), KMS basics, backups, IAM best practices, cost optimization strategies and tagging.
- Labs: Enable encryption for S3/RDS, create KMS key, run cost estimation and tagging audit.
- Deliverables: Security checklist and cost-reduction suggestions.

### Week 13 — Advanced topics & integrations
- Topics: API Gateway + Lambda integrations, SDK usage, application-level security, caching (ElastiCache), messaging (SNS, SQS).
- Labs: Build a small API with API Gateway -> Lambda -> DynamoDB; add SNS/SQS for decoupling.
- Deliverables: End-to-end API demo and integration notes.

### Week 14 — Troubleshooting & operational excellence
- Topics: Debugging common issues, log analysis, root cause analysis, backup & recovery, runbooks.
- Labs: Simulate failures and document recovery steps; create a runbook.
- Deliverables: Runbook examples and incident postmortem template.

### Week 15 — Final projects & portfolio polish
- Topics: End-to-end architecture design, documentation, README polish, resume & LinkedIn alignment.
- Labs: Finalize 1-2 showcase projects (infrastructure + app), produce walkthrough video or README.
- Deliverables: Portfolio-ready projects with clear instructions to reproduce.

(Adjust week numbers and topics as the programme progresses — this journal is a living document.)

---

## How to use this repo
- Browse /labs for step-by-step exercises and outputs.
- Browse /projects for complete projects and documentation.
- Each lab/project has a README with prerequisites, steps, and expected results.

Checklist to reproduce my work:
1. Create an AWS sandbox account or use the one provided by the programme.
2. Install AWS CLI and configure credentials (aws configure).
3. Follow the lab/project README in the respective folder.

---

## Goals & Roadmap
- Short term: Complete remaining labs; create 2 end-to-end projects (infrastructure + application).
- Medium term: Learn Terraform / deeper CloudFormation, practice CI/CD pipelines.
- Long term: Prepare for AWS Certified Cloud Practitioner or AWS Certified Solutions Architect — Associate.

---

## Contact & LinkedIn
I’m open to collaboration, mentorship, and entry-level roles.

- LinkedIn: your-linkedin-url
- GitHub: https://github.com/nqobiile
- Email: your-email@example.com

---

## Contributing
This repo is primarily a personal learning log. If you have suggestions or improvements (formatting, additional labs, or resources), please open an issue or submit a pull request.

---

## License
This repository is licensed under the MIT License. See LICENSE for details.
