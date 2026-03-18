🟢 Step 1: Configure Security Group for Load Balancer (ALB-SG)

Navigated to:

EC2 → Security Groups → ALB-SG → Edit inbound rules

Added inbound rules:

Rule 1:

Type: HTTP

Port: 80

Source: 0.0.0.0/0

👉 Allows public access to web application

Rule 2:

Type: Custom TCP

Port: 8080

Source: My IP

👉 Allows restricted access to testing application

🟢 Step 2: Configure Security Group for Web Server (Web-Server-SG)

Navigated to:

EC2 → Security Groups → Web-Server-SG → Edit inbound rules

Added inbound rules:

Rule 1:

Type: HTTP

Port: 80

Source: ALB-SG

Rule 2:

Type: Custom TCP

Port: 8080

Source: ALB-SG

👉 Only ALB can send traffic to EC2 instances

🟢 Step 3: Configure Security Group for EFS (EFS-SG-project-1)

Navigated to:

EC2 → Security Groups → EFS-SG-project-1 → Edit inbound rules

Added inbound rule:

Rule:

Type: NFS

Port: 2049

Source: Web-Server-SG

👉 Only EC2 instances can access EFS

🟢 Step 4: Verify Security Group Flow

ALB-SG allows traffic from internet

Web-Server-SG allows traffic only from ALB-SG

EFS-SG allows traffic only from Web-Server-SG

🔐 Final Security Flow
User → ALB (ALB-SG) → EC2 (Web-Server-SG) → EFS (EFS-SG)
✅ Result

Public users can access application via ALB

EC2 instances are not directly exposed to internet

EFS is securely accessible only from EC2

Architecture is secured using security group chaining
