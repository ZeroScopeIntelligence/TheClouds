# Troubleshooting and Common Cloud Access Issues

This guide covers common identity, permission, API credential, and access problems in the Microsoft Azure labs.

## Recommended troubleshooting workflow

1. Identify the exact user or workload identity, group, resource, requested action, and timestamp.
2. Reproduce the issue with the affected non-administrator test identity.
3. Verify account status, sign-in events, group membership, and recent changes.
4. Inspect effective permissions at the resource's actual scope.
5. Check explicit denies, inherited policies, conditions, boundaries, organization policies, and resource-level policies.
6. Make the smallest justified correction, then test both allowed and denied actions.
7. Record the cause and resolution without secrets or unnecessary personal information.

## Common problems

### 1. Misconfigured permissions or access denied

**Symptoms:** Access denied/forbidden errors, or a user can view a resource but cannot modify it.

**Check:** Correct identity; group membership; assigned role or policy; resource scope; management-plane versus data-plane permission; explicit denies, conditions, permission boundaries, deny assignments, and organization policies.

**Resolution:** Correct the specific group membership or narrowly scoped role/policy. Never resolve an error by granting unrestricted Owner, Administrator, or Contributor access.

### 2. Incorrect or missing group membership

**Symptoms:** A new employee cannot access a resource even though the department group has a role.

**Check:** Exact user and group, nested-group behavior, dynamic membership rules, and propagation delay.

**Resolution:** Add the identity to the approved group or correct the membership rule. Allow changes to propagate and refresh the sign-in session before retesting.

### 3. API keys, access keys, and token failures

**Symptoms:** Invalid credentials, unauthorized API calls, expired tokens, or authentication failures.

**Check:** Intended service identity and environment; expiration, revocation, or disablement; credential source; required API/service enablement; required permissions; system clock for time-based tokens.

**Resolution and credential safety:**
- Never paste API keys, access keys, client secrets, private keys, refresh tokens, or bearer tokens into GitHub, tickets, screenshots, or chat.
- If a credential may have been exposed, revoke or disable it promptly, review audit activity, and issue a replacement using the provider's secure workflow.
- Store secrets in an approved secrets manager or protected environment variables with restricted access.
- Prefer short-lived credentials, workload identity, managed identity, or service-account impersonation over long-lived static keys where supported.
- Do not put an employee's personal API key into shared application configuration.

### 4. Wrong account, tenant, subscription, project, or region

**Symptoms:** The expected resource is missing or a seemingly correct role does not work.

**Check:** Active account, tenant/directory, subscription or project, region, and full resource identifier.

**Resolution:** Switch to the intended authorized environment and verify the resource path before making permission changes.

### 5. Role changes have not taken effect

**Symptoms:** Access still fails after a role or group update.

**Check:** Confirm the change was saved; inspect effective assignments; consider propagation delay and cached sessions or tokens.

**Resolution:** Wait for propagation, obtain a fresh sign-in or token where appropriate, and retest. Do not repeatedly add broader roles.

### 6. Workload or service identity authentication fails

**Symptoms:** A VM, application, or automation job cannot call a cloud API.

**Check:** Intended workload identity; identity enabled; API/service enabled; required role granted on the correct resource; application configured to use the expected identity.

**Resolution:** Prefer managed/workload identity and grant only the required role. Avoid embedding human credentials or static keys in source code.

### 7. Missing audit evidence

**Symptoms:** The team cannot determine who changed a role or why access was denied.

**Check:** Provider audit logs, sign-in logs, activity logs, and service-specific logs. Confirm logging was enabled and the investigator has read access.

**Resolution:** Enable appropriate audit logging for the lab, protect log access, and record timestamps, request IDs, and resource identifiers without recording secrets.

## Provider documentation

- [Troubleshoot Azure RBAC](https://learn.microsoft.com/azure/role-based-access-control/troubleshooting)
- [Microsoft Entra sign-in logs](https://learn.microsoft.com/entra/identity/monitoring-health/concept-sign-ins)
- [Managed identities](https://learn.microsoft.com/entra/identity/managed-identities-azure-resources/overview)

## Lab safety

Use only fictional identities and resources you are authorized to administer. Never commit credentials or attempt to bypass access controls.
