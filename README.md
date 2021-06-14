### What is Cloud Computing?
- Simply put, cloud computing is the delivery of computing services including servers, storage, databases, networking, software, analytics and intelligence over the Internet (or “the cloud”).
- Benefits:
	- Flexibility
	- Efficiency
	- Strategic value


# Who is using it in the industry?
- Netflix, Amazon Prime, Spotify


### What is AWS?
- Cloud Computing Platform from Amazon (Amazon Web Services) which uses 3 main parts:
	- SaaS (Software as a Service)
	- IaaS (Infrastructure as a Service)
	- PaaS (Platform as a Service)

- Benefits:
	- Easy to Use
	- Flexible
	- Secure






### How to create an EC2 instance and deploy the node app

## EC2

- choose EC2 inside AWS
- search for Ubuntu Server 16.04 LTS (HVM), SSD Volume Type and select it (must be 64-bit (x86))
- select the t2.micro under the Type column
- click Next: Configure Instance Details
- Network: leave it as default
- Subnet: select the DevOpsStudents subnet
- Auto-assign Public IP: Enable
- click Next: Add Storage
- Choose how much storage you need and the Volume Type
- click Next: Add Tags
- Add whatever tags you'd like
- click Next: Configure Security Group
- Choose Create a new security group
- for SSH under the Source column select My IP
- Add a new rule of type HTTP and under the Source column set it to Anywhere
- click Review and Launch

## Deploy the node App

- Open AWS and a local terminal
- Select the instance you just created
- Under the SSH client column you will find informations on how to connect via SSH
- Do chmod 400 devop_bootcamp.pem (this is the key file)
- Now ssh into your VM using the ssh command provided in AWS: ssh -i "devop_bootcamp.pem" user@awsVirtualMachineLink.com
- After you managed to ssh into your VM do the following:
	- sudo apt-get update -y
	- sudo apt-get upgrade -y
	- sudo apt-get install nginx

- Now you need to exit from your VM 
- do the following:
	- scp -i ~/.ssh/devop_bootcamp.pem /home/user/app user@vmLink.com:/home/ubuntu/
- now log back in
- go inside /home/ubuntu/app
- run node app.js
- access yourIP:3000 in the browser 
