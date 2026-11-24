# Google Cloud Lab: Configure Secure SSH Access to a Linux VM

## Objective

Deploy or use a small Linux virtual machine in your dedicated lab environment, configure secure SSH access, verify connectivity, and remove lab resources when finished.

## Prerequisites

- A separate, authorized Google Cloud lab account or project—not your primary or production account.
- A Linux VM created specifically for this exercise, or permission to administer an existing lab VM.
- An SSH client on your workstation. OpenSSH is available on most Linux/macOS systems and can be installed or enabled on Windows.
- A key pair or the provider's supported SSH identity method.
- A note of the VM name, region/zone, and resources created for cleanup.

## Security requirements

- Use SSH public-key authentication; do not enable password-based SSH just to make the lab easier.
- Keep the private key on your own workstation. Never upload it to GitHub, paste it into chat, or share it.
- Restrict inbound TCP port 22 to your current public IP address with a /32 source range, or use a private access option such as a provider bastion or IAP.
- Never expose SSH to the entire internet with `0.0.0.0/0` or `::/0`.
- Do not enable direct root login. Connect with the normal VM user and use approved privilege escalation only when required.
- Use a non-production VM and non-sensitive test data.

## Part 1: Prepare the VM

1. Create a small Linux VM in your lab environment using a supported distribution.
2. Configure a network security rule that permits TCP port 22 only from your current public IP address.
3. Configure the provider's supported SSH public-key method. Do not transfer the private key to the VM.
4. Confirm the VM is running and note its public address, or the provider's private access method.

### Provider-specific notes

Use OS Login where appropriate to manage SSH access through IAM. Google Cloud IAP TCP forwarding can provide SSH access without assigning a public IP or opening SSH to the internet.

## Part 2: Generate an SSH key pair (if needed)

On your workstation, generate a dedicated key pair for this lab:

```bash
ssh-keygen -t ed25519 -C "cloud-lab-ssh"
```

Use a passphrase when prompted. Save the key in a secure location. The public key ends in `.pub`; only the public key should be registered with the VM or provider. Keep the private key private.

On Linux/macOS, restrict access to the private key file:

```bash
chmod 600 ~/.ssh/<private-key-file>
```

Do not run this against a key file you do not own or understand.

## Part 3: Connect to the VM

Use the connection method appropriate to the platform:

```bash
gcloud compute ssh <INSTANCE_NAME> --zone <ZONE> --project <PROJECT_ID>
```

Replace placeholders with your actual lab values. For AWS, ensure the private key path is correct. For Google Cloud, authenticate with the Google Cloud CLI and select the intended project and zone first.

## Part 4: Verify the session

After connecting, run basic identification commands:

```bash
whoami
hostname
uname -a
```

Confirm that you are connected to the expected lab VM and account. Exit the SSH session when finished:

```bash
exit
```

## Part 5: Troubleshooting

- **Permission denied (publickey):** Confirm the correct username, public key registration, and private key selection. Check that the private key file is readable only by its owner.
- **Connection timed out:** Confirm the VM is running, the address is correct, the network route is available, and the firewall/NSG/security group allows TCP 22 from your current public IP.
- **Connection refused:** Confirm the VM is reachable and the SSH service is installed and running. Use the provider's serial console or recovery workflow if you are authorized.
- **Wrong key or user:** Verify the image's default Linux username and the key pair associated with this VM.
- **Your public IP changed:** Update the narrow firewall source rule to your current IP; do not broaden it to the whole internet.
- **Host key warning:** Do not blindly disable host-key checking. Verify the VM was recreated or its host key changed through a trusted provider console before updating your known-hosts entry.

Provider reference: [Official Google Cloud SSH documentation](https://cloud.google.com/compute/docs/connect/ssh-using-ssh)

## Part 6: Cleanup

1. Exit the SSH session.
2. Delete the VM if it was created only for this lab.
3. Delete lab-only disks, snapshots, public IP addresses, network interfaces, and other attached resources after confirming they are not shared.
4. Remove the temporary SSH public key, OS Login/IAM assignment, or other lab-only access configuration when no longer needed.
5. Delete temporary firewall rules or security-group rules created for this lab.
6. Securely remove the lab's local private key if it is no longer needed. Never delete a key used by another environment.
7. Check the provider resource inventory and billing dashboard for remaining resources.

Follow the repository's [Cloud Lab Cleanup Guide](../LAB-CLEANUP-GUIDE.md) where available, or the main branch guide if the branch does not contain a copy.

## Completion checklist

- [ ] SSH key-based authentication worked.
- [ ] Port 22 was restricted to a trusted source or private access method.
- [ ] I confirmed the VM identity after connecting.
- [ ] I did not expose or commit private credentials.
- [ ] I removed lab-only resources and temporary access.
- [ ] I checked for remaining billable resources.

## Lab notes

Record the VM name, region/zone, Linux distribution, connection method, and troubleshooting notes. Do not record private keys, passphrases, tokens, or other secrets.
