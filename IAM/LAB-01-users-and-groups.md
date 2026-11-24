# Lab 01: Prepare Google Cloud User Identities, Groups, and Membership

## Objective
Prepare four ordinary human user identities and two Google Groups, then add two users to each group.

## Important Identity Model
Google Cloud IAM does not create ordinary human user accounts inside a project. User identities and Google Groups are managed through Google Workspace or Cloud Identity. Cloud IAM grants roles to these group principals in Lab 02.

If you only have a personal Google account without a managed organization, group creation through the Admin console may not be available. Use a managed domain and identities you are authorized to administer.

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

| Employee name | Suggested username | Google Group | Department |
| --- | --- | --- | --- |
| James Wilson | `jwilson` | `cloud-project-viewers` | Finance |
| Emily Carter | `ecarter` | `cloud-project-viewers` | Compliance |
| Michael Rodriguez | `mrodriguez` | `cloud-storage-operators` | IT |
| Sophia Martinez | `smartinez` | `cloud-storage-operators` | Development |

These are standard human user accounts managed by Google Workspace or Cloud Identity, not service accounts. Create the corresponding email addresses using a domain managed by your organization; the usernames are suggestions.

## Steps

1. Sign in to the [Google Admin console](https://admin.google.com/) with an authorized administrator.
2. Open **Directory → Users** and create four dedicated lab users: James Wilson (`jwilson`), Emily Carter (`ecarter`), Michael Rodriguez (`mrodriguez`), and Sophia Martinez (`smartinez`). Use your managed domain for their email addresses.
3. Follow your organization's password and sign-in requirements. Never place passwords in this repository.
4. Open **Directory → Groups → Create group**.
5. Create `cloud-project-viewers`.
6. Repeat to create `cloud-storage-operators`.
7. Open `cloud-project-viewers`, choose **Add members**, and add James Wilson and Emily Carter.
8. Open `cloud-storage-operators` and add Michael Rodriguez and Sophia Martinez.
9. Review group visibility and posting settings. Do not make groups public for this exercise.

## Validation
Confirm both groups exist and each contains the two intended test users. No Cloud IAM roles are granted yet; Lab 02 handles permissions.


## Expanded fictional company directory

Use this fictional roster to practice department-based identity administration. These are sample names and usernames only; check for naming conflicts and use your provider's required sign-in format.

| Employee | Username | Department | Group |
|---|---|---|---|
| Olivia Bennett | `obennett` | Human Resources | `hr-readers` |
| Ethan Brooks | `ebrooks` | Human Resources | `hr-staff` |
| Maya Patel | `mpatel` | Sales | `sales-users` |
| Noah Thompson | `nthompson` | Sales | `sales-users` |
| Ava Garcia | `agarcia` | Finance | `finance-readers` |
| Liam Chen | `lchen` | Finance | `finance-analysts` |
| Sophia Martinez | `smartinez` | IT | `it-operators` |
| James Wilson | `jwilson` | IT | `it-auditors` |
| Isabella Rivera | `irivera` | Development | `dev-engineers` |
| Lucas Kim | `lkim` | Development | `dev-engineers` |
| Mia Johnson | `mjohnson` | Support | `support-readers` |
| Daniel Lewis | `dlewis` | Support | `support-operators` |

Create each distinct group in the table, create the 12 test users, and add each user to the group shown. Never store passwords, API keys, access keys, or tokens in this repository.

### Suggested access boundaries

- **HR:** access only to dedicated HR lab resources; do not grant access to real employee records.
- **Sales:** application-specific access to a dedicated sales test resource.
- **Finance:** read-only or analytics access to isolated finance test resources.
- **IT:** separate operational and audit groups; audit membership must not imply administrative rights.
- **Development:** permissions scoped to a dedicated development environment.
- **Support:** diagnostic access limited to approved support resources.

Do not attach broad administrator permissions to department groups. Apply the narrowest resource-specific permissions and test both allowed and denied actions.

Google Cloud human users and Google Groups are managed through Workspace or Cloud Identity. Cloud IAM grants roles to group principals through resource policy bindings.


## Cleanup
Keep users and groups for Labs 02 and 03. Delete only identities and groups created specifically for this lab when the series is complete.

## References
- [Create a user](https://cloud.google.com/identity/docs/how-to/create-user)
- [Google Groups administration](https://support.google.com/a/answer/33343)
