## Deploying a WordPress website on AWS
We are hosting a wordpress website on AWS


### Resources:

- Amazon `VPC` with public and private subnets in 2 different `availability zones`.
- We are using 2 `Availabilty Zones` for high availabilty and fault tolerance.
- An `Internet Gateway` is used to access internet by instances inside VPC.
- Resources such as NAT Gateway, Bastion Host & Application Load Balancer uses `Public Subnets`.
- We will put webservers & databases server in `Private Subnets` to protect them. 
- The `NAT Gateway` allows the instances in private subnets to allow internet access.
- We are using `MYSQL RDS` Database.
- We will create `Security Groups` for our EC2 instances & database servers for inbound & outbound rules.
- We are using `EC2 instance` to host our website.
- `Application Load Balancer` is used to distribute web traffic across instances in multiple AZs.
- Using `Auto Scaling Group` to make our EC2 instances highly available, scalable, fault tolerance & elastic.
- We are using `AWS S3` to store our webfiles.
- Amazon `Route 53` to register our Domain name.
- We will use `IAM Role` to give permission to EC2 instance to download webfiles from `AWS S3`.
- Amazon `CloudWatch` to monitor our resources in our VPC to make sure all resources are up and to collect logs and track metrics.



### Architecture:
![Project Diagram](https://github.com/ahsan598/aws-wordpress-website/blob/main/aws-wordpress-website-diagram.svg)




##### Note: NAT-GW is a chargable service per hour, so I will only use them when needed them otherwise they will remain down. All the resourses created in the course of doing this project has to be deleted in order to avoid charges.