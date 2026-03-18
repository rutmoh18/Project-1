Step 1: Create Custom VPC

Navigated to VPC Dashboard

Created a custom VPC with CIDR block 192.168.0.0/24

Enabled DNS hostnames and DNS resolution

🟢 Step 2: Create Subnets

Created 4 subnets across 2 Availability Zones:

Public Subnets:

Public-Subnet-1A → 192.168.0.0/26

Public-Subnet-2B → 192.168.0.64/26

Private Subnets:

Private-Subnet-1A → 192.168.0.128/26

Private-Subnet-2B → 192.168.0.192/26

🟢 Step 3: Configure Internet Gateway

Created an Internet Gateway

Attached it to the VPC

🟢 Step 4: Configure Route Tables
Public Route Table:

Added route:

0.0.0.0/0 → Internet Gateway

Associated with public subnets

🟢 Step 5: Create NAT Gateway

Created NAT Gateway in public subnet

Allocated Elastic IP

Enabled internet access for private subnets

🟢 Step 6: Configure Private Route Table

Added route:

0.0.0.0/0 → NAT Gateway

Associated with private subnets

🟢 Step 7: Launch EC2 Instance

Service: Amazon EC2

Launched EC2 instance in public subnet

Connected via SSH

Installed Apache web server

sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
🟢 Step 8: Create and Configure EFS

Service: Amazon EFS

Created EFS file system

Configured mount targets in private subnets

Created security group for EFS

🟢 Step 9: Mount EFS on EC2
sudo yum install -y amazon-efs-utils
sudo mkdir /var/www/html
sudo mount -t efs <efs-id>:/ /var/www/html

Verified mount using df -h

Configured auto-mount using /etc/fstab

🟢 Step 10: Deploy Web Application

Created index.html inside EFS

sudo vi /var/www/html/index.html

Added custom web content

🟢 Step 11: Create AMI

Created AMI from configured EC2 instance

Used as golden image for scaling

🟢 Step 12: Create Launch Template

Created launch template using AMI

Selected instance type and security group

🟢 Step 13: Create Target Groups

Service: Elastic Load Balancing

Created two target groups:

Web-App → Port 80

Test-App → Port 8080

🟢 Step 14: Create Application Load Balancer

Created ALB (Internet-facing)

Selected multiple Availability Zones

Attached security group

🟢 Step 15: Configure Listeners

Port 80 → Forward to Web-App

Port 8080 → Forward to Test-App

🟢 Step 16: Create Auto Scaling Group

Service: AWS Auto Scaling

Used launch template

Attached target groups

Configured:

Desired: 2

Min: 0

Max: 5

🟢 Step 17: Configure Security Groups

ALB-SG:

Allow HTTP (80) from internet

Allow 8080 from specific IP

Web-Server-SG:

Allow traffic only from ALB-SG

EFS-SG:

Allow NFS (2049) only from Web-Server-SG

🟢 Step 18: Test Application

Accessed application via ALB DNS

Verified:

Port 80 → Web app

Port 8080 → Test app

Confirmed load balancing and scaling

✅ Final Result

Fully functional scalable architecture

Load balanced application

Auto scaling enabled

Secure communication between services

Shared storage using EFS
