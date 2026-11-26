# Identity and Access Management (IAM)

Identity and Access Management (IAM) is the set of tools, policies, and processes used to control who or what can access cloud resources and what actions they are allowed to perform.

IAM is a foundational cloud security control. It helps organizations verify identities, grant appropriate permissions, enforce least privilege, and review access over time.

This guide introduces IAM concepts and provides learning paths for **Amazon Web Services (AWS)**, **Microsoft Azure / Microsoft Entra ID**, and **Google Cloud Platform (GCP)**.

---

## Learning Objectives

By completing the IAM learning path, you should be able to:

- Explain the difference between authentication and authorization.
- Identify users, groups, roles, policies, and service identities.
- Apply the principle of least privilege.
- Create users and groups and assign permissions in each cloud platform.
- Configure MFA and password or authentication policies where supported.
- Review effective access and remove permissions that are no longer needed.
- Recognize the security differences between human identities and workload identities.

## IAM Fundamentals

### Authentication vs. Authorization

| Concept | Meaning | Example |
| --- | --- | --- |
| Authentication | Verifies an identity. | Signing in with an account and completing MFA. |
| Authorization | Determines what an authenticated identity can do. | Allowing a user to view a storage bucket but not delete it. |

Authentication answers **"Who are you?"** Authorization answers **"What are you allowed to do?"**

### Core IAM Components

| Component | Purpose |
| --- | --- |
| User | Represents an individual identity, usually a person or workload depending on the platform. |
| Group | Collects users so permissions can be managed consistently. |
| Role | A set of permissions that can be assumed or assigned for a defined purpose. |
| Policy | A set of rules describing allowed or denied actions and, in many systems, the resources or conditions involved. |
| Permission | An authorization to perform a particular action on a resource. |
| Service identity | An identity used by an application, automation, or workload rather than an individual person. |

Terminology and behavior vary by provider. For example, AWS IAM roles are assumed by trusted principals, Azure uses Microsoft Entra identities together with Azure RBAC role assignments, and Google Cloud IAM grants roles to principals on resource hierarchies.

### Principle of Least Privilege

Grant only the minimum permissions required to perform a task, for only as long as those permissions are needed.

Recommended practices:

- Start with no access beyond what is required to sign in.
- Assign access through groups or roles where practical instead of creating one-off permissions for every user.
- Prefer read-only permissions when write access is unnecessary.
- Scope permissions to the smallest appropriate resource, project, subscription, or account.
- Avoid broad administrator or owner roles for routine work.
- Review access regularly and remove temporary or unused permissions.
- Use separate privileged accounts or controlled elevation processes for administrative tasks.

### Identity and Credential Baseline

Use this baseline for the repository's practice environments:

- Create a unique identity for each person. Never share accounts.
- Use a unique password for every account. The repository's minimum lab standard is **at least 12 characters and at least one special character**; meet stronger provider or organization requirements where applicable.
- Enable MFA wherever supported, especially for privileged identities.
- Use an approved password manager and deliver initial credentials securely.
- Never commit passwords, recovery codes, access keys, API keys, tokens, or private keys to GitHub.
- Prefer workload identities and short-lived credentials over long-lived keys for applications and automation.
- Verify effective access after making role or policy changes.
- Remove test identities and credentials during lab cleanup when they are no longer needed.

Password rules are not identical across providers. Where a platform does not expose a particular password control, document the limitation rather than weakening another security control.

---

## Lab 1: AWS IAM

**Platform:** Amazon Web Services

**Portal:** https://console.aws.amazon.com/iam/

### Objectives

- Create an IAM user for a test identity.
- Create a group and assign permissions to it.
- Review AWS managed and customer-managed policies.
- Configure account-level password settings.
- Enable MFA for the test identity.
- Validate that permissions match the user's intended duties.

### Part A: Create an IAM Group

1. Sign in to the AWS Management Console using your dedicated lab environment.
2. Open **IAM**.
3. In the navigation pane, select **User groups**.
4. Select **Create group**.
5. Enter a descriptive group name, such as `CloudLab-ReadOnly`.
6. Under permissions policies, select an appropriate read-only policy for the lab. For a basic exercise, review the AWS managed `ReadOnlyAccess` policy and understand its scope before attaching it.
7. Review the policy and group details, then create the group.

**Security note:** AWS managed policies can grant access across many services. For production-like practice, create a narrowly scoped customer-managed policy for the exact resources and actions required.

### Part B: Create an IAM User

1. In IAM, select **Users**.
2. Select **Create user**.
3. Enter a unique test username, such as `lab.user01`.
4. Configure console access only when the lab requires an interactive sign-in.
5. Use the platform's secure credential creation and delivery options. Do not put generated passwords in notes or screenshots.
6. Add the user to the `CloudLab-ReadOnly` group.
7. Review the permissions summary and create the user.
8. Confirm that the user has only the permissions intended for the exercise.

Avoid creating access keys unless a lab specifically requires programmatic access. Prefer temporary credentials and role-based access for workloads.

### Part C: Review and Configure the Account Password Policy

1. Open **IAM → Account settings**.
2. Locate **Password policy** and choose **Edit**.
3. Select the custom password policy option.
4. Set the minimum password length to **12 characters**.
5. Under password strength, enable the available character-type requirements that are appropriate for the lab, including uppercase letters, lowercase letters, numbers, and symbols.
6. Under additional requirements, review the options for password expiration, user password changes, and password reuse prevention.
7. For this lab's policy exercise, configure a **60-day password expiration** where the account and current AWS policy options support it, allow users to change their own passwords, and prevent password reuse.
8. Save the policy and verify the resulting settings.

**Important:** AWS console options and password-policy behavior can change. Follow the current console labels and AWS documentation. A password expiration setting is a lab policy choice, not a universal recommendation for every environment; follow the applicable security standard and favor MFA and strong, unique credentials.

### Part D: Enable MFA

1. Open **IAM → Users**.
2. Select the test user.
3. Open the **Security credentials** tab.
4. Find the multi-factor authentication (MFA) section.
5. Choose **Assign MFA device**.
6. Follow the console instructions to configure a supported MFA device.
7. Sign in with the test identity and verify that the additional authentication step is required.

Use a supported authenticator or hardware security key. Keep recovery information protected.

### Part E: Validate Permissions

1. Sign in as the test user using the credentials delivered securely.
2. Confirm that the user can perform the intended read-only task.
3. Attempt a harmless action that should be outside the assigned permission set, such as opening a restricted management page or checking whether a write action is denied.
4. Record the result without capturing credentials or sensitive data.
5. Return to the administrator session and review the user's group membership and attached policies.

### AWS Lab Checklist

- [ ] Created a dedicated IAM group.
- [ ] Reviewed the policy attached to the group.
- [ ] Created a unique test user.
- [ ] Added the test user to the group.
- [ ] Reviewed the account password policy.
- [ ] Enabled MFA for the test user.
- [ ] Validated allowed and denied actions.
- [ ] Removed temporary users, credentials, and policies that are no longer needed.

**Official documentation:** [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) · [Manage IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_manage.html) · [AWS account password policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html) · [MFA for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)

---

## Lab 2: Microsoft Azure and Microsoft Entra ID

**Platform:** Microsoft Azure

**Portals:** https://entra.microsoft.com/ · https://portal.azure.com/

Microsoft Entra ID manages identities and authentication. Azure role-based access control (Azure RBAC) controls access to Azure resources. These systems work together, but they serve different purposes.

### Security Groups vs. Microsoft 365 Groups

| Group type | Primary purpose | Typical use |
| --- | --- | --- |
| Security group | Manage access control, permissions, licenses, and device policies. | Grant users access to applications, resources, and administrative scopes. |
| Microsoft 365 group | Provide shared workspaces and collaboration tools across Microsoft 365 apps. | Collaborate using services such as Outlook, SharePoint, and Teams. |

Choose the group type based on the resource and access requirement. A Microsoft 365 group is not a substitute for understanding Azure RBAC assignments.

### Part A: Create a Test User

1. Open the **Microsoft Entra admin center**.
2. Navigate to **Identity → Users → All users**.
3. Select **New user → Create new user**.
4. Enter a unique username and the required profile information for the fictional lab identity.
5. Configure the initial password using the secure process provided by the tenant.
6. Review the properties and create the user.
7. Confirm that the test user appears in the user list.

Use fictional data only. Do not use real personal information in screenshots or repository documentation.

### Part B: Create a Security Group

1. In Microsoft Entra admin center, navigate to **Identity → Groups → All groups**.
2. Select **New group**.
3. Under **Group type**, select **Security**.
4. Enter a descriptive group name, such as `CloudLab-Users`.
5. Choose the membership type appropriate for the exercise.
6. Add the test user as a member.
7. Review the configuration and create the group.

**Note:** A group does not need an access permission merely to exist. Create the group first, then assign only the application or resource permissions required by the lab.

### Part C: Review Microsoft 365 Groups

1. Return to **Identity → Groups → All groups**.
2. Select **New group**.
3. Review the available group types and select **Microsoft 365** for a collaboration-focused exercise.
4. Review the available ownership, membership, and collaboration settings.
5. Create the group only when the lab requires a shared Microsoft 365 workspace.

Compare its purpose and available features with the Security group created in Part B. Avoid creating unnecessary groups in a shared tenant.

### Part D: Configure Microsoft Authenticator

1. Open the Microsoft Entra admin center.
2. Navigate to **Protection → Authentication methods → Policies**. The exact menu wording may vary as the portal changes.
3. Locate **Microsoft Authenticator**.
4. Verify that the method is enabled for the intended users or lab group.
5. Review the configuration and save any required changes.
6. Use a test identity to complete the supported registration process.
7. Confirm that the sign-in policy requires the configured authentication method where applicable.

Enabling an authentication method makes it available according to the policy; it does not by itself guarantee that every sign-in will require MFA. Use an appropriate Conditional Access policy or the tenant's supported security defaults to enforce MFA.

### Part E: Assign an Azure RBAC Role

1. Open the Azure portal.
2. Navigate to a dedicated lab resource group or another approved test scope.
3. Open **Access control (IAM)**.
4. Select **Add → Add role assignment**.
5. Choose a narrowly scoped role appropriate for the exercise, such as **Reader** for a read-only task.
6. Select the appropriate user, group, or workload identity.
7. Review the scope and assignment, then complete the role assignment.
8. Verify access using the test identity.

Do not assign Owner or broad Contributor access merely to make a lab work. Azure RBAC role assignments apply at a scope and can inherit down the resource hierarchy.

### Azure / Entra Lab Checklist

- [ ] Created a fictional test user.
- [ ] Created a Security group.
- [ ] Added the test user to the Security group.
- [ ] Compared Security groups and Microsoft 365 groups.
- [ ] Reviewed the Microsoft Authenticator authentication method policy.
- [ ] Registered a supported authentication method for the test identity.
- [ ] Assigned a least-privilege Azure RBAC role at a test scope.
- [ ] Validated access and removed temporary assignments when finished.

**Official documentation:** [Microsoft Entra ID documentation](https://learn.microsoft.com/en-us/entra/identity/) · [Create users](https://learn.microsoft.com/en-us/entra/fundamentals/how-to-create-delete-users) · [Create groups](https://learn.microsoft.com/en-us/entra/fundamentals/how-to-manage-groups) · [Authentication methods](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-methods) · [Azure RBAC overview](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)

---

## Lab 3: Google Cloud IAM

**Platform:** Google Cloud Platform

**Portal:** https://console.cloud.google.com/

Google Cloud IAM manages access by granting roles to principals at a resource scope. A principal can be a user, group, service account, or another supported identity.

### Part A: Review IAM and the Resource Hierarchy

1. Sign in to the dedicated Google Cloud lab environment.
2. Select the intended lab organization, folder, or project.
3. Open **IAM & Admin → IAM**.
4. Review the existing principals, roles, and resource scope.
5. Identify which permissions are inherited from parent resources.

Google Cloud permissions can be inherited through the resource hierarchy. Check the scope before changing access.

### Part B: Add a Principal

1. Open **IAM & Admin → IAM**.
2. Select **Grant access**.
3. Enter the email address of a fictional or designated test principal.
4. Select a role suitable for the task. For an initial read-only exercise, review the Viewer role and its scope.
5. Review the principal and role assignment.
6. Grant access and verify that the principal appears in the IAM policy.

### Part C: Review Predefined and Custom Roles

1. Open **IAM & Admin → Roles**.
2. Review the predefined roles relevant to the lab.
3. Compare the permissions included in each role.
4. Where the lab requires it and your permissions allow it, create a custom role containing only the required permissions.
5. Assign the role at the narrowest supported scope.
6. Validate the resulting access.

Avoid basic Owner, Editor, and Viewer roles when a narrower predefined or custom role is suitable. Review role permissions before assignment.

### Part D: Review Service Accounts

1. Open **IAM & Admin → Service Accounts**.
2. Review the service accounts available in the test project.
3. Create a dedicated service account only when a lab workload requires one.
4. Grant only the permissions the workload needs.
5. Prefer attached service identities or workload identity federation over downloaded, long-lived service-account keys.
6. Review and remove unnecessary service accounts and credentials during cleanup.

### Google Cloud Lab Checklist

- [ ] Reviewed the project and resource hierarchy.
- [ ] Added a test principal.
- [ ] Granted a least-privilege role.
- [ ] Compared predefined and custom roles.
- [ ] Reviewed service account access.
- [ ] Validated effective permissions.
- [ ] Removed temporary role assignments and credentials that are no longer needed.

**Official documentation:** [Cloud IAM overview](https://cloud.google.com/iam/docs/overview) · [Grant, change, and revoke access](https://cloud.google.com/iam/docs/granting-changing-revoking-access) · [IAM roles](https://cloud.google.com/iam/docs/roles-overview) · [Service accounts](https://cloud.google.com/iam/docs/service-account-overview)

---

## Cross-Cloud IAM Comparison

| Capability | AWS | Microsoft Azure | Google Cloud |
| --- | --- | --- | --- |
| Identity platform | AWS IAM and related identity services | Microsoft Entra ID | Cloud IAM principals and identity services |
| Permission model | Policies attached to identities and resources; roles are assumed by trusted principals | Azure RBAC role assignments at defined scopes | Roles granted to principals on resource hierarchy |
| Group support | IAM user groups | Entra Security and Microsoft 365 groups | Google Groups can be IAM principals |
| Workload identity | IAM roles and temporary credentials | Managed identities and service principals | Service accounts and workload identity federation |
| MFA | Supported for IAM users and federated identities | Microsoft Entra authentication methods and Conditional Access | Google account and Cloud Identity controls |
| Audit | CloudTrail | Entra audit and sign-in logs; Azure activity logs | Cloud Audit Logs |

The products have different capabilities and terminology. Do not assume that similarly named roles or groups grant identical permissions across providers.

## IAM Security Best Practices

1. **Use least privilege:** Grant only the permissions needed for the task and scope access narrowly.
2. **Require strong authentication:** Enable MFA for human identities, especially privileged users.
3. **Prefer group-based access:** Use groups and role assignments to keep permissions consistent and manageable.
4. **Separate human and workload identities:** Applications should use managed or workload identities rather than personal user credentials.
5. **Avoid long-lived credentials:** Prefer temporary credentials, managed identities, and federation where supported.
6. **Review privileged access:** Audit Owner, Administrator, and equivalent roles regularly.
7. **Monitor identity activity:** Review sign-in events, role changes, policy changes, and audit logs.
8. **Remove stale access:** Disable unused identities and remove obsolete permissions and credentials.
9. **Protect recovery methods:** Secure recovery codes and administrative break-glass accounts and monitor their use.
10. **Document changes:** Record the purpose, scope, validation result, and cleanup steps for each lab.

## Troubleshooting and Validation

| Issue | What to check |
| --- | --- |
| User cannot sign in | Account status, username, authentication method, MFA registration, and sign-in policy. |
| User can sign in but cannot access a resource | Role assignment, policy statements, resource scope, group membership, and inherited permissions. |
| Permission changes are not visible | Confirm the change was saved, check propagation time, refresh the session, and verify the correct identity is signed in. |
| User has more access than expected | Review direct and inherited assignments, group memberships, attached policies, and broader roles. |
| Workload cannot access a service | Check its service identity, trust relationship, token or credential configuration, and narrowly scoped permissions. |

Never work around an authorization error by granting broad administrator access. Identify the missing permission and determine whether it is genuinely required.

## Lab Cleanup

At the end of each exercise:

1. Record the configuration and validation results using sanitized notes.
2. Remove test users, group memberships, role assignments, and policies created only for the exercise.
3. Delete temporary service identities and revoke keys or credentials that are no longer required.
4. Confirm that no privileged access was left assigned unintentionally.
5. Review provider audit logs and resource inventories where appropriate.
6. Record the cleanup result.

Do not remove shared or pre-existing identities, policies, or resources. Only remove items you created for the lab and are authorized to delete.

See the repository's [Lab Cleanup Guide](../LAB-CLEANUP-GUIDE.md) for the general cleanup process.

---

## Further Learning

- [AWS IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Microsoft Entra security operations](https://learn.microsoft.com/en-us/entra/architecture/security-operations-introduction)
- [Azure RBAC best practices](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)
- [Google Cloud IAM best practices](https://cloud.google.com/iam/docs/using-iam-securely)

**Stay Curious. Stay Sharp. Stay Secure.**
