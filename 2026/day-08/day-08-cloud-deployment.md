# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment
## Part 1: Launch Cloud Instance & SSH Access
#### ✅ Step 1: Created a AWS ec2 instance 
#### ✅ Step 2: Connected via SSH 
## Part 2: Install Docker & Nginx
#### ✅ Step 1: Update system `sudo apt update`
#### ✅ Step 2: Sucessesfully installed nginx `sudo apt install nginx`
#### ✅ Verify nginx is running: `systemctl status nginx` 🟢 Running
## Part 3: Security Group Configuration
#### ✅ Added inbound roule in security group (http/https)
## Part 4: Extract Nginx Logs
#### ✅ Step 1: view nginx logs `journalctl -u nginx -n 20`
#### ✅ Step 2: save logs to file `journalctl -u nginx -n 20 > nginx-logs.txt`
#### ✅ Step 3: download log file to your local machine `scp -i docking_key.pem ubuntu@ec2-54-206-28-179.ap-southeast-2.compute.amazonaws.com:/home/ubuntu/nginx-logs.txt .`
