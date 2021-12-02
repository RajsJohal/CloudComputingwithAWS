### Cloud Computing

## What is Cloud Computing
Cloud computing is the on demand delivery of IT resources over the internet with pay as you go pricing. Rather than buying, owning and maintaining physical data centers adn servers, you can access technology services, such as computing power, storage, and databses on an as needed basis from a cloud provider such as AWS.

**Benefits**
- Agility
- Elasticity
- Cost Savings
- Deploy Globally in Minutes

**Who uses Cloud Computing**
Organizations of every type, size and industry use the cloud for varying use cases such as data backup, disaster recovery, email, virtual desktops, software development and testing, big data analytics, and customer-facing web applications. 

E.g. Healthcare companies are using the cloud to develop more personalized treatments for patients. Financial services companies are using the cloud to power real time fraud detection and prevention. And video game makeers are using the cloud to deliver online games to millions of players around the world.

**Types of Cloud Computing**
- Infrastructure as a Service (IaaS)
Contains the basic building blocks for cloud IT. Provides access to networking features, computers and data storage space. IaaS delivers the highest level of flxibility and management control over your IT resources.

- Platform as a Service (PaaS)
Removes the need for you to manage underlying infrastructure (hardware and OS), and allows you to focus on the deployment and management of your applications. This helps you be more efficient as you dont need to worry about resource procurement, capacity planning, software maintenance, patching or any of the other undifferentiated heavy lifting involved in running your application.

- Software as a Service (SaaS)
Provides you with a complete product that is run and managed by the service provider. You dont have to think about how the service is maintained or how the underlying infrastructure is managed. You only need to think about how you will use that particular software.

**What is AWS?**
Amazon Web Service is the world's most comprehensive and broadly adopted cloud platform, offering over 200 fully featured services from data centers globally. Millions of customers - including the fastest growing startups, largest enterprises and leading government agencies are using AWS to lower costs, become more agile and innovate faster.

**Benefits of AWS**
- Most Functionality
- Largest Community of Customers and Partners
- Most Secure
- Fastest Pace of Innovation
- Most Proven Operational Expertise
- Global Network of AWS Regions with Availability Zones

## Creating an EC2 Instance
- Login to AWS Management Console with Sparta Global credentials
- Navigate to EC2 and launch an instance
- Once an instance of EC2 has been launched, open a Git Bash terminal and set up an ssh directory with the .pem encryption key 
- Connect to the instance from the terminal by running an ssh command and running the ubuntu version setup with the instance.
- Git clone the app repository to the EC2 and run the provision script, then npm to run the app on the IP associated with the EC2 instance.
- App is located on the public subnet of the VPC
- Create an EC2 instance - VM
- Ubuntu 18.04 LTS
- Select size of VM
- Security Group rules
- SSH into EC2 via Git Bash using AWS Key
- Check VM with update and upgrade -y
- Install nginx to be accessed on public IP
- enable public IP for the EC2 instance 
- Load App code into the EC2 via Git clone
- Install dependencies 
- CD into App folder
- npm install and npm start to load app into web browser

**EC2 for Database**
- Located within the private subnet within the VPC and only the app can access the database (NEVER HAS A PUBLIC IP)
- EC2 Linux Ubuntu 18.04 LTS
- T2.Micro
- Default Storage
- Tags eng99_raj_db
- SG allow 27017 only from your app IP
- Place App EC2 instnce IP in the SG of DB EC2 
- Allow SSH port 22 from your IP only
- eng99_raj_db_sg
- SSH into your DB EC2 instance 
- Install required MongoDB
- Status Active
- Change MongoDB.conf file BindIP to 0.0.0.0
- Restart, enable, status
- head back to app instance 
- Create env var DB_HOST="mongodb://db-ip:port/posts"
- Source it 
- cd app
- node seeds/seed.js
- npm start