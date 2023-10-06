# Scenario Based Interview Questions on EC2, IAM and VPC

## VPC Architecture Design

**Q:** You have been assigned to design a VPC architecture for a 2-tier application. The application needs to be highly available and scalable. How would you design the VPC architecture?

**A:** In this scenario, I would design a VPC architecture in the following way:
   - Create 2 subnets: public and private.
   - The public subnet would contain the load balancers and be accessible from the internet.
   - The private subnet would host the application servers.
   - Distribute the subnets across multiple Availability Zones for high availability.
   - Configure auto scaling groups for the application servers.

## Outbound Internet Access Control

**Q:** Your organization has a VPC with multiple subnets. You want to restrict outbound internet access for resources in one subnet, but allow outbound internet access for resources in another subnet. How would you achieve this?

**A:** To restrict outbound internet access for resources in one subnet, we can modify the route table associated with that subnet by removing the default route (0.0.0.0/0) pointing to an internet gateway. For the subnet requiring outbound internet access, retain the default route pointing to the internet gateway.

## Enabling Internet Access for Private Subnet

**Q:** You have a VPC with a public subnet and a private subnet. Instances in the private subnet need to access the internet for software updates. How would you allow internet access for instances in the private subnet?

**A:** To allow internet access for instances in the private subnet, you can use a NAT Gateway or a NAT instance. Place the NAT Gateway/instance in the public subnet and configure the private subnet's route table to send outbound traffic to the NAT Gateway/instance.

## Private IP Communication

**Q:** You have launched EC2 instances in your VPC, and you want them to communicate with each other using private IP addresses. What steps would you take to enable this communication?

**A:** Instances within the same VPC can communicate with each other using private IP addresses by default. Ensure instances are in the same VPC and subnet or connected through peering. Verify security group settings for proper communication.

## Network Access Control

**Q:** You want to implement strict network access control for your VPC resources. How would you achieve this?

**A:** Implement granular network access control for VPC resources using Network Access Control Lists (NACLs). Define inbound and outbound rules in NACLs based on source/destination IP, ports, and protocols to control traffic at the subnet level.

## Isolated Environment in VPC

**Q:** Your organization requires an isolated environment within the VPC for running sensitive workloads. How would you set up this isolated environment?

**A:** Create an isolated subnet within the VPC by not attaching an internet gateway. Place sensitive workloads in this subnet to protect them from inbound and outbound internet traffic. If outbound internet access is needed, use a NAT Gateway/instance in a different subnet.

## Secure Access to AWS Services in VPC

**Q:** Your application needs to access AWS services, such as S3 securely within your VPC. How would you achieve this?

**A:** Securely access AWS services within the VPC using VPC endpoints. Create VPC endpoints for specific AWS services (e.g., S3, DynamoDB) and associate them with the VPC, allowing secure communication between VPC instances and AWS services.

## IAM Concepts

**Q:** What is the difference between IAM users, groups, roles, and policies?

**A:** 
- IAM User: Represents an individual or application needing AWS access. Has long-term credentials (username/password or access keys).
- IAM Role: Assumed by entities to obtain temporary credentials. Useful for granting permissions to external entities or cross-account access.
- IAM Group: Collection of IAM users for simplified permission management.
- IAM Policy: Document defining permissions and access controls in AWS.

## Bastion Host Setup

**Q:** You have a private subnet in your VPC containing instances that should not have direct internet access. However, you still need to securely access these instances for administrative purposes. How would you set up a bastion host to facilitate this access?

**A:** To securely access instances in the private subnet:
   - Create a bastion host in a public subnet.
   - Configure its security group for SSH (or RDP) access from trusted IPs.
   - Place instances in the private subnet, allowing SSH (or RDP) access from the bastion host's security group.
   - Connect to the bastion host, then access private subnet instances using their private IPs.

