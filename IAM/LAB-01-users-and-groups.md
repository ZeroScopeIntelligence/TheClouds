# Lab 01: Create IAM Users, Groups, and Membership

## Objective
Create four ordinary IAM users and two IAM groups. Add two users to each group so the later labs can demonstrate how group-based permissions work.

## Design

| IAM user | IAM group | Purpose |
| --- | --- | --- |
| `cloud-audit-user` | `Cloud-Audit-Readers` | Read-only review |
| `cloud-network-user` | `Cloud-Audit-Readers` | Read-only network review |
| `cloud-storage-user` | `Cloud-S3-Operators` | Work with objects in a test S3 bucket |
| `cloud-app-user` | `Cloud-S3-Operators` | Additional storage operator test identity |

These are standard IAM users for learning group membership, not IAM roles or service identities.

## Steps

1. Sign in to the AWS Management Console using an authorized lab administrator. Do not use the root user for routine work.
2. Open **IAM → User groups → Create group**.
3. Create `Cloud-Audit-Readers`. Do not attach a policy yet.
4. Repeat to create `Cloud-S3-Operators`.
5. Open **IAM → Users → Create user**.
6. Create `cloud-audit-user` and `cloud-network-user`.
7. Create `cloud-storage-user` and `cloud-app-user`.
8. Configure console access only if required for the lab. Follow the account's password and MFA requirements; never store passwords in this repository.
9. Add `cloud-audit-user` and `cloud-network-user` to `Cloud-Audit-Readers`.
10. Add `cloud-storage-user` and `cloud-app-user` to `Cloud-S3-Operators`.
11. Require MFA for interactive test access where supported.

## Validation

- Confirm both groups exist.
- Confirm each group has its two intended members.
- Open each user and verify its group membership.
- No group policies are attached yet; Lab 02 adds them.

## Security Notes

These are disposable learning identities. For workforce access in real environments, study IAM Identity Center and federation. Never publish passwords, access keys, secret keys, or MFA recovery information.

## Cleanup
Keep the users and groups for Labs 02 and 03. Delete them when the exercise series is complete.

## References
- [Create IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
- [IAM user groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html)
