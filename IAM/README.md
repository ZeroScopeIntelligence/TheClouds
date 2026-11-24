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
