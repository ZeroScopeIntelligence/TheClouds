# Lab 04: Department-Based Identity Directory

## Objective

Build a fictional company identity directory with HR, Sales, Finance, IT, Development, and Support departments. Create department groups, add test users, and document least-privilege access boundaries.

## Sample directory

| Employee | Username | Department | Group |
|---|---|---|---|
| Olivia Bennett | `obennett` | Human Resources | `ZS-HR-Readers` |
| Ethan Brooks | `ebrooks` | Human Resources | `ZS-HR-Staff` |
| Maya Patel | `mpatel` | Sales | `ZS-Sales-Users` |
| Noah Thompson | `nthompson` | Sales | `ZS-Sales-Users` |
| Ava Garcia | `agarcia` | Finance | `ZS-Finance-Readers` |
| Liam Chen | `lchen` | Finance | `ZS-Finance-Analysts` |
| Sophia Martinez | `smartinez` | IT | `ZS-IT-Operators` |
| James Wilson | `jwilson` | IT | `ZS-IT-Auditors` |
| Isabella Rivera | `irivera` | Development | `ZS-Dev-Engineers` |
| Lucas Kim | `lkim` | Development | `ZS-Dev-Engineers` |
| Mia Johnson | `mjohnson` | Support | `ZS-Support-Readers` |
| Daniel Lewis | `dlewis` | Support | `ZS-Support-Operators` |

## Steps

1. Use a dedicated non-production account, tenant, or organization.
2. Create the distinct groups listed above.
3. Create the fictional test users using the provider's identity service.
4. Add each user to the corresponding group.
5. Apply permissions only after identifying the exact lab resources each group needs.
6. Test with non-administrator identities and record allowed and denied actions.
7. Never record passwords, tokens, API keys, or private keys.

## Provider-specific identity model

Create users and security groups in Microsoft Entra ID. Assign Azure RBAC roles to groups at the narrowest resource, resource-group, or subscription scope needed. Entra directory roles and Azure resource roles are different.

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
