
🔹 1. Created Custom VPC

Navigated to VPC Dashboard

Clicked on Create VPC

Selected VPC only

Provided following configuration:

Name: My-Project-VPC

IPv4 CIDR Block: 192.168.0.0/24

Tenancy: Default

Clicked on Create VPC

✅ Result: VPC successfully created


🔹 2. Created Subnets (Public & Private)

Created 4 subnets across 2 Availability Zones for high availability:

📌 Public Subnets

Public-Subnet-1A → 192.168.0.0/26

Public-Subnet-2B → 192.168.0.64/26

📌 Private Subnets

Private-Subnet-1A → 192.168.0.128/26

Private-Subnet-2B → 192.168.0.192/26

✅ Result: Subnets created successfully across multiple AZs

🔹 3. Created and Attached Internet Gateway

Navigated to Internet Gateways

Clicked Create Internet Gateway

Name: Internet-Gateway-For-Project-1

Attached IGW to My-Project-VPC

✅ Result: Internet Gateway attached to VPC

🔹 4. Created Route Table for Public Subnets

Created new route table: Route-Table-For-Public

Added route:

0.0.0.0/0 → Internet Gateway (IGW)

Associated with:

Public-Subnet-1A

Public-Subnet-2B

✅ Result: Public subnets now have internet access

🔹 5. Created NAT Gateway (for Private Subnets)

Allocated Elastic IP

Created NAT Gateway in:

Public-Subnet-1A

Attached Elastic IP to NAT Gateway

✅ Result: NAT Gateway created successfully

🔹 6. Configured Route Table for Private Subnets

Used Main Route Table (or updated it)

Added route:

0.0.0.0/0 → NAT Gateway

Associated with:

Private-Subnet-1A

Private-Subnet-2B

✅ Result: Private subnets can access internet securely via NAT

🎯 Final Architecture Outcome

Custom VPC with CIDR 192.168.0.0/24

2 Public + 2 Private Subnets (Multi-AZ)

Internet Gateway for public access

NAT Gateway for private subnet outbound access

Proper route table configuration
