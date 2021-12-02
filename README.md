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
- SG allow 27017 only from your app IP (TCP)
- Place App EC2 instnce IP in the SG of DB EC2 
- Allow SSH port 22 from your IP only
- eng99_raj_db_sg
- SSH into your DB EC2 instance 
- Install required MongoDB for 18.04 Ubuntu
- Status Active
- Change MongoDB.conf file BindIP to 0.0.0.0
- `sudo systemctl` restart, enable, status
- head back to app instance 
- Create env var DB_HOST="mongodb://db-ip:port/posts"
- `sudo nano ~/.bashrc` 
- inside bashrc, `export DB_HOST=="mongodb://db-ip:port/posts"` 
- Source it 
- `cd app`
- `node seeds/seed.js`
- `npm install`
- `npm start`
- Enter App EC2 ip:3000/posts into web browser to see database

## AMI (Amaozon Machine Image)
- Select EC2 instance and then create an image of the instance in the actions tab
- Once the image has been created, stop the original instance and launch the image
- Some details will be required
- t2-micro 
- Storage
- Tags 
- Security Groups 
- Once the details above have been added the image will be formed into an instance which contains all the data from the original instance
- The IP of the image will be different from the original instance
- So make sure to change the IP where necessary, such as the security groups and in the bashrc file in the app VM.

## Security Groups
Acts as a virtual firewall for your EC2 instance to control inbound and outbound traffic. 
When you launch an instance in the VPC you can assign upto 5 security groups to one instance. Security groups act at the instance level, not the subnet level. Therefore each instance in a subnet in your VPC can be assigned to a different set of security groups.  

## CloudWatch
Amazon CloudWatch monitors your AWS resources and the applications you run on AWS real time. CloudWatch can be used to collect and track metrics, which are variables you can measure for your resources and applications. 

**Alarms**
CloudWatch alarms can be set to watch metrics and send notifications when the mterics reach a certin threshold set by the account holder, the alarms can also make changes to the resources being monitored. 
For example, you can monitor CPU usage ad disk reads and writes of your Amazon EC2 instances and then use this data to determine whether you should launch additional instances to handle increased load. You can also use this data to stop under-used instances to save money. 

**SNS**
A managed service that provides message delivery from publishers to subscribers (aka producers and consumers). Publishers communicate asynchronously with subscribers by sending messages to a topic, which is a logical access point and communication channel. Clients can subscribe to the SNS topic and recieve published messges using a supported endpoint type such as Amazon Kinesis Data Firehose, Amazon SQS, AWS Lambda, HTTP, email, mobile push notifications and mobile text messages (SMS).

## Explain how to make your app Highly Available and Scalable
Scalable
- Modularity over monolithic
An applications software is contstructed of multiple and loosely coupled building blocks (functions). These functions collectively integrate through pre-defined common interfaces or APIs to form the desired application functionaility (microservices architecture). 
- Horizontal Scaling/Scale-out 
The capability to automatically add systems/instances in a distributed manner in order to handle an increase in load. The load is distributed across multiple instances. By distributing these instances across Availability zones, horizontal scaling only increases performance but also improves overall reliability. 
For this method to work seamlessly, the application needs to be designed to support a stateless scaling model, where the applications state information is stored and requested independently from the applications instances. 
- Leverage the content delivery network 
- Go serverless where possible
- Secure by design
- Design for failure
The reliability of a service or solution in the cloud depends on multiple factors, the primary of which is resiliency. This design principle becomes even more critical at scale because the failure impact magnitude typically will be higher. Therefore, to achieve a reliable scalability, it is essential to design a resilient solution, capable of recovering from infrastructure or service disruptions. This principle involves designing the overall solution in such a way that even if one or more of its components fail, the solution is still be capable of providing an acceptable level of its expected function(s).
**What services are used to achieve this**
- High Availaability
Elastic Load Balancing
Availability Zones 
- Scalable
Amazon CloudFront and edge locations

