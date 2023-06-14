## Deploying a WordPress website on AWS secuerly and high availabilty

### Resources created in this project:
- Amazon Virtual Private Cloud (Amazon VPC)
- Internet Gateway (IGW)
- NAT Gateway (across all public subnets)
- Amazon VPC subnets (public, private) in all the Availability Zones (AZs) selected
- Routing tables for public subnets - routing through IGW
- Routing tables for private subnets - routing through NAT Gateway
- Mulitple VPC Security Groups
- Bastion Auto Scaling Group instances - in public subnets
- Amazon Relational Database Service (Amazon RDS) Aurora cluster - in private - subnets
- Amazon Elastic File System (Amazon EFS) file system - with mount targets in private subnets
- Amazon Elastic Load Balancing (Amazon ELB) Application Load Balancer (ALB) - in public subnets
- Amazon Route53 DNS record set
- Amazon CloudWatch alarms to monitor Amazon EFS burst credit balance
- WordPress


### Project Architecture:
![Project Diagram](https://github.com/ahsan598/aws-wordpress-website/blob/main/aws-wordpress-website-diagram.svg)


### Deployment:

Navigate to AWS console, select the region nearest to your location and create a custom VPC for this project. Then create two public subnets and four private subnets; [total 6 subnets] in two AZ's (availabilty zones). 

Internet gateway allows communication between your public subnets and the internet and that's why we need to create a IGW (Internet Gateway) for this purpose.

Then in the routing table we have to configure the route internet traffic from IGW to public subnets.
As for our private subnets, which will be used for backend application hosting and database hosting, we don't want to access them from the internet directly. So we need NAT gateway for updates, security patches or any download purpose. So we need to create NAT-GW(Network Address Translation Gateway) for this puposes.

##### Note: NAT-GW is a chargable service per hour, so I will only use them when needed them otherwise they will remain down.

Launch an EC2 instance using a suitable AMI (Amazon Machine Image), choose the desired instance type, storage, and other configuration options. Configure the network settings to use the VPC and subnet we created.

We are going to create a Amazon Relational Database Service (Amazon RDS) using MySQL or another supported database engine to host our WordPress database. Configure the RDS instance with appropriate storage, instance size, and networking settings.
Ensure the RDS instance is accessible from the EC2 instances within your VPC.

Connect to the EC2 instance using SSH or other remote access methods. Download and install WordPress on the EC2 instance. Configure the WordPress installation, including the database connection settings.

We will create an Elastic File System (EFS) with mount targets in each availability zone to store the files and application codes for our WordPress site. Then from Amazon EC2 instance move files to EFS.

Obtain a domain name for your WordPress website if we don't have one. Configure DNS records to point our domain to the public IP address of your EC2 instance or set up an Amazon Route 53 record for our domain.

### Now it's time to deploy!
Access your WordPress website through the domain name to ensure it's working correctly.





##### Learned from aos note by @Azeez Salu 