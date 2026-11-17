# Lab 01: Create Microsoft Entra Users, Security Groups, and Membership

## Objective
Create four ordinary cloud-only Microsoft Entra ID test users and two security groups. Add two users to each group.

## Design

| Test user | Security group | Purpose |
| --- | --- | --- |
| `cloud-audit-user` | `ZS-Resource-Readers` | Read resource configuration |
| `cloud-network-user` | `ZS-Resource-Readers` | Read-only network review |
| `cloud-storage-user` | `ZS-Storage-Contributors` | Work with blob data in a test storage account |
| `cloud-app-user` | `ZS-Storage-Contributors` | Additional storage operator test identity |

These are standard human user identities, not service principals or managed identities.

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
2. Create four dedicated test users: `cloud-audit-user`, `cloud-network-user`, `cloud-storage-user`, and `cloud-app-user`. Use approved test UPNs in your tenant.
3. Follow tenant password and sign-in requirements. Never place passwords in this repository.
4. Open **Groups → All groups → ZS-Resource-Readers → Members → Add members** and add `cloud-audit-user` and `cloud-network-user`.
5. Open **ZS-Storage-Contributors → Members → Add members** and add `cloud-storage-user` and `cloud-app-user`.

## Validation
Open each group and verify it contains the two intended members. No Azure resource role is assigned in this lab; that occurs in Lab 02.

## Important Distinction
Entra ID manages users and groups. Azure RBAC controls access to Azure resources. Creating a group does not automatically give it access to a subscription or resource.

## Cleanup
Keep these test identities and groups for Labs 02 and 03. Remove them after the exercise if they are not used elsewhere.

## References
- [Create users in Microsoft Entra ID](https://learn.microsoft.com/entra/fundamentals/how-to-create-delete-users)
- [Manage groups](https://learn.microsoft.com/entra/fundamentals/how-to-manage-groups)
