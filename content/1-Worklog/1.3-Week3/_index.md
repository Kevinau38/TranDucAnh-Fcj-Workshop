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
* Master Internet Gateway and NAT Gateway.
* Practice VPC configuration and subnets.
* Understand network security best practices.
* Hands-on: Build multi-tier network architecture.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn VPC fundamentals and concepts. <br> - Understand CIDR blocks and IP addressing. <br> - Learn about subnets (public vs private). <br> - Study route tables and routing.                                                                      | 26/01/2026 | 26/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html>           |
| 3   | - Learn Security Groups concepts. <br> - Understand Network ACLs (NACLs). <br> - Compare Security Groups vs NACLs. <br> - Study stateful vs stateless filtering.                                               | 27/01/2026 | 27/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html> |
| 4   | - Learn Internet Gateway concepts. <br> - Understand NAT Gateway and NAT Instance. <br> - Study public vs private subnet routing. <br> - Learn about Elastic IPs.                                                    | 28/01/2026 | 28/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html> |
| 5   | - **Practice:** VPC setup and configuration: <br>   + Create custom VPC with CIDR block. <br>   + Create public and private subnets. <br>   + Configure route tables. <br>   + Set up Internet Gateway. <br>   + Configure NAT Gateway. <br>   + Test connectivity between subnets.                                 | 29/01/2026 | 29/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-getting-started.html> |
| 6   | - **Hands-on Project:** Build multi-tier network architecture: <br>   + Design 3-tier architecture (web, app, database). <br>   + Create VPC with multiple subnets across AZs. <br>   + Configure public subnets for web tier. <br>   + Configure private subnets for app and database tiers. <br>   + Set up Internet Gateway for public access. <br>   + Configure NAT Gateway for private subnet internet access. <br>   + Create and configure Security Groups for each tier. <br>   + Set up Network ACLs for additional security. <br>   + Deploy EC2 instances in each tier. <br>   + Test end-to-end connectivity and security.                                  | 30/01/2026 | 30/01/2026      |  |


### Week 3 Achievements:

* **Understood AWS VPC networking concepts:**
  * Learned VPC architecture and components.
  * Understood CIDR blocks and IP addressing schemes.
  * Learned public and private subnet configurations.
  * Understood route tables and routing mechanisms.
  * Learned about VPC peering and connectivity options.

* **Gained expertise in network security:**
  * Understood Security Groups and their stateful nature.
  * Learned Network ACLs and stateless filtering.
  * Understood differences between Security Groups and NACLs.
  * Implemented layered security approach.
  * Configured inbound and outbound rules effectively.

* **Successfully configured Internet connectivity:**
  * Set up Internet Gateway for public subnet access.
  * Configured NAT Gateway for private subnet internet access.
  * Understood Elastic IP allocation and management.
  * Learned routing for internet-bound traffic.
  * Implemented secure internet connectivity patterns.

* **Built multi-tier network architecture:**
  * Designed and implemented 3-tier architecture.
  * Created VPC with multiple subnets across availability zones.
  * Configured web tier in public subnets with internet access.
  * Set up app and database tiers in private subnets.
  * Implemented proper security group rules for each tier.
  * Configured Network ACLs for additional security layer.
  * Deployed and tested EC2 instances in each tier.
  * Verified end-to-end connectivity and security isolation.
  * Implemented high availability and fault tolerance.

* **Developed foundational AWS networking skills** including VPC design, subnet planning, security configuration, and multi-tier architecture implementation.
