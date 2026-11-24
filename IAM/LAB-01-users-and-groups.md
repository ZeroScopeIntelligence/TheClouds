# Lab 01: Create IAM Users, Groups, and Membership

## Objective
Create four ordinary IAM users and two IAM groups. Add two users to each group so the later labs can demonstrate how group-based permissions work.

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

## Sample Employee Directory

| Employee name | Suggested username | IAM group | Department |
| --- | --- | --- | --- |
| James Wilson | `jwilson` | `Cloud-Audit-Readers` | Finance |
| Emily Carter | `ecarter` | `Cloud-Audit-Readers` | Compliance |
| Michael Rodriguez | `mrodriguez` | `Cloud-S3-Operators` | IT |
| Sophia Martinez | `smartinez` | `Cloud-S3-Operators` | Development |

Use these as display names and suggested usernames for ordinary human IAM users. Adapt usernames if they already exist in your AWS account. These are not IAM roles or service identities.

## Create an IAM Group from the AWS Console Search Bar

You can create a group directly from the IAM console and add users while creating it:

1. In the AWS Management Console, use the top **Search** bar to search for **IAM**, then open the IAM service.
2. In the IAM navigation pane, select **User groups** (sometimes shown as **IAM groups**).
3. Select **Create group**.
4. Enter the group name. For this walkthrough, enter `IT`. Group names can contain spaces; use clear names that match the department or team's purpose.
5. Under **Select users**, choose the existing IAM users who should belong to this group. You can skip this selection if you have not created the users yet and add them later.
6. Under **Attach permissions policies**, find and select the policy for the lab.
7. Select only least-privilege policies for the group's purpose. For this lab, prefer **ReadOnlyAccess** plus a relevant service-specific access policy when needed. Do not select **AdministratorAccess**.
8. Review the group name, selected users, and attached policy, then select **Create group**.

**Important security rule:** Never attach **AdministratorAccess** to this group or assign full administrator permissions to an ordinary user. Use **ReadOnlyAccess** when read-only visibility is appropriate, and add only the specific service or resource access policy required for the user's duties. Review the permissions granted by every attached policy; broad read access can still expose sensitive data. The repository's default standard is least privilege.

After the group is created, open **IAM → User groups → IT** and verify its members and attached policies. Group membership gives users the group's permissions, so review both before adding users.

## Configure the AWS Account Password Policy

You can set an account-wide password policy from IAM Account settings. This policy applies to IAM users in the AWS account.

1. In the AWS Management Console, search for **IAM** and open the IAM service.
2. In the IAM navigation pane, select **Account settings**.
3. Find **Password policy** and select **Edit**.
4. Choose **Custom** to configure the password requirements.
5. Set the minimum password length to **12 characters**.
6. Under **Password strength**, select all available complexity options:
   - Require at least one uppercase letter
   - Require at least one lowercase letter
   - Require at least one number
   - Require at least one non-alphanumeric character (special character)
7. Under **Other requirements**:
   - Enable **Password expiration** and set it to **60 days**.
   - Enable **Allow users to change their own password**.
   - Enable **Prevent password reuse**. If the console asks for a number of previous passwords to remember, choose the value specified by your lab or organization.
8. Review the settings and save the password policy.

**Verify the policy:** Return to **IAM → Account settings → Password policy** and confirm the minimum length, all password-strength options, 60-day expiration, user self-service password changes, and password reuse prevention are enabled.

**Security note:** This is an account-wide policy for IAM users; it does not replace MFA. Follow any stronger organizational requirements. Password expiration is included here as a lab configuration requirement; real organizations should set expiration rules according to their security policy and current guidance.

## Add or Change Permissions on an Existing IAM Group

After creating a group, you can return to it later to attach additional policies:

1. In the AWS Management Console, search for **IAM** and open the IAM service.
2. Select **User groups** (or **IAM groups**) in the navigation pane.
3. Select the group you want to update. For this walkthrough, open **IT**.
4. Open the **Permissions** section or tab.
5. Select **Add permissions**. A drop-down menu appears.
6. Choose **Attach policies**.
7. Search the available policies and select only the policies that match the group's responsibilities.
8. For general read-only visibility, consider **ReadOnlyAccess**. Then add a suitable service-specific policy only when the group needs access to that service. For example, use a narrowly scoped S3 policy for an S3 task rather than granting broad permissions across AWS.
9. Review the selected policies and choose **Add permissions** / **Attach policies** to apply them (the final button label may vary with the console view).
10. Return to the group's **Permissions** section and verify the attached policies.

**Least-privilege reminder:** Prefer read-only access plus a narrowly scoped service access policy where appropriate. Do not attach **AdministratorAccess** or give full administrator permissions to ordinary users. A group's attached policies apply to its members, so check the policy's actions and resource scope before attaching it. Remove policies that are no longer required.

## Create a User from the AWS Console Search Bar

If you are using the AWS Management Console's search navigation, you can create a user this way:

1. Sign in to the AWS Management Console with your authorized lab account. Do not use the root user for routine administration.
2. Use the top **Search** bar to search for **IAM** and open the IAM service.
3. In the IAM navigation pane, select **Users** (or **IAM users**, depending on the console view).
4. Select **Create user** in the upper-right area of the Users page.
5. Enter the new user's unique **User name**, then select **Next**.
6. On the permissions step, choose **Add user to group** and select the existing group that matches the user's department or job duties. If the group has not been created yet, create it first under **IAM → User groups → Create group**.
7. Select **Next**, review the user name and selected group, then select **Create user**.

The user is now created and is a member of the selected group. Group membership alone does not grant access unless the group has permissions attached. Keep permissions least-privilege and add only the policies required by the lab.

**Sign-in access note:** This flow creates the IAM user and assigns group membership. If a lab specifically requires AWS Management Console sign-in or programmatic access, configure only the required access method afterward and follow the lab's credential-handling and MFA requirements. Do not create access keys unless a task explicitly needs them, and never commit credentials to GitHub.

## Steps

1. Sign in to the AWS Management Console using an authorized lab administrator. Do not use the root user for routine work.
2. Open **IAM → User groups → Create group**.
3. Create `Cloud-Audit-Readers`. Do not attach a policy yet.
4. Repeat to create `Cloud-S3-Operators`.
5. Open **IAM → Users → Create user**.
6. Create James Wilson (`jwilson`) and Emily Carter (`ecarter`).
7. Create Michael Rodriguez (`mrodriguez`) and Sophia Martinez (`smartinez`).
8. Configure console access only if required for the lab. Follow the account's password and MFA requirements; never store passwords in this repository.
9. Add James Wilson and Emily Carter to `Cloud-Audit-Readers`.
10. Add Michael Rodriguez and Sophia Martinez to `Cloud-S3-Operators`.
11. Require MFA for interactive test access where supported.

## Validation

- Confirm both groups exist.
- Confirm each group has its two intended members.
- Open each user and verify its group membership.
- No group policies are attached yet; Lab 02 adds them.

## Security Notes

These are disposable learning identities. For workforce access in real environments, study IAM Identity Center and federation. Never publish passwords, access keys, secret keys, or MFA recovery information.


## Expanded fictional company directory

Use this fictional roster to practice department-based identity administration. These are sample names and usernames only; check for naming conflicts and use your provider's required sign-in format.

| Employee | Username | Department | Group |
|---|---|---|---|
| Olivia Bennett | `obennett` | Human Resources | `HR-Readers` |
| Ethan Brooks | `ebrooks` | Human Resources | `HR-Staff` |
| Maya Patel | `mpatel` | Sales | `Sales-Users` |
| Noah Thompson | `nthompson` | Sales | `Sales-Users` |
| Ava Garcia | `agarcia` | Finance | `Finance-Readers` |
| Liam Chen | `lchen` | Finance | `Finance-Analysts` |
| Sophia Martinez | `smartinez` | IT | `IT-Operators` |
| James Wilson | `jwilson` | IT | `IT-Auditors` |
| Isabella Rivera | `irivera` | Development | `Dev-Engineers` |
| Lucas Kim | `lkim` | Development | `Dev-Engineers` |
| Mia Johnson | `mjohnson` | Support | `Support-Readers` |
| Daniel Lewis | `dlewis` | Support | `Support-Operators` |

Create each distinct group in the table, create the 12 test users, and add each user to the group shown. Never store passwords, API keys, access keys, or tokens in this repository.

### Suggested access boundaries

- **HR:** access only to dedicated HR lab resources; do not grant access to real employee records.
- **Sales:** application-specific access to a dedicated sales test resource.
- **Finance:** read-only or analytics access to isolated finance test resources.
- **IT:** separate operational and audit groups; audit membership must not imply administrative rights.
- **Development:** permissions scoped to a dedicated development environment.
- **Support:** diagnostic access limited to approved support resources.

Do not attach broad administrator permissions to department groups. Apply the narrowest resource-specific permissions and test both allowed and denied actions.

For workforce access in production, prefer IAM Identity Center and federation with temporary credentials over long-lived IAM users.


## Cleanup
Keep the users and groups for Labs 02 and 03. Delete them when the exercise series is complete.

## References
- [Create IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
- [IAM user groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html)
