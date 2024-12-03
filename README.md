# VPC-Peering
How to Connect Instances in Different Private Networks (VPCs) Using VPC Peering

## Project Description
This project demonstrates how to establish communication between EC2 instances located in different Virtual Private Clouds (VPCs) using VPC Peering. It walks through the process of setting up two VPCs in AWS, configuring subnets, routing tables, and security groups to enable seamless connectivity between instances while maintaining secure and isolated networks.

![image alt]( https://github.com/ris21/VPC-Peering/blob/4732366a7a60a9e8d35c262523ce5ac8ace8a4c2/VPC%20Peering%20Network%20Toplogy.png)

### Skills gained
- VPC creation
- CIDR block planning
- Route propagation
- Security group configurations
  
## Project Steps
### 1. Two VPCs were crea ted:
-	VPC-A: Configured with the IPv4 CIDR block 10.0.0.0/16 and named VPC-A. Default settings were used, and a tag Key=Name, Value=VPC-A was added.
-	VPC-B: Configured with the IPv4 CIDR block 20.0.0.0/16 and named VPC-B. Default settings were used, and a tag Key=Name, Value=VPC-B was added.
### 2. Two subnets were created:
-	Subnet-1: Associated with VPC-A, named my-subnet-VPC-A-private, and configured with the CIDR block 10.0.0.0/24.
-	Subnet-2: Associated with VPC-B, named my-subnet-VPC-B-public, and configured with the CIDR block 20.0.0.0/24.
### 3. An Internet Gateway was created and attached to VPC-B.
### 4.Two route tables were created and configured:
-	Route Table for VPC-A: Named VPC-A-PrivateRoute, associated with Subnet-1 (my-subnet-VPC-A-private).
-	Route Table for VPC-B: Named VPC-B-PublicRoute, with a route added for 0.0.0.0/0 targeting the Internet Gateway. It was associated with Subnet-2 (my-subnet-VPC-B-public).
### 4. Two security groups were created:
-	Security Group for VPC-A: Named SSHAccess, associated with VPC-A, and configured to allow inbound SSH traffic.
-	Security Group for VPC-B: Named SSHAccess, associated with VPC-B, and configured to allow inbound SSH traffic.
### 5. Two EC2 instances were launched:

-	Instance in VPC-A: Deployed in the private subnet (my-subnet-VPC-A-private) with the t2.micro instance type, public IP disabled, and the associated SSHAccess security group.
-	Bastion Instance in VPC-B: Deployed in the public subnet (my-subnet-VPC-B-public) with the t2.micro instance type, public IP enabled, and the associated SSHAccess security group.
### 6. A VPC Peering connection was created and accepted:
-	The connection linked VPC-A (requestor) and VPC-B (accepter). Once the connection was established, it was accepted in the VPC Peering console.
### 7. Route tables were updated to enable communication via the peering connection:
-	In the route table for VPC-A, a route was added with the destination set to the CIDR block of VPC-B and the target set to the peering connection.
-	In the route table for VPC-B, two routes were added: one for the CIDR block of VPC-A (targeting the peering connection) and another for 0.0.0.0/0 (targeting the Internet Gateway).
