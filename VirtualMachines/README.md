# Desktop Virtualization: VMware and VirtualBox

This guide introduces two desktop virtualization platforms that can be used to build local learning environments for cloud, networking, Windows Server, Linux, and cybersecurity labs.

## Platforms

### Broadcom VMware Workstation Pro

VMware Workstation Pro runs multiple guest operating systems on a Windows or Linux desktop host. It is useful for creating Windows Server and Linux test machines, taking snapshots, and configuring virtual networks.

- Product information: https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion
- Broadcom support and knowledge base: https://knowledge.broadcom.com/

Check Broadcom's current product documentation, supported host operating systems, download process, and applicable licensing terms before installation or use.

### Oracle VirtualBox

Oracle VirtualBox is a cross-platform desktop virtualization platform for running guest operating systems on supported Windows, macOS, and Linux hosts.

- Official website: https://www.virtualbox.org/
- Downloads: https://www.virtualbox.org/wiki/Downloads
- User manual: https://www.virtualbox.org/manual/

Review the current VirtualBox manual and the separate Extension Pack license before installing optional components.

## Suggested lab use cases

- Build a Windows Server VM for Active Directory Domain Services and DNS practice.
- Create Windows and Linux client VMs to test domain joining and administration.
- Prepare Linux VMs for cloud CLI tools and automation exercises.
- Test PowerShell and shell scripts in disposable guest systems.
- Practice virtual networking, routing, and client/server communication.
- Take snapshots before major changes so you can return to a known-good state.

## Virtual networking basics

Common desktop hypervisors offer network modes such as NAT, bridged networking, and host-only or private networking. Names and behavior vary by platform.

- **NAT:** Allows a guest to use the host's network connection while typically keeping the guest behind address translation.
- **Bridged:** Connects a guest to the same network as the host, subject to the network's policies.
- **Host-only / private:** Creates a network intended for communication between the host and selected guests, depending on platform configuration.

Use an isolated host-only or private network for experiments that do not need internet access. Use NAT when guests need outbound access for updates or downloads. Avoid bridging vulnerable or untrusted test machines onto a production or shared network.

## Planning VM resources

Choose CPU, memory, and storage allocations based on the host's available resources and the guest operating system's requirements. Leave enough resources for the host to remain responsive. Dynamically allocated virtual disks can reduce initial storage use, but they may still grow to their configured maximum.

## Safe lab practices

1. Use licensed and trusted installation media.
2. Keep host operating systems and hypervisor software updated.
3. Use snapshots as short-term rollback points, not as a replacement for backups.
4. Do not store real credentials, personal information, or production data in disposable lab VMs.
5. Keep intentionally vulnerable systems on isolated networks.
6. Do not expose guest management services directly to the public internet.
7. Review each platform's documentation and license terms before use.
8. Shut down and remove lab VMs, virtual disks, snapshots, and networks when they are no longer needed.

## Suggested starter topology

```text
             Desktop Host
                  |
          Virtual Hypervisor
             /         \
            /           \
       DC01 (Server)   CLIENT01
       AD DS / DNS     Windows
            \           /
             \         /
          Private Lab Network
```

This is a conceptual lab layout. Configure IP addressing, DNS, and network isolation according to the chosen hypervisor and the goals of the exercise.

## Next steps

After building a local VM environment, continue with the cloud-provider labs in this repository. Local virtual machines are useful for learning operating systems and networking, while AWS, Azure, and Google Cloud labs introduce provider-managed infrastructure and identity services.
