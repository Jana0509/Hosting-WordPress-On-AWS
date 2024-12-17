# Hosting-WordPress-On-AWS
Host a Scalable, Reliable and Secure WordPress Application in 3 Tier Architecture on AWS 

## Introduction:
This Project demonstrates deployment of WordPress website in VPC from scratch and hosting a website Scalable, Reliable and Secure on AWS uisng various AWS Services.This Website is deployed on EC2 instances sitting in private subnet fronted with the Application Load Balancer(ALB) routing the traffic across different Availability Zones(AZs) and EFS(Elastic File Service) for shared storage and storing the data in RDS(Relational Database Service) also sitting in private subnet. To connect the Private instances, EC2 Instance Connect Endpoint Service for secure SSH access.

## Architecture Overview: 



# The architecture includes:

- A Custom VPC with a  Public Subnet and Private Subnet across two Availability Zones.
- EC2 Instances Across different Availbility Zones used to compute the WordPress Website and sitting in the Private Subnets.
- EC2 Auto Scaling group for the scalaibility for the EC2 instances.
- Relational Database Service(RDS) main and standby for storing the data deployed in private subnet across multiple availability Zones.
- Elastic File Storage(EFS) for the shared storage across AZs mounted to the EC2 Instances.
- Application Load Balancer(ALB) for routing the traffic across Multiple AZs sitting in Public Subnet.
- NAT Gateway deployed in public subnet acts as a proxy for the private instances to communicate with Internet.
- EC2 Instance Connect to securely access the private instances.
- Route 53 for the for domain name registration and DNS configuration
- IAM for the Secured usage across Resources
- SSL/TLS encryption using AWS Certificate Manager.
- Simple Notification Service (SNS) for notifications about scaling events

# AWS Resources Used

- VPC : Created a Custom VPC from Scratch with public and private subnets across two availability zones.
- NAT GATEWAY : Used as a proxy for the private Instances such as EC2 to contact Internet.
- ALB : Distributes traffic across EC2 instances in multiple availability zones
- ASG : Used for Scalability of EC2 Instances.
- EFS : Provides shared storage for WordPress files across EC2 instances across Multiple Availabilty Zones.
- RDS : Data Storage service in the relational manner across Multiple availability Zones.
- ACM : To Store TLS/SSL Certificates and Provides SSL/TLS certificates for secure website communication.
- IAM : Identity and Access Management for the Resources and users
- Simple Notification Service (SNS): Sends notifications related to Auto Scaling activities.
- EC2 Instance Connect Endpoint Service: Used to securely SSH into instances in private subnets without requiring bastion hosts or public IPs.


