# Lab 02 – User and Group Management

## Objective
Organize test identities into Microsoft Entra groups so access can be assigned consistently and reviewed centrally.

## Scenario
A fictional organization uses department and security-focused groups to organize identities across Administration, Finance, Help Desk, HR, IT, Sales, and Security. This lab uses the group inventory shown in the Microsoft Entra admin center as a reference.

## Prerequisites
- Complete Lab 01.
- A dedicated lab tenant and permission to manage users and groups.
- Use fictional test identities and non-production data.

## Tasks
1. Open the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Navigate to **Entra ID > Groups > All groups**.
3. Review the group list and identify each group's **Group type** and **Membership type**.
4. Create the example groups listed below if they do not already exist in your lab tenant. Use **Assigned** membership for this exercise.
5. Add fictional test users to the appropriate groups.
6. Open each group's **Members** page and verify membership.
7. Review group owners and document who is responsible for membership changes.
8. Do not assign directory-wide or subscription-wide administrator roles simply because a user belongs to a department group.

## Example group inventory

The following nine groups are represented in the Microsoft Entra admin center screenshot used for this lab:

| Group name | Group type | Membership type | Email |
|---|---|---|---|
| Administrators | Security | Assigned | — |
| Finance | Security | Assigned | — |
| Help Desk | Security | Assigned | — |
| HR | Microsoft 365 | Assigned | HR@zeroscopeinteloutlook955.onmicrosoft.com |
| IT | Security | Assigned | — |
| Sales | Security | Assigned | — |
| Security Admins | Security | Assigned | — |
| Security Analysts | Security | Assigned | — |
| Security Team | Security | Assigned | — |

The email address is shown for the HR Microsoft 365 group in the reference screenshot. Email addresses and group availability can differ between tenants. Object IDs are intentionally not reproduced because they are tenant-specific identifiers.

### Group type reference

- **Security:** Used to manage access to resources and assign permissions to a collection of users, devices, or service principals.
- **Microsoft 365:** Provides collaboration features for group members, such as a shared mailbox, calendar, SharePoint site, and other connected services, depending on configuration.

### Membership type reference

- **Assigned:** An administrator manually adds and removes members.
- **Dynamic User:** Membership is determined automatically by user attributes and a configured rule.
- **Dynamic Device:** Membership is determined automatically by device attributes and a configured rule.

For this lab, the groups in the inventory use **Assigned** membership.

## Example membership plan

| Example user | Example group |
|---|---|
| Alex Morgan | Security Analysts |
| Jordan Lee | IT |
| Taylor Reed | Finance |
| Casey Quinn | Administrators |

These names are examples. Use the test accounts created in your own tenant, and grant only the access required for each exercise.

## Validation
- Review the nine groups in the example inventory, or create the groups that are appropriate for your lab.
- Confirm each group's type and membership type.
- Verify that test users belong only to their intended groups.
- Confirm group owners and document membership responsibilities.
- Do not grant unrelated or excessive permissions.

## Zero Trust connection
Groups simplify access administration, but membership should not grant broad access by default. Each group's permissions must be justified and scoped to the work its members perform. Review membership regularly and remove access when it is no longer required.

## Cleanup
Remove temporary memberships and delete only the test groups created for this exercise when the lab is complete. Do not delete pre-existing or shared groups.

## Evidence
Capture the group list, group type, membership type, and member lists. Redact tenant identifiers, personal information, and other sensitive details before saving screenshots in the repository.
