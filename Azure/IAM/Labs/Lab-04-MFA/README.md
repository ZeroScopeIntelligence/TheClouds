# Lab 04 – Multifactor Authentication (MFA)

## Objective
Understand how MFA strengthens authentication and how authentication methods are managed in Microsoft Entra ID. This lab reviews the Microsoft Authenticator method policy and verifies that the method is enabled for all users in the lab tenant.

## Scenario
The organization wants stronger sign-in protection for workforce identities, especially accounts with elevated permissions. Microsoft Authenticator is enabled as an available authentication method for all users.

## Prerequisites
- A dedicated lab tenant and test users.
- An administrator authorized to review and manage authentication-method policies.
- A supported device for Microsoft Authenticator registration.
- Awareness of the tenant's current security defaults and Conditional Access configuration.

## Tasks

### 1. Open Authentication methods
1. Open the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Navigate to **Entra ID > Authentication methods**.
3. Locate the **Authentication method policies** section.

### 2. Review the Microsoft Authenticator policy
1. Under **Authentication method policies**, find **Microsoft Authenticator**.
2. Confirm that the method is **Enabled**.
3. Select **Microsoft Authenticator** to open its configuration.
4. Under the **Enable and Target** settings, verify that the method is enabled for **All users**.
5. If the lab tenant is not configured this way, update the policy to **Enable** and target **All users**, then save the change if you are authorized to do so.
6. Return to the policy list and confirm that Microsoft Authenticator is shown as enabled.

> **Important:** Enabling Microsoft Authenticator for all users makes it an available authentication method for the targeted users. It does not automatically register every user's device or prove that every user has completed MFA setup. Users may still need to register the app, and an MFA requirement must be enforced through an applicable policy or security-default setting.

### 3. Register and test a lab user
1. Use a dedicated test identity and follow Microsoft's official [security information registration](https://mysignins.microsoft.com/security-info) process.
2. Register Microsoft Authenticator on the test user's supported device.
3. Sign in as the test user and verify that the expected authentication challenge is presented when MFA is required.
4. Review the sign-in logs and confirm the authentication details.
5. Document the result without recording authentication secrets, QR codes, or recovery codes.

### 4. Review other MFA enforcement
1. Review whether Security Defaults or Conditional Access already enforce MFA.
2. Understand how the existing configuration affects the test user's sign-in.
3. Avoid creating overlapping or broad policies without understanding their interaction and testing them safely.

## Validation
- Microsoft Authenticator is **Enabled** under Authentication method policies.
- The Microsoft Authenticator configuration targets **All users**.
- The dedicated test identity has successfully registered the method.
- A test sign-in produces the expected MFA challenge when MFA is required.
- The sign-in log records the authentication result.

## Zero Trust connection
A password alone should not be treated as sufficient proof of identity. MFA strengthens identity verification, but it does not replace authorization, device evaluation, or monitoring. Enabling an authentication method and requiring users to complete MFA are related but separate configuration steps.

## Safety notes
- Perform changes in a dedicated lab tenant.
- Do not experiment with MFA requirements on your only administrator account.
- Maintain a separately protected emergency-access account and monitor its use.
- Before targeting all users, review the impact and ensure appropriate recovery and emergency-access arrangements are in place.
- Never publish recovery codes, QR codes, phone numbers, or authentication secrets.

## Cleanup
If you changed the policy for this exercise, document the original setting and restore it only if required by the lab owner. Do not disable a tenant-wide authentication method without authorization. Remove test authentication methods only when the account is no longer needed and only after confirming the account's recovery requirements.

## Evidence
Capture the Authentication method policies page showing Microsoft Authenticator enabled and its configuration showing **All users** selected. Also capture a redacted test sign-in log showing the MFA result. Do not include QR codes, phone numbers, recovery codes, or other authentication secrets.
