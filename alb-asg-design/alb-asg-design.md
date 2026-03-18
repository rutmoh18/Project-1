🟢 Step 1: Create Launch Template

Service: Amazon EC2

Navigated to:

EC2 → Launch Templates → Create launch template

Selected:

AMI (created earlier)

Instance type: t2.micro

Attached Security Group

Created Launch Template:

Launch-Template-Project-1
🟢 Step 2: Create Target Groups


🔹 Target Group 1

Name: Web-App

Protocol: HTTP

Port: 80

Target type: Instance

🔹 Target Group 2

Name: Test-App

Protocol: HTTP

Port: 8080

Target type: Instance

🟢 Step 3: Create Security Group for ALB

Created Security Group:

ALB-SG

Inbound rules:

HTTP (80)

Custom TCP (8080)

(Currently allowed all traffic)

🟢 Step 4: Create Application Load Balancer

Navigated to:

EC2 → Load Balancers → Create Load Balancer

Selected:

Type: Application Load Balancer

Scheme: Internet-facing

Selected:

2 Availability Zones

Attached:

ALB-SG

🟢 Step 5: Configure Listeners

Listener 1:

HTTP : 80 → Forward to Web-App

Listener 2:

HTTP : 8080 → Forward to Test-App

🟢 Step 6: Create Auto Scaling Group

Service: AWS Auto Scaling

Navigated to:

EC2 → Auto Scaling Groups → Create Auto Scaling Group

Selected:

Launch Template: Launch-Template-Project-1

Attached:

Target Groups:

Web-App

Test-App

Configured capacity:

Desired: 2

Min: 0

Max: 5

🟢 Step 7: Verify Instances

Auto Scaling launched 2 instances

Instances automatically registered in:

Web-App (port 80)

Test-App (port 8080)

Health status:

✅ Healthy

🟢 Step 8: Test Load Balancer

Opened ALB DNS in browser

Port 80:
http://<ALB-DNS>

👉 Displayed main website

Port 8080:
http://<ALB-DNS>:8080

👉 Displayed CPU load application

🟢 Step 9: Verify Load Balancing

Refreshed multiple times

Observed different hostnames

👉 Traffic distributed across instances

✅ Final Output

ALB successfully routing traffic

Auto Scaling managing instances

Target groups healthy

Application accessible on multiple ports
