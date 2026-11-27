# Lab 01: Build a Google Cloud VPC with Public and Private Subnets

## Objective
Create a custom-mode VPC network with two subnets, review automatically created routes, and understand how firewall rules and external IP addresses affect connectivity.

## Concepts
- **VPC network:** A global, logically isolated network resource in Google Cloud.
- **Subnet:** A regional IPv4 or IPv6 address range within a VPC.
- **Custom-mode VPC:** A network where you explicitly define subnet ranges and regions.
- **Route:** A rule determining the next hop for network traffic.
- **Firewall rule:** A VPC-level rule controlling traffic to or from VM instances.
- **Cloud NAT:** A managed service that lets resources without external IP addresses initiate outbound connections.

> Google Cloud VPC networks are global, while their subnets are regional. A subnet is not inherently public or private. Routes, firewall policies, and external IP or Cloud NAT configuration determine connectivity.

## Topology and addressing

| Component | Name | IPv4 range |
| --- | --- | --- |
| Project | Dedicated networking lab project | Your selected project |
| VPC | network-lab | Custom mode |
| Subnet | public-subnet | 10.30.1.0/24 |
| Subnet | private-subnet | 10.30.2.0/24 |
| Region | Selected lab region | Same region for both subnets |

No VM instances, external IP addresses, or Cloud NAT resources are required.

## Prerequisites and cost safety
- Use a dedicated Google Cloud project with MFA enabled and permission to create VPC resources.
- Review project billing, quotas, and organization policies.
- This exercise creates network configuration only; do not deploy compute or Cloud NAT resources.

## Steps

### 1. Select the lab project
1. Open the Google Cloud console and select the dedicated lab project.
2. Confirm it is not used for production or shared workloads.
3. Open **VPC network**.

### 2. Create a custom-mode VPC
1. Select **VPC networks** > **Create VPC network**.
2. Name it `network-lab`.
3. Select **Custom** subnet creation mode.
4. Add `public-subnet` with range `10.30.1.0/24` in your selected region.
5. Add `private-subnet` with range `10.30.2.0/24` in the same region.
6. Confirm the ranges do not overlap and create the network.

### 3. Review firewall rules
1. Open the VPC network's **Firewall** tab or the VPC firewall rules page.
2. Review rules applying to the new network and any inherited organization policies.
3. Do not create unrestricted ingress rules allowing all sources and protocols.
4. In a later VM lab, create narrowly scoped rules using specific targets, source ranges, protocols, and ports.

### 4. Review routes
1. Open **Routes** and filter for `network-lab`.
2. Identify the subnet routes created for the VPC.
3. Review the default internet route and its next hop, if present and applicable.
4. A default route alone does not make a VM reachable from the internet. A VM generally needs an external IP for direct internet connectivity, and firewall rules must allow the traffic.
5. A VM without an external IP can use Cloud NAT for outbound connectivity in a later lab. Do not create Cloud NAT here.

### 5. Compare subnet roles
- The public subnet is a naming convention for resources that a later lab may configure with approved external connectivity.
- The private subnet is intended for internal resources without external IP addresses.
- VPC firewall rules apply at the network level and are separate from routes.
- Do not expose SSH or RDP to all internet sources.

## Validation checklist
- [ ] VPC uses custom subnet mode.
- [ ] Both subnets exist in the selected region.
- [ ] CIDRs are `10.30.1.0/24` and `10.30.2.0/24`.
- [ ] Ranges do not overlap.
- [ ] Firewall rules have been reviewed.
- [ ] VPC routes have been reviewed.
- [ ] No VM, external IP, or Cloud NAT resource was created.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Subnet creation fails | Confirm the CIDR is valid and non-overlapping. |
| Subnet does not appear in another region | Subnets are regional even though the VPC network is global. |
| VM has no internet access | In a later VM lab, check routes, external IP or Cloud NAT, firewall rules, and guest OS configuration. |
| Traffic is blocked | Review VPC firewall rules, target tags or service accounts, priorities, and higher-level policies. |

## Cleanup
1. Confirm the VPC contains no shared or production resources.
2. Delete firewall rules created specifically for this lab, if any.
3. Delete `network-lab` and verify its subnets are removed.
Do not delete shared or production resources.

## Lessons learned
Record the difference between a global VPC, regional subnet, route, firewall rule, external IP, and Cloud NAT. Add sanitized screenshots of VPC details, subnet list, routes, and firewall review. Never include credentials or project-sensitive information.

## Official documentation
- [VPC networks overview](https://cloud.google.com/vpc/docs/vpc)
- [Create and manage VPC networks](https://cloud.google.com/vpc/docs/create-modify-vpc-networks)
- [VPC routes](https://cloud.google.com/vpc/docs/routes)
- [VPC firewall rules](https://cloud.google.com/firewall/docs/firewalls)
