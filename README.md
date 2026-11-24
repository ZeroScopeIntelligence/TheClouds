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
- Follow the [Identity and Credential Security Standard](#identity-and-credential-security-standard): unique accounts, least privilege, and passwords of at least 12 characters with at least one special character.
- Never publish passwords, access keys, API keys, tokens, private keys, or connection strings in GitHub, screenshots, or notes.

**Treat the lab account as disposable, but protect the credentials used to access it.** For account isolation and provider-specific setup, follow the official documentation linked below.

## Identity and Credential Security Standard

Apply this baseline whenever creating a human user account:

- **Unique identity:** Give every person an individual account and a unique username within the organization or identity directory. Check for existing names and follow a consistent naming convention; never share accounts or reuse another person's identity.
- **Least privilege by default:** Start with no permissions beyond what is required to sign in. Grant only the minimum role and resource scope needed for the person's current duties. Prefer group-based assignments, narrow resource scopes, and read-only access when sufficient. Do not grant Administrator, Owner, or equivalent broad roles by default.
- **Password baseline:** Require a password of at least **12 characters** with at least **one special character**. Each account must have its own unique password; never reuse passwords between users, accounts, or services. Use a randomly generated password or a long, memorable passphrase that meets the provider's rules.
- **MFA:** Enable multi-factor authentication wherever supported, and require it for privileged accounts.
- **Credential handling:** Deliver initial credentials securely, require a change at first sign-in when the platform supports it, and store credentials only in an approved password manager. Never write passwords, recovery codes, API keys, or tokens in GitHub, lab notes, screenshots, or source code.
- **Provider enforcement:** Treat the 12-character / one-special-character rule as this repository's minimum lab standard. Configure the provider or identity platform to enforce it where supported, and always meet any stronger organization or provider requirement. Do not weaken a provider policy to fit the lab.
- **Non-human identities:** Do not use a human password for workloads. Prefer managed/workload identities and short-lived credentials; scope service accounts and API credentials to the specific task.

After account creation, verify the user's effective permissions and test that actions outside the assigned duties are denied. Remove temporary access when it is no longer needed.

## Remote Access: Always Use a VPN

**Always connect to an approved, trusted VPN before remotely accessing cloud lab systems or administering a VM over SSH.** Connect to the VPN first, confirm the secure tunnel is active, and only then start the remote session. If the VPN is unavailable, do not make the remote connection; use an approved private-access method or wait until secure access is restored.

A VPN is an additional protection layer—not a replacement for SSH key authentication, host-key verification, least-privilege access, or restrictive firewall rules. Keep SSH ingress limited to the VPN's known egress address or private network range where practical; never open port 22 to the entire internet. Avoid untrusted public Wi-Fi for administrative sessions.


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

### Desktop Virtualization

The [Virtual Machines guide](VirtualMachines/README.md) introduces local desktop hypervisors that can be used to prepare and test lab systems before connecting them to cloud environments. It covers Broadcom VMware Workstation Pro and Oracle VirtualBox, with setup considerations, virtual networking, snapshots, and safe lab practices.


Labs and projects will be organized around these core topics:

| Area | Focus |
| --- | --- |
| Cloud Fundamentals | Cloud concepts, service models, deployment models, regions, zones, and shared responsibility |
| Compute | Cloud virtual machines, instances, and workloads | 
| Desktop Virtualization | Local VM platforms using VMware Workstation Pro or Oracle VirtualBox |
| Storage | Object, block, and file storage |
| Networking | VPCs, virtual networks, subnets, routing, and firewalls |
| Secure Remote Access (SSH) | SSH keys, Linux VM access, network restrictions, troubleshooting, and cleanup |
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
│   ├── LAB-CLEANUP-GUIDE.md
│   └── VirtualMachines/
│       └── README.md
├── aws
├── azure
└── google-cloud
```

Each lab should include its objective, prerequisites, setup steps, implementation, validation, cleanup instructions, and lessons learned. The AWS, Azure, and Google Cloud branches each include a dedicated SSH learning path for securely accessing Linux virtual machines.

---

## Important Notes

- Follow each cloud provider's documentation and security recommendations.
- Use least-privilege permissions when configuring identities and access.
- Review pricing before deploying resources. Some cloud services can incur charges, even during experimentation.
- Use a separate, dedicated lab account or isolated environment—not your primary account.
- Clean up lab-created resources and credentials after every lab.
- Never commit passwords, API keys, access tokens, private keys, or other secrets to this repository.
- Use these labs only in cloud accounts and environments you are authorized to manage.

## About ZeroScope Solutions

ZeroScope Solutions is a technology-focused initiative exploring cybersecurity, cloud infrastructure, networking, and emerging technologies through hands-on projects and research.

**Stay Curious. Stay Sharp. Stay Secure.**
