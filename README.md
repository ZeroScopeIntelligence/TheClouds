# ZeroScope Solutions Cloud Labs

A hands-on cloud learning repository covering **Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP)**. This repository brings all three major cloud platforms together in one place, with practical labs, notes, configurations, and project documentation.

The goal is to build a strong understanding of cloud computing, infrastructure, networking, identity and access management, security, monitoring, and automation across different cloud environments.

---

## What Is Cloud Computing?

Cloud computing is the delivery of computing resources and technology services over the internet. Instead of purchasing and maintaining all the physical hardware yourself, you can use resources provided by a cloud provider, such as servers, storage, databases, networking, and software, when you need them.

Cloud services can be provisioned, configured, scaled, and managed through web consoles, command-line tools, APIs, and automation. Depending on the service and configuration, customers may pay for the resources they consume.

### Core Cloud Service Models

| Model | What It Provides | Example |
| --- | --- | --- |
| Infrastructure as a Service (IaaS) | Virtualized computing resources such as virtual machines, storage, and networks. | Cloud virtual machines |
| Platform as a Service (PaaS) | A managed platform for building, deploying, and running applications. | Managed application platforms |
| Software as a Service (SaaS) | Ready-to-use software delivered over the internet. | Web-based email and collaboration tools |

### Cloud Deployment Models

- **Public Cloud:** Services are provided over the internet by a cloud provider and shared across customers through logically separated environments.
- **Private Cloud:** Cloud infrastructure is dedicated to one organization.
- **Hybrid Cloud:** Combines private infrastructure with public cloud services.
- **Multi-Cloud:** Uses services from multiple cloud providers, such as AWS, Azure, and Google Cloud.

### Why Learn Cloud Computing?

Cloud computing is widely used to host applications, store and process data, connect systems, support business operations, and deliver technology services. Understanding cloud platforms helps develop practical skills in:

- Designing and managing cloud infrastructure.
- Building virtual networks and connecting systems.
- Managing identities, permissions, and access.
- Securing workloads, applications, and data.
- Monitoring systems, investigating events, and maintaining availability.
- Automating deployments and managing infrastructure consistently.
- Understanding cost, scalability, reliability, and shared security responsibilities.

### Shared Responsibility

Cloud security is a shared responsibility between the cloud provider and the customer. The provider is responsible for security of the cloud, while customers are responsible for securing the resources and configurations they manage. The exact division depends on the provider and service model. These labs will include security considerations as part of each exercise.

---

## Important: Use a Separate Cloud Lab Account

**Do not use your primary personal or everyday cloud account for these exercises.** Create a separate, dedicated cloud account or isolated lab environment for learning. This keeps experiments, permissions, test users, API credentials, and billable resources away from your personal or production environment.

- Use a dedicated lab account, tenant, or project as supported by the provider. Keep it separate from your primary account and any real business or production environment.
- Follow the provider's age, identity-verification, billing, and account-creation requirements. Get the account owner's or parent/guardian's permission where required; never bypass provider requirements.
- Set up billing alerts or budgets before creating resources. Alerts are not always hard spending limits, so continue checking actual usage.
- Use fictional identities and test data only. Do not upload personal, confidential, or real customer information.
- Use least-privilege access. Do not use your everyday administrator identity for routine lab work.
- Never publish passwords, access keys, API keys, tokens, private keys, or connection strings in GitHub, screenshots, or notes.

**Treat the lab account as disposable, but protect the credentials used to access it.** For account isolation and provider-specific setup, follow the official documentation linked below.

---

## Cloud Platforms

This repository uses separate branches to organize hands-on learning for each platform.

### Amazon Web Services (AWS)

Learn and practice cloud services and infrastructure using AWS.

- Compute: EC2
- Storage: S3
- Networking: VPC, subnets, route tables, security groups
- Identity and Access Management: IAM
- Monitoring and auditing: CloudWatch, CloudTrail
- Security: security groups, network ACLs, and security best practices

**Branch:** [aws](https://github.com/ZeroScopeIntelligence/TheClouds/tree/aws)

### Microsoft Azure

Explore Microsoft's cloud platform and its infrastructure and security services.

- Compute: Azure Virtual Machines
- Storage: Azure Storage
- Networking: Virtual Networks, subnets, Network Security Groups
- Identity and Access Management: Microsoft Entra ID and Azure RBAC
- Monitoring: Azure Monitor
- Security: Microsoft Defender for Cloud

**Branch:** [azure](https://github.com/ZeroScopeIntelligence/TheClouds/tree/azure)

### Google Cloud Platform (GCP)

Build practical experience with Google Cloud services and cloud infrastructure.

- Compute: Compute Engine
- Storage: Cloud Storage
- Networking: VPC networks, subnets, firewall rules
- Identity and Access Management: Cloud IAM
- Monitoring and logging: Cloud Monitoring and Cloud Logging
- Security: Security Command Center and cloud security controls

**Branch:** [google-cloud](https://github.com/ZeroScopeIntelligence/TheClouds/tree/google-cloud)

---

## Learning Areas

Labs and projects will be organized around these core topics:

| Area | Focus |
| --- | --- |
| Cloud Fundamentals | Cloud concepts, service models, deployment models, regions, zones, and shared responsibility |
| Compute | Virtual machines, instances, and workloads |
| Storage | Object, block, and file storage |
| Networking | VPCs, virtual networks, subnets, routing, and firewalls |
| Identity and Access Management | Users, roles, policies, and permissions |
| Cloud Security | Secure configurations, access controls, and threat protection |
| Monitoring and Logging | Metrics, logs, alerts, and auditing |
| Automation | Infrastructure as Code, scripting, and repeatable deployments |
| Projects | Practical multi-service and cross-platform exercises |

---

## Lab Completion and Resource Cleanup

**Every lab must include a cleanup step, and all resources created solely for that lab must be removed when the lab is complete.** This includes resources that can continue generating charges or expose access if left running.

Before finishing a lab:

1. Review the lab instructions and identify every resource created, changed, or assigned during the exercise.
2. Export or save only the notes, screenshots, and sanitized results needed for your learning record. Do not save secrets or sensitive data in the repository.
3. Delete lab-created resources that are no longer needed, such as virtual machines, disks, snapshots, storage buckets or containers, test databases, public IP addresses, load balancers, and temporary network components.
4. Remove temporary IAM users, groups, role assignments, policies, service principals, service accounts, and test credentials created for the lab, where they are no longer needed.
5. Revoke or delete lab-generated API keys, access keys, tokens, and other credentials. If a credential may have been exposed, revoke it and create a replacement only when needed.
6. Check the provider's resource inventory, billing/cost dashboard, and activity or audit logs to confirm cleanup. Some services have dependencies or delayed deletion.
7. Record the cleanup result in the lab notes.

**Important:** Delete only resources created for the lab and confirmed to be safe to remove. Do not delete shared infrastructure, resources belonging to someone else, or the cloud account/tenant/project itself unless the lab explicitly requires it and you are authorized to do so. Some resources have retention, backup, or recovery requirements; review those before deletion.

See [LAB-CLEANUP-GUIDE.md](LAB-CLEANUP-GUIDE.md) for the reusable cleanup checklist and provider-specific reminders. Every lab should link to or include its own cleanup instructions.

---

## Repository Structure

Each cloud platform has its own branch, keeping its labs, notes, and projects organized independently.

```text
TheClouds/
├── main
│   ├── README.md
│   └── LAB-CLEANUP-GUIDE.md
├── aws
├── azure
└── google-cloud
```

Each lab should include its objective, prerequisites, setup steps, implementation, validation, cleanup instructions, and lessons learned.

---

## Important Notes

- Follow each cloud provider's documentation and security recommendations.
- Use least-privilege permissions when configuring identities and access.
- Review pricing before deploying resources. Some cloud services can incur charges, even during experimentation.
- Use a separate, dedicated lab account or isolated environment—not your primary account.
- Clean up lab-created resources and credentials after every lab.
- Never commit passwords, API keys, access tokens, private keys, or other secrets to this repository.
- Use these labs only in cloud accounts and environments you are authorized to manage.

## Official Documentation

- [AWS Documentation](https://docs.aws.amazon.com/)
- [AWS account management](https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-creating.html)
- [Microsoft Azure Documentation](https://learn.microsoft.com/azure/)
- [Microsoft Entra tenant guidance](https://learn.microsoft.com/entra/fundamentals/create-new-tenant)
- [Google Cloud Documentation](https://cloud.google.com/docs)
- [Google Cloud resource management](https://cloud.google.com/resource-manager/docs/creating-managing-projects)

---

## About ZeroScope Solutions

ZeroScope Solutions is a technology-focused initiative exploring cybersecurity, cloud infrastructure, networking, and emerging technologies through hands-on projects and research.

**Stay Curious. Stay Sharp. Stay Secure.**
