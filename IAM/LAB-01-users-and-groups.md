# Lab 01: Create IAM Users, Groups, and Membership

## Objective
Create four ordinary IAM users and two IAM groups. Add two users to each group so the later labs can demonstrate how group-based permissions work.

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

## Cleanup
Keep the users and groups for Labs 02 and 03. Delete them when the exercise series is complete.

## References
- [Create IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
- [IAM user groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html)
