🟢 Step 1: Verify EC2 Web Server

Accessed EC2 instance using public IP

Verified Apache web server is running

http://<EC2-Public-IP>

👉 Web page loaded successfully

🟢 Step 2: Verify EFS Mount

Checked mounted file system:

df -h

👉 Confirmed EFS is mounted on /var/www/html

🟢 Step 3: Validate Data Persistence

Created/updated index.html inside EFS

Stopped and started EC2 instance

👉 Observation:

Data remained unchanged

Website still working

✅ Confirms EFS persistence

🟢 Step 4: Verify AMI Functionality

Launched new EC2 instance using created AMI

👉 Observation:

Apache already installed

Website already configured

EFS mount working

✅ Confirms AMI is properly configured

🟢 Step 5: Verify Auto Scaling Group

Checked Auto Scaling Group

👉 Observations:

Desired capacity maintained (2 instances)

Instances launched automatically

Instances replaced on termination

✅ Auto Scaling working correctly

🟢 Step 6: Verify Target Group Health

Navigated to Target Groups

👉 Observations:

Instances registered automatically

Health status: Healthy

✅ Load balancer can route traffic

🟢 Step 7: Verify Load Balancer (ALB)

Accessed ALB DNS:

http://<ALB-DNS>

👉 Website loaded successfully

🟢 Step 8: Test Multiple Ports
Port 80:
http://<ALB-DNS>

👉 Main application working

Port 8080:
http://<ALB-DNS>:8080

👉 Test application working

🟢 Step 9: Verify Load Balancing

Refreshed browser multiple times

👉 Observations:

Different instance hostnames displayed

Traffic distributed across instances

✅ Load balancing working correctly

🟢 Step 10: Test Fault Tolerance

Manually terminated one EC2 instance

👉 Observations:

Auto Scaling launched new instance

Target group registered new instance

Application remained accessible

✅ High availability confirmed

🎯 Final Testing Result

Web server working correctly

EFS persistence verified

AMI reusable and functional

Auto Scaling operational

Load Balancer distributing traffic

Fault tolerance achieved

✅ Conclusion

The application successfully meets the following requirements:

High Availability

Scalability

Data Persistence

Load Distribution
