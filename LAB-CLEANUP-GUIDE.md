# Cloud Lab Cleanup Guide

Use this checklist at the end of **every lab** in this repository.

## Before starting

- [ ] Confirm you are working in the dedicated lab account, tenant, or project—not your primary personal or production environment.
- [ ] Confirm you are authorized to create and remove the resources involved.
- [ ] Review pricing and configure budget or billing alerts where available.
- [ ] Record the names, regions, resource groups, projects, and identifiers of resources you create. Do not record credentials or secrets.

## Remote administration requirement

- [ ] Before every remote connection to a lab VM or cloud environment, connect to an approved, trusted VPN and confirm that the VPN tunnel is active.
- [ ] Keep the VPN connected for the full remote administration session. If it disconnects, end the remote session and restore the VPN before reconnecting.
- [ ] Restrict SSH and management access to the VPN's known egress address or private network range where practical. A VPN does not replace SSH keys, host-key verification, least privilege, or firewall restrictions.
- [ ] Disconnect the remote session before disconnecting the VPN. If no approved VPN is available, do not connect remotely.

## After completing the lab

- [ ] Save sanitized notes and screenshots needed for the learning record.
- [ ] Delete temporary compute resources, including virtual machines, instances, containers, and serverless resources created only for the lab.
- [ ] Delete associated storage, disks, snapshots, images, test databases, backups, and temporary files when they are no longer required.
- [ ] Remove temporary networking resources, such as public IP addresses, load balancers, gateways, firewall rules, and test networks, after checking dependencies.
- [ ] Remove lab-only users, groups, role assignments, policies, service principals, and service accounts when no longer needed.
- [ ] Revoke or delete lab-generated API keys, access keys, tokens, certificates, and other credentials.
- [ ] Check resource inventories and billing/cost dashboards for anything left behind.
- [ ] Review audit/activity logs for failed deletions or unexpected resources.
- [ ] Add a cleanup summary to the lab notes.

## Credential handling

- Never commit secrets to GitHub or include them in screenshots, terminal output, or documentation.
- Prefer managed identities, workload identities, and short-lived credentials over long-lived keys when the platform supports them.
- Store any required secrets in an approved secrets manager; do not put them in source code.
- If a key or token is exposed, revoke it promptly and investigate its use. Rotating a key does not make an exposed old key safe; ensure the old credential is disabled or deleted.

## Account creation and access review

- [ ] Create a separate, uniquely named account for each person; never share usernames.
- [ ] Grant only the minimum permissions required for the person's assigned lab task. Begin with no extra permissions and avoid broad administrator roles.
- [ ] Set a unique password for each account: at least **12 characters** and at least **one special character**, or a stronger provider/organization requirement.
- [ ] Enable MFA where supported, especially for privileged identities.
- [ ] Verify effective permissions and remove temporary role assignments and accounts after the lab.
- [ ] Store credentials in an approved password manager; never commit them to GitHub or lab notes.

## Provider reminders

### AWS

Review the lab's AWS region and account before deleting resources. Check EC2 instances and attached EBS volumes, snapshots, Elastic IP addresses, load balancers, S3 buckets and objects, RDS databases, IAM users/roles/policies, and CloudFormation stacks as applicable. Empty a lab-created S3 bucket before deleting it. Check dependencies and retention settings first.

Official references:
- [Delete or close an AWS resource](https://docs.aws.amazon.com/)
- [AWS Billing and Cost Management](https://docs.aws.amazon.com/cost-management/)

### Microsoft Azure

Check the correct tenant and subscription. Review the lab's resource group and its contents, including virtual machines, managed disks, public IP addresses, network interfaces, virtual networks, storage accounts, databases, and role assignments. A resource group can be a convenient cleanup boundary only when all resources in it belong exclusively to that lab.

Official references:
- [Azure resource management](https://learn.microsoft.com/azure/azure-resource-manager/management/)
- [Azure cost management](https://learn.microsoft.com/azure/cost-management-billing/costs/)

### Google Cloud

Check the correct organization, project, and region. Review Compute Engine instances and disks, static IP addresses, Cloud Storage buckets and objects, databases, networks, firewall rules, service accounts, IAM bindings, and other resources created for the lab. Deleting a project can affect every resource in it, so only do so when the project is dedicated to that lab and you are explicitly authorized.

Official references:
- [Google Cloud resource management](https://cloud.google.com/resource-manager/docs)
- [Google Cloud billing](https://cloud.google.com/billing/docs)

## Safety rules

- Delete only resources created for the lab and confirmed to be safe to remove.
- Do not delete shared infrastructure, production resources, another person's resources, or the cloud account/tenant/organization itself.
- Do not remove organization-wide identities, policies, logs, backups, or security controls unless the lab specifically calls for it and you have authorization.
- Some deletions are irreversible or may have retention and recovery implications. Check dependencies and provider documentation before confirming.
- If you cannot confidently identify a resource, stop and ask the account owner or administrator before deleting it.

## Lab sign-off

Add a short note to the lab report:

> **Cleanup:** Completed / Not completed  
> **Resources removed:** List the lab-created resources deleted.  
> **Credentials revoked:** List credential types only—never include secret values.  
> **Verification:** State which resource inventory and billing pages or logs you checked.  
> **Outstanding items:** List anything remaining and why it was not removed.
