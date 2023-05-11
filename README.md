## Deploying a WordPress website on AWS secuerly and high availabilty

### Resources used in this project:
-   Amazon VPC (Virtual Private Cloud) with Public & Private Subnets in two Availability Zones
-   Internet Gateway & NAT Gateways
-   Public Route Table (Public subnet)
-   Private Route Table (Private subnet)
-   Route 53 ( Public & Private Hosted Zone) with simple routing policies
-   EC2 Instances ( Security groups, NACL )
-   Application Load Balancer
-   Auto Scaling Group
-   Elastic File System (EFS)
-   RDS ( Multi AZ, Replicas )
-   Install WordPress


### Project Architecture:
![Project Diagram](https://github.com/ahsan598/aws-wordpress-website/blob/main/aws-wordpress-website-diagram.svg)


### How I Implemented:

Navigate to AWS console, select the region nearest to your location and create a custom VPC for this project. Then create two public subnets and four private subnets; [total 6 subnets] in two AZ's (availabilty zones). 

Internet gateway allows communication between your public subnets and the internet and that's why we need to create a IGW (Internet Gateway) for this purpose.

Then in the routing table we have to configure the route internet traffic from IGW to public subnets.
As for our private subnets, which will be used for backend application hosting and database hosting, we don't want to access them from the internet directly. So we need NAT gateway for updates, security patches or any download purpose. So we need to create NAT-GW(Network Address Translation Gateway) for this puposes.

Note: NAT-GW is a chargable service per hour, so I will only use them when needed them otherwise they will remain down.

I set up HOST for accessing my instances in the private subnets as I can't access them from public internet. I applied some security for the host by changing the `ssh port` 22 to another custom port[from instances and from security group also]. change the security group for the ssh connection which will only connect from home networks.

We are going to create a Amazon Relational Database Service (Amazon RDS) to host our WordPress database.
Amazon RDS is an AWS service that makes it easy to set up, operate, and scale a relational database in the cloud.

We will create an Elastic File System (EFS) with mount targets in each availability zone to store the files and application codes for our WordPress site. Then from Amazon EC2 instance move files to EFS.

We will register a domain name in Route 53 for our WordPress site.
Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints.

Now it's time to deploy!