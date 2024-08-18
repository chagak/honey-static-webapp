How to Host a Static Website on AWS
# Static Website Hosting on AWS

This project demonstrates the deployment of a static HTML web application on AWS using various cloud services and infrastructure components. The project includes configuring a secure and scalable environment, deploying web servers, and ensuring high availability and fault tolerance.

## Project Overview

The web app is hosted on Amazon EC2 instances within a Virtual Private Cloud (VPC) and utilizes several AWS resources to ensure reliability, security, and scalability. The infrastructure is designed to leverage multiple Availability Zones, with public and private subnets, an Application Load Balancer, and an Auto Scaling Group.

## Architecture

The infrastructure includes:

1. **Virtual Private Cloud (VPC):** Configured with public and private subnets across two Availability Zones.
2. **Internet Gateway:** Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups:** Act as a network firewall to control inbound and outbound traffic.
4. **Availability Zones:** Used to enhance system reliability and fault tolerance.
5. **Public Subnets:** Host infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint:** Provides secure connections to instances in both public and private subnets.
7. **Private Subnets:** Web servers (EC2 instances) are placed here for enhanced security.
8. **NAT Gateway:** Allows instances in private subnets to access the Internet.
9. **EC2 Instances:** Host the static website.
10. **Application Load Balancer:** Distributes traffic evenly across an Auto Scaling Group of EC2 instances.
11. **Auto Scaling Group:** Manages EC2 instances to ensure availability, scalability, and fault tolerance.
12. **GitHub:** Used for version control and collaboration.
13. **AWS Certificate Manager:** Secures application communications.
14. **Amazon SNS:** Configured to alert about activities within the Auto Scaling Group.
15. **Route 53:** Used to register the domain name and set up a DNS record.

## Deployment Steps

### Infrastructure Setup

1. **VPC Configuration:** Set up a VPC with public and private subnets across two Availability Zones.
2. **Internet Gateway:** Deploy to enable Internet access for VPC instances.
3. **Security Groups:** Create and assign to control access to resources.
4. **EC2 Instances:** Launch instances within private subnets.
5. **Load Balancer & Auto Scaling:** Configure to distribute traffic and manage instance scaling.

### Web Server Setup

Use the following Bash script to set up the web server on EC2 instances:

```bash
#!/bin/bash

sudo su
yum update -y
yum install -y httpd
cd /var/www/html
yum install git -y
git clone https://github.com/chagak/honey-static-webapp.git
cp -r honey-static-webapp/* /var/www/html/
rm -rf honey-static-webapp/
systemctl enable httpd 
systemctl start httpd
```

This script performs the following tasks:
- Updates all installed packages.
- Installs Apache HTTP Server and Git.
- Clones the project repository from GitHub.
- Deploys the static website files to the Apache web root.
- Starts the Apache service and enables it to start on boot.

## Repository Contents

- **Infrastructure Diagrams:** Visual representation of the architecture.
- **Deployment Scripts:** Bash script for deploying the web app on EC2 instances.

## Conclusion

This project demonstrates a robust and scalable approach to hosting a static website on AWS, utilizing best practices in cloud architecture, security, and automation.
