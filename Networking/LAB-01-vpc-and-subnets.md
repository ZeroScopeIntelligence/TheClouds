# Lab 01: Build an AWS VPC with Public and Private Subnets

## Objective
Create an isolated Amazon VPC, divide it into public and private subnets, and configure routing so only the public subnet has a direct route to the internet.

## Concepts
- **VPC:** A logically isolated network in AWS.
- **CIDR:** Notation describing an IP address range.
- **Subnet:** A range of IP addresses inside a VPC, associated with one Availability Zone.
- **Route table:** Rules that determine where subnet traffic is sent.
- **Internet gateway (IGW):** Enables internet connectivity for appropriately addressed and secured resources.
- **Security group:** A stateful virtual firewall associated with network interfaces or resources.

## Topology and addressing

| Component | Name | IPv4 range / route |
| --- | --- | --- |
| VPC | network-lab | 10.10.0.0/16 |
| Public subnet | public-subnet | 10.10.1.0/24 |
| Private subnet | private-subnet | 10.10.2.0/24 |
| Public route table | public-rt | VPC local route; 0.0.0.0/0 to IGW |
| Private route table | private-rt | VPC local route only |

AWS reserves five IPv4 addresses in each subnet, so the usable host count is lower than the total address count.

## Prerequisites and cost safety
- Use a dedicated AWS learning account with MFA enabled and permission to create VPC resources.
- Review current pricing. This configuration-only lab does not require EC2, NAT Gateway, or public IPv4 addresses; avoid creating them.
- Never expose SSH or RDP to 0.0.0.0/0.

## Steps

### 1. Create the VPC
1. Open **VPC** in the AWS Management Console, then **Your VPCs** > **Create VPC**.
2. Choose **VPC only**.
3. Name it `network-lab` and set IPv4 CIDR to `10.10.0.0/16`.
4. Keep IPv6 disabled for this introductory exercise and create the VPC.

### 2. Create the subnets
1. Open **Subnets** > **Create subnet** and select `network-lab`.
2. Create `public-subnet` with `10.10.1.0/24`.
3. Create `private-subnet` with `10.10.2.0/24`.
4. Select an Availability Zone for each. Confirm both ranges are inside the VPC and do not overlap.

### 3. Create and attach an internet gateway
1. Open **Internet gateways** > **Create internet gateway**.
2. Name it `network-lab-igw`.
3. Select it and choose **Attach to a VPC**.
4. Attach it to `network-lab`.

### 4. Configure the public route table
1. Create a route table named `public-rt` in `network-lab`.
2. Add route `0.0.0.0/0` with the internet gateway as its target.
3. Associate the route table with `public-subnet`.
4. Confirm the VPC-local route remains present.

### 5. Configure the private route table
1. Create `private-rt` in `network-lab`.
2. Associate it with `private-subnet`.
3. Leave the VPC-local route in place. Do not add a default route to the IGW or create a NAT gateway.

### 6. Understand the result
- A subnet is considered public when its associated route table has a route to an internet gateway.
- A subnet without a direct IGW route is private in this lab.
- An IGW route alone does not make an instance reachable. A resource also needs suitable public addressing and security controls.
- Security groups and network ACLs are separate controls and will be explored in a later lab.

## Validation checklist
- [ ] VPC CIDR is `10.10.0.0/16`.
- [ ] Both subnets are inside the VPC and do not overlap.
- [ ] IGW is attached to the VPC.
- [ ] Public subnet route table has `0.0.0.0/0` pointing to the IGW.
- [ ] Private subnet has no direct IGW default route.
- [ ] Each subnet is associated with the intended route table.

## Troubleshooting

| Symptom | Check |
| --- | --- |
| Subnet CIDR rejected | Ensure it is within the VPC range and does not overlap another subnet. |
| Public subnet has no internet route | Confirm IGW attachment and route-table association. |
| Resource is not reachable | Review public IP assignment, security groups, network ACLs, and the resource service. |
| Private subnet unexpectedly has internet access | Review its route table and any other connectivity components. |

## Cleanup
1. Disassociate subnets from custom route tables, then delete the custom route tables.
2. Detach and delete the internet gateway.
3. Delete both subnets.
4. Delete the VPC.
5. Confirm no lab-created resources remain. Delete only resources created for this lab.

## Lessons learned
Record the difference between a VPC, subnet, route table, IGW, and security group. Add sanitized screenshots of the VPC resource map and route tables. Never include credentials or account-sensitive information.

## Official documentation
- [Create a VPC](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html)
- [VPC subnet basics](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html)
- [Route tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- [Internet gateways](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)
