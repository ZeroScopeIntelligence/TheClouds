# Lab 01: Build an Azure Virtual Network with Public and Private Subnets

## Objective
Create an Azure Virtual Network (VNet) with two non-overlapping subnets, apply Network Security Groups (NSGs), and understand Azure routing and public connectivity.

## Concepts
- **VNet:** A logically isolated network in Azure.
- **CIDR:** Notation describing an IP address range.
- **Subnet:** A smaller address range inside a VNet.
- **NSG:** Stateful security rules that allow or deny inbound and outbound traffic.
- **Route table:** User-defined routes that can direct traffic through a next hop.
- **Public IP:** An address assigned to a resource or network interface to provide configured external connectivity.

> Azure does not make a subnet public merely by naming it “public.” Public reachability depends on public IP configuration, NSG rules, routing, and services such as NAT Gateway or Azure Firewall.

## Topology and addressing

| Component | Name | IPv4 range |
| --- | --- | --- |
| Resource group | rg-zs-network-lab | Selected region |
| VNet | vnet-zs-network-lab | 10.20.0.0/16 |
| Front-end subnet | snet-public | 10.20.1.0/24 |
| Private subnet | snet-private | 10.20.2.0/24 |
| NSG | nsg-zs-public | Associate with snet-public |
| NSG | nsg-zs-private | Associate with snet-private |

The labels public and private describe the intended design, not an automatic Azure subnet property. No VMs or public IP addresses are required.

## Prerequisites and cost safety
- Use a dedicated Azure learning subscription with MFA enabled and permission to create networking resources.
- Review subscription pricing and quotas. This exercise creates networking configuration only; do not deploy VMs, NAT Gateway, or other billable services.

## Steps

### 1. Create a resource group
1. In the Azure portal, open **Resource groups** > **Create**.
2. Name it `rg-zs-network-lab`.
3. Select an available region and create it.

### 2. Create the VNet and subnets
1. Open **Virtual networks** > **Create**.
2. Select `rg-zs-network-lab` and the same region.
3. Name the VNet `vnet-zs-network-lab`.
4. Set IPv4 address space to `10.20.0.0/16`.
5. Add `snet-public` with `10.20.1.0/24`.
6. Add `snet-private` with `10.20.2.0/24`.
7. Confirm the ranges are within the VNet and do not overlap, then create the VNet.

### 3. Create and associate the front-end NSG
1. Open **Network security groups** > **Create**.
2. Name it `nsg-zs-public` in the same resource group and region.
3. Review default inbound and outbound rules.
4. Do not add broad inbound allow rules. For this configuration-only lab, retain the default inbound protections.
5. Associate the NSG with `snet-public` using the NSG's **Subnets** page or subnet configuration.

### 4. Create and associate the private NSG
1. Create `nsg-zs-private`.
2. Review its default rules and associate it with `snet-private`.
3. Note how NSG rules are evaluated by priority and how stateful connections are handled.

### 5. Inspect routing
1. Open the VNet and review **Subnets**.
2. Confirm both subnet ranges and NSG associations.
3. Azure automatically provides system routes, including routes for traffic within the VNet.
4. A custom route table is not required for this lab. Later, user-defined routes can direct traffic through Azure Firewall or a network virtual appliance.
5. Do not assign public IP addresses or deploy NAT Gateway for this exercise.

### 6. Compare subnet roles
- The front-end subnet is reserved for a future, separately secured entry point such as an application gateway or load balancer.
- The private subnet is intended for internal workloads without direct public IP assignments.
- NSGs filter traffic; they do not by themselves create a public or private subnet.
- Avoid inbound management access from the entire internet.

## Validation checklist
- [ ] Resource group is `rg-zs-network-lab`.
- [ ] VNet address space is `10.20.0.0/16`.
- [ ] Both subnets exist and do not overlap.
- [ ] Each subnet has the intended NSG association.
- [ ] No broad inbound allow rule has been added.
- [ ] No VM, public IP, or NAT Gateway was deployed.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Address range rejected | Confirm subnet CIDR is inside the VNet range and does not overlap. |
| NSG association fails | Verify resource subscription, region, and subnet association settings. |
| Traffic unexpectedly allowed or denied | Review NSG priority, direction, source, destination, protocol, and default rules. |
| Route differs from expectation | Review system routes and any associated user-defined route table. |

## Cleanup
1. Confirm `rg-zs-network-lab` contains only resources created for this exercise.
2. Delete the resource group and wait for deletion to complete.
3. Verify the subscription resource list contains no remaining lab resources.
Do not delete shared or production resources.

## Lessons learned
Record the difference between a VNet, subnet, NSG, route table, and public IP. Add sanitized screenshots of the address space, subnet list, and NSG associations. Never include credentials or subscription-sensitive information.

## Official documentation
- [Create a virtual network](https://learn.microsoft.com/azure/virtual-network/quick-create-portal)
- [Virtual network concepts](https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview)
- [Network security groups](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview)
- [Azure virtual network traffic routing](https://learn.microsoft.com/azure/virtual-network/virtual-networks-udr-overview)
