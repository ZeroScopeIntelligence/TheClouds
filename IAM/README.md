# Google Cloud IAM

## Purpose
Learn how identities are created, organized into groups, assigned permissions, and tested using least privilege.

## How Google Cloud IAM Works
Google Cloud IAM does not create ordinary human user accounts inside a project. User identities and Google Groups are managed through Google Workspace or Cloud Identity. Cloud IAM grants roles to group principals through allow-policy bindings on resources.

## Lab Sequence

| Lab | Topic | Status |
| --- | --- | --- |
| 01 | [Prepare users, groups, and membership](./LAB-01-users-and-groups.md) | Ready |
| 02 | [Assign different IAM roles to groups](./LAB-02-group-permissions.md) | Ready |
| 03 | [Test, audit, and clean up access](./LAB-03-test-and-cleanup.md) | Ready |
| 04 | [Department-based identity directory](./LAB-04-department-directory.md) | Ready |

## Permission Design

| Group | Role | Scope |
| --- | --- | --- |
| `cloud-project-viewers` | `roles/viewer` | Dedicated lab project |
| `cloud-storage-operators` | `roles/storage.objectUser` | Dedicated test bucket |

## Troubleshooting

See the [troubleshooting guide](../Troubleshooting/README.md) for permission errors, group membership, API credentials, and audit diagnostics.

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

## Safety Checklist
- Use disposable lab identities in a non-production environment.
- Enable MFA for privileged identities.
- Avoid broad Owner and Editor roles.
- Review each role's effective permissions and scope.
- Remove temporary access after testing.

## References
- [Lab template](../LAB-TEMPLATE.md)
- [Notes](../NOTES.md)
- [Google Cloud IAM documentation](https://cloud.google.com/iam/docs/overview)
