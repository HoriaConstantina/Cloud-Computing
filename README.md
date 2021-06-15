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
	- sudo apt-get install python-software-properties
	- curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
	- sudo apt-get install nodejs -y
	- sudo npm install pm2 -g

- Now you need to exit from your VM 
- do the following:
	- scp -i ~/.ssh/devop_bootcamp.pem -r /home/user/app user@vmLink.com:/home/ubuntu/
- now log back in
- go inside /home/ubuntu/app
- run node app.js
- access yourIP:3000 in the browser 


### Creating the DB EC2 Instance

- choose EC2 inside AWS
- search for Ubuntu Server 16.04 LTS (HVM), SSD Volume Type and select it (must>
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
- Add a new rule of type Custom TCP and under the Source column set it to your app instance IP (your.app.instance.ip/32)
- click Review and Launch
- select the devop_bootcamp.pem file and you are ready to Launch

## After the DB Instance was created
- scp -i ~/.ssh/devop_bootcamp.pem -r /home/user/app user@vmLink.com:/home/ubuntu/
- Now ssh into your VM using the ssh command provided in AWS: ssh -i "devop_bootcamp.pem user@awsVirtualMachineLink.com
- Once you are inside your db instance do the following:
	- cd mongoDB/db/
	- sudo ./provision.sh (in case it is not working do: chmod +x provision.sh)

## After you have both instances up and running
- ssh into your app instance
- cd ~
- sudo nano .bashrc
- at the end of the file type: export DB_HOST://your.db.instance.ip:27017/posts", save and exit
- source .bashrc
- sudo nano /etc/profile
- at the end of the file type: DB_HOST://your.db.instance.ip:27017/posts", save and exit
- cd /home/ubuntu/app/seeds
- node seed.js
- wait until you see "Database Seeded, Databases Cleared"
- cd /home/ubuntu/app
- npm start or node app.js
- access your app ip in your browser
