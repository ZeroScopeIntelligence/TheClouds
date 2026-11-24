# Lab 01: Create Microsoft Entra Users, Security Groups, and Membership

## Objective
Create four ordinary cloud-only Microsoft Entra ID test users and two security groups. Add two users to each group.

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

| Employee name | Suggested username | Security group | Department |
| --- | --- | --- | --- |
| James Wilson | `jwilson` | `Resource-Readers` | Finance |
| Emily Carter | `ecarter` | `Resource-Readers` | Compliance |
| Michael Rodriguez | `mrodriguez` | `Storage-Contributors` | IT |
| Sophia Martinez | `smartinez` | `Storage-Contributors` | Development |

These are standard human user identities, not service principals or managed identities. Use your tenant's verified domain when creating each user's sign-in name; the usernames above are suggestions.

## Prerequisites
An authorized Entra tenant, permission to create users and groups, and permission to assign Azure RBAC roles in Lab 02. Use a dedicated non-production tenant where possible.

## Steps: Create Groups

1. Open [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Navigate to **Entra ID → Groups → All groups → New group**.
3. Set group type to **Security** and membership type to **Assigned**.
4. Create `Resource-Readers`.
5. Repeat for `Storage-Contributors`.

## Alternative: Create a User Using the Entra Admin Center Search Bar

You can also start user creation from the admin center's search bar. In the current portal navigation, users and groups are found under **Entra ID**. The exact labels can vary slightly as Microsoft updates the portal.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) with an authorized account.
2. Use the portal **Search** bar to search for **Users** and open **Entra ID → Users**.
3. Select **Add user**, then choose **Create new user**.
4. In **User principal name**, enter the user's unique username (for example, `obennett`) and select your tenant's verified domain. This is the user's sign-in name.
5. Edit the **Display name** so it shows the person's full name (for example, Olivia Bennett).
6. Continue to the password section. Generate a unique initial password for this user that is at least **12 characters** and contains at least **one special character**, while meeting any stronger tenant requirements. Do not reuse a password from another account or put it in this repository. Deliver it securely and select the option to require the user to change the password at next sign-in when available.
7. Select **Next: Properties** (or the equivalent next step). Enter the user's **First name** and **Last name**.
8. Under **Job information**, enter the user's job title. Add department details if the lab or tenant uses them.
9. Continue to **Assignments**. Add the user to the correct department security group that you created earlier (for example, an HR user to `HR-Readers` or `HR-Staff`). Do not assign extra directory roles or Azure resource permissions unless a later lab specifically requires them.
10. Select **Next: Review + create**, check the username, display name, first and last name, job title, and group membership, then select **Create**.
11. Open the new user record and verify the account and group membership. Repeat the process for each fictional employee, using a different username and unique initial password for every account.

**Important:** The password is an initial sign-in credential, not a shared team password. Give it to the intended user through an approved secure method. The user should set their own password at first sign-in if the tenant supports that workflow.

## Steps: Create Users

1. Navigate to **Entra ID → Users → All users → New user → Create new user**.
2. Create James Wilson (`jwilson`), Emily Carter (`ecarter`), Michael Rodriguez (`mrodriguez`), and Sophia Martinez (`smartinez`). Set their display names and use sign-in names under your tenant's verified domain.
3. Follow tenant password and sign-in requirements. Never place passwords in this repository.
4. Open **Entra ID → Groups → All groups → Resource-Readers → Members → Add members** and add James Wilson and Emily Carter.
5. Open **Entra ID → Groups → All groups → Storage-Contributors → Members → Add members** and add Michael Rodriguez and Sophia Martinez.

## Validation
Open each group and verify it contains the two intended members. No Azure resource role is assigned in this lab; that occurs in Lab 02.

## Important Distinction
Entra ID manages users and groups. Azure RBAC controls access to Azure resources. Creating a group does not automatically give it access to a subscription or resource.


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

Entra groups organize identities; Azure RBAC role assignments grant access to Azure resources at a defined scope. Keep directory roles separate from resource roles.


## Cleanup
Keep these test identities and groups for Labs 02 and 03. Remove them after the exercise if they are not used elsewhere.

## References
- [Create users in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users)
- [Manage groups](https://learn.microsoft.com/entra/fundamentals/how-to-manage-groups)
