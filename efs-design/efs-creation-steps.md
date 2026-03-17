📄 Elastic File System (EFS) Setup

🔹 1. Created Security Group for EFS

Navigated to VPC → Security Groups

Clicked on Create Security Group

Provided:

Name: EFS-SG-project-1

Description: secure EFS

VPC: My-Project-VPC

📌 Inbound Rule:

Type: All Traffic (Recommended: NFS - 2049 for production)

Source: VPC CIDR or EC2 Security Group

📌 Outbound Rule:

Allowed all traffic (default)

✅ Result: Security Group created for EFS access

🔹 2. Created Elastic File System (EFS)

Navigated to Amazon EFS → Create file system

Provided:

Name: EFS-Shared-Storage-Project-1

File system type: Regional (Multi-AZ for high availability)

📌 Additional Settings:

Automatic backup: Disabled

Lifecycle management:

Transition to IA: 30 days

Transition to Archive: 90 days

📌 Performance Settings:

Throughput mode: Elastic (Recommended)

✅ Result: EFS configuration defined

🔹 3. Configured Network Access (Mount Targets)
📌 Selected VPC:

My-Project-VPC

📌 Mount Targets Created:
AZ-1 (ap-south-1a)

Subnet: Private-Subnet-1A

Security Group: EFS-SG-project-1

AZ-2 (ap-south-1b)

Subnet: Private-Subnet-2B

Security Group: EFS-SG-project-1

✅ Result: EFS accessible from EC2 instances in private subnets

🔹 4. Reviewed and Created EFS

Verified all configurations

Clicked Create File System

✅ Result:
EFS successfully created and available
(File System ID: fs-082f07766256953b9)

🎯 Final Outcome

Highly available shared file storage (Multi-AZ)

Accessible from private EC2 instances

Secure via Security Group

Automatically scalable storage
