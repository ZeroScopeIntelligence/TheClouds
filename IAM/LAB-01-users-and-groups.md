# Lab 01: Prepare Google Cloud User Identities, Groups, and Membership

## Objective
Prepare four ordinary human user identities and two Google Groups, then add two users to each group.

## Important Identity Model
Google Cloud IAM does not create ordinary human user accounts inside a project. User identities and Google Groups are managed through Google Workspace or Cloud Identity. Cloud IAM grants roles to these group principals in Lab 02.

If you only have a personal Google account without a managed organization, group creation through the Admin console may not be available. Use a managed domain and identities you are authorized to administer.

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

## Cleanup
Keep users and groups for Labs 02 and 03. Delete only identities and groups created specifically for this lab when the series is complete.

## References
- [Create a user](https://cloud.google.com/identity/docs/how-to/create-user)
- [Google Groups administration](https://support.google.com/a/answer/33343)
