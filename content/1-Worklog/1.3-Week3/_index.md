---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
### Week 3 Objectives:

* Learn AWS VPC and networking concepts.
* Understand Security Groups and Network ACLs.
* Understand Internet Gateway and NAT Gateway.
* Practice VPC configuration and subnets.
* Understand network security best practices.
* Hands-on: Build multi-tier network architecture.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn VPC fundamentals and concepts. <br> - Understand CIDR blocks and IP addressing. <br> - Learn about subnets (public vs private). <br> - Study route tables and routing.                                                                      | 26/01/2026 | 26/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-cidr-blocks.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html>           |
| 3   | - Learn Security Groups concepts. <br> - Understand Network ACLs (NACLs). <br> - Compare Security Groups vs NACLs. <br> - Study stateful vs stateless filtering.                                               | 27/01/2026 | 27/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html> <br> <https://tutorialsdojo.com/understanding-security-groups-and-network-access-control-lists-nacls-in-aws/> <br> <https://medium.com/@subhampradhan966/aws-security-groups-and-network-access-control-lists-nacls-4add51916150> |
| 4   | - Learn Internet Gateway concepts. <br> - Understand NAT Gateway and NAT Instance. <br> - Study public vs private subnet routing. <br> - Learn about Elastic IPs.                                                    | 28/01/2026 | 28/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/route-table-options.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-eip-overview.html> |
| 5   | - **Practice:** Create basic VPC infrastructure: <br>   + Create custom VPC with CIDR block (10.0.0.0/16). <br>   + Create public subnet for web tier. <br>   + Create private subnet for app tier. <br>   + Configure route tables for each subnet. <br>   + Set up Internet Gateway and attach to VPC. <br>   + Configure NAT Gateway in public subnet. <br>   + Test basic connectivity.                                 | 29/01/2026 | 29/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html> |
| 6   | - **Hands-on Project:** Expand to multi-tier network architecture: <br>   + Add database subnet to existing VPC. <br>   + Configure subnets across 2 Availability Zones. <br>   + Create Security Groups for web, app, and database tiers. <br>   + Configure Security Group rules (web → app → database). <br>   + Deploy EC2 instances in web tier (public subnet). <br>   + Deploy EC2 instances in app tier (private subnet). <br>   + Test connectivity between tiers. <br>   + Verify security isolation and internet access.                                  | 30/01/2026 | 30/01/2026      |  |


### Week 3 Achievements:

* **Understood AWS VPC networking concepts:**
  * Learned VPC architecture and components.
  * Understood CIDR blocks and IP addressing schemes.
  * Learned public and private subnet configurations.
  * Understood route tables and routing mechanisms.

* **Gained expertise in network security:**
  * Understood Security Groups and their stateful nature.
  * Learned Network ACLs and stateless filtering.
  * Understood differences between Security Groups and NACLs.
  * Implemented layered security approach.
  * Configured inbound and outbound rules effectively.

* **Successfully created basic VPC infrastructure:**
  * Created custom VPC with CIDR block 10.0.0.0/16.
  * Configured public subnet for web tier.
  * Configured private subnet for app tier.
  * Set up Internet Gateway and attached to VPC.
  * Configured NAT Gateway in public subnet for private subnet internet access.
  * Configured route tables for proper traffic routing.
  * Tested basic connectivity between subnets.

* **Expanded VPC to multi-tier network architecture:**
  * Added database subnet to existing VPC infrastructure.
  * Configured subnets across 2 Availability Zones for high availability.
  * Created Security Groups for web, app, and database tiers.
  * Configured Security Group rules for tier-to-tier communication (web → app → database).
  * Deployed EC2 instances in web tier (public subnet).
  * Deployed EC2 instances in app tier (private subnet).
  * Tested connectivity between tiers.
  * Verified security isolation and proper internet access.
  * Implemented multi-tier architecture with proper network segmentation.

* **Developed foundational AWS networking skills** including VPC design, subnet planning, security configuration, and multi-tier architecture implementation.
