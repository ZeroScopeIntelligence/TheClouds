# Lab 04: Department-Based Identity Directory

## Objective

Build a fictional company identity directory with HR, Sales, Finance, IT, Development, and Support departments. Create department groups, add test users, and document least-privilege access boundaries.

## Sample directory

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

## Steps

1. Use a dedicated non-production account, tenant, or organization.
2. Create the distinct groups listed above.
3. Create the fictional test users using the provider's identity service.
4. Add each user to the corresponding group.
5. Apply permissions only after identifying the exact lab resources each group needs.
6. Test with non-administrator identities and record allowed and denied actions.
7. Never record passwords, tokens, API keys, or private keys.

## Provider-specific identity model

Create human users and Google Groups in Workspace or Cloud Identity. Grant Cloud IAM roles to group principals through resource policy bindings at the narrowest project, folder, bucket, or resource scope.

## Validation checklist

- [ ] All 12 fictional users exist in the lab identity directory.
- [ ] Each department group exists.
- [ ] Each user is a member of the intended group.
- [ ] Permissions match the documented access boundaries.
- [ ] Users are denied access to unrelated department resources.
- [ ] No real credentials or production identities were committed.

## Cleanup

Remove test users, groups, and role assignments when the exercise series is complete. Keep only identities required by other labs.

## Next

Continue with [Lab 02: Group permissions](./LAB-02-group-permissions.md) and [Lab 03: Test, audit, and cleanup](./LAB-03-test-and-cleanup.md).
