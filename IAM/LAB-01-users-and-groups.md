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
