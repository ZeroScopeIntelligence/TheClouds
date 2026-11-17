# Lab 01: Create Microsoft Entra Users, Security Groups, and Membership

## Objective
Create four ordinary cloud-only Microsoft Entra ID test users and two security groups. Add two users to each group.

## Sample Employee Directory

| Employee name | Suggested username | Security group | Department |
| --- | --- | --- | --- |
| James Wilson | `jwilson` | `ZS-Resource-Readers` | Finance |
| Emily Carter | `ecarter` | `ZS-Resource-Readers` | Compliance |
| Michael Rodriguez | `mrodriguez` | `ZS-Storage-Contributors` | IT |
| Sophia Martinez | `smartinez` | `ZS-Storage-Contributors` | Development |

These are standard human user identities, not service principals or managed identities. Use your tenant's verified domain when creating each user's sign-in name; the usernames above are suggestions.

## Prerequisites
An authorized Entra tenant, permission to create users and groups, and permission to assign Azure RBAC roles in Lab 02. Use a dedicated non-production tenant where possible.

## Steps: Create Groups

1. Open [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Navigate to **Identity → Groups → All groups → New group**.
3. Set group type to **Security** and membership type to **Assigned**.
4. Create `ZS-Resource-Readers`.
5. Repeat for `ZS-Storage-Contributors`.

## Steps: Create Users

1. Navigate to **Identity → Users → All users → New user → Create new user**.
2. Create James Wilson (`jwilson`), Emily Carter (`ecarter`), Michael Rodriguez (`mrodriguez`), and Sophia Martinez (`smartinez`). Set their display names and use sign-in names under your tenant's verified domain.
3. Follow tenant password and sign-in requirements. Never place passwords in this repository.
4. Open **Groups → All groups → ZS-Resource-Readers → Members → Add members** and add James Wilson and Emily Carter.
5. Open **ZS-Storage-Contributors → Members → Add members** and add Michael Rodriguez and Sophia Martinez.

## Validation
Open each group and verify it contains the two intended members. No Azure resource role is assigned in this lab; that occurs in Lab 02.

## Important Distinction
Entra ID manages users and groups. Azure RBAC controls access to Azure resources. Creating a group does not automatically give it access to a subscription or resource.

## Cleanup
Keep these test identities and groups for Labs 02 and 03. Remove them after the exercise if they are not used elsewhere.

## References
- [Create users in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users)
- [Manage groups](https://learn.microsoft.com/entra/fundamentals/how-to-manage-groups)
