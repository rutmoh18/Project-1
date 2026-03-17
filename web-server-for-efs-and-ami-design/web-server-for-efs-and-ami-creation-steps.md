🚀 AWS EC2 + EFS Web Server Setup (Step-by-Step)
🟢 Step 1: Launch EC2 Instance

Service: Amazon EC2

Selected AMI: Amazon Linux 2023

Instance type: t2.micro (Free tier eligible)

Created/selected a key pair

Network configuration:

VPC: Custom VPC

Subnet: Public Subnet

Auto-assign Public IP: Enabled

Security Group:

Allow SSH (Port 22)

Allow HTTP (Port 80)

👉 Instance successfully launched and in Running state

🟢 Step 2: Connect to EC2 (SSH)
ssh -i Web-Server-For-EFS-And-Ami.pem ec2-user@<Public-IP>

👉 Connected successfully to the instance

🟢 Step 3: Install Apache Web Server
sudo yum install httpd -y

Start and enable Apache:

sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd

👉 Apache is active and running

🟢 Step 4: Install EFS Utilities

Service: Amazon EFS

sudo yum install amazon-efs-utils -y

👉 Required package installed to mount EFS

🟢 Step 5: Mount EFS to EC2 (IMPORTANT 🔥)
✅ 1. Create Mount Directory (if not exists)
sudo mkdir -p /var/www/html
✅ 2. Mount EFS File System
sudo mount -t efs -o tls fs-082f07766256953b9:/ /var/www/html/

👉 Explanation:

fs-082f07766256953b9 → Your EFS File System ID

/var/www/html → Apache web root directory

-o tls → Secure encrypted connection

✅ 3. Verify Mount
df -h

👉 You should see EFS mounted on /var/www/html

🟢 Step 6: Make Mount Permanent (Auto Mount after Restart)

Edit fstab file:

sudo vi /etc/fstab

Add this line:

fs-082f07766256953b9.efs.ap-south-1.amazonaws.com:/ /var/www/html efs defaults,_netdev 0 0

👉 This ensures:

EFS automatically mounts after reboot

🟢 Step 7: Create Website
cd /var/www/html
sudo vi index.html

👉 Add your HTML code (custom UI)

🟢 Step 8: Access Website

Open browser:

http://<Public-IP>

👉 Output:

“Welcome to Ritik Capstone Project 1”

Website loads successfully

🟢 Step 9: Testing Persistence

Stopped the EC2 instance

Started it again

👉 Observations:

Public IP changed

Website still working

✅ Because data is stored in EFS (persistent storage)

🎯 Architecture Flow
User → Browser → EC2 (Apache Web Server)
                      ↓
                 Amazon EFS (Storage)
💡 Key Points (Interview Ready)

EFS is a scalable shared file system

Multiple EC2 instances can access the same EFS

Data persists independently of EC2 lifecycle

Apache serves static content from EFS-mounted directory

Used /etc/fstab for automatic mounting

🔥 Final Result

✔ EC2 instance created
✔ Apache installed and running
✔ EFS mounted successfully
✔ Website deployed
✔ Persistent storage verified
