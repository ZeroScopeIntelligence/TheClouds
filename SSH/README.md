# Azure SSH Labs

Hands-on exercises for securely administering Linux virtual machines over SSH in Azure.

## Learning objectives

- Understand SSH client/server authentication and host keys.
- Generate and protect an Ed25519 SSH key pair.
- Register a public key using the cloud provider's supported workflow.
- Restrict network access to SSH (TCP 22).
- Connect to an approved VPN before remote access, then connect to a Linux VM and verify the remote system.
- Troubleshoot common SSH connectivity and authentication errors.
- Remove temporary access and cloud resources after the exercise.

## Labs

- [Lab 01: Configure secure SSH access to a Linux VM](./LAB-01-secure-ssh-access.md)

## Security baseline

- Use a dedicated lab account/project and a non-production VM.
- **Always connect through an approved, trusted VPN before remote administration.** Keep it connected for the entire session.
- Prefer public-key authentication and keep private keys on your workstation.
- Restrict SSH ingress to the VPN's known egress IP (/32) or use a private access service, where practical.
- Never expose port 22 to the entire internet. A VPN does not replace SSH key authentication or firewall restrictions.
- Do not enable direct root login or commit credentials to source control.
- Clean up the VM, temporary firewall rules, keys, and other lab resources when finished.

## Official documentation

https://learn.microsoft.com/azure/virtual-machines/linux/ssh-from-windows
