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
- EFS : Provides shared storage for WordPress files across EC2 instances in Multiple Availabilty Zones.
- RDS : Data Storage service in the relational manner across Multiple availability Zones.
- ACM : To Store TLS/SSL Certificates and Provides SSL/TLS certificates for secure website communication.
- IAM : Identity and Access Management for the Resources and users
- Simple Notification Service (SNS): Sends notifications related to Auto Scaling activities.
- EC2 Instance Connect Endpoint Service: Used to securely SSH into instances in private subnets without requiring bastion hosts or public IPs.


# PROCEDURE FOR CREATING THE RESOURCES AND INSTALLATION:

1. Create the Custom VPC with private and public subnet in two availability zones.
   PFA Link for Creating the VPC : https://github.com/Jana0509/3-Tier-VPC-AWS

2. Create RDS MYSQL DB in Database Subnet. 

3. Creation EC2 Instance Connect Endpoint to SSH with the Web Instances in private subnet
(EC2 INSTANCE CONNECT : This allows SSH connections to the EC2 instances without the need for bastion hosts or public IP addresses, ensuring secure and controlled access.)

4. Create the EFS and mount it to the EC2 instances.

   4.1 Create the web root directory by SSH with the Web Instances using EC2 Instance Connect Endpoint
 
    sudo mkdir -p /var/www/html

   4.2 Mount EFS to the web root directory:
    
    sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport "$EFS_DNS_NAME":/ /var/www/html
   
   4.3 Restart Apache:

    sudo service httpd restart

Mounting the EFS to the EC2 instances will be done using Launch Template User data.

5.  Create the Launch Template with the user data
   Please refer the EC2 Launch Template file.

6. Create the Auto Scaling group and use the Launch template which we have created in previous step.

7. Create the Application Load balancer in public subnet and assign the target group
   
8. Access the WordPress website through the Load Balancer's DNS name.
