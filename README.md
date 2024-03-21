![Alt text](/Host_a_Static_Website_on_AWS.png)
---

# Hosting a Static Website on AWS

This project outlines the deployment of a static HTML web application on AWS. The setup includes a robust AWS infrastructure utilizing EC2 instances, VPC, Internet Gateway, Security Groups, NAT Gateway, Application Load Balancer, Auto Scaling, Certificate Manager, Route 53, and more to ensure high availability, fault tolerance, security, and scalability. Below is a detailed guide on how the project was set up, along with deployment scripts.

## Infrastructure Overview

The project's infrastructure includes the following key components:

1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different availability zones for enhanced isolation and availability.
2. **Internet Gateway**: Deployed to enable connectivity between VPC instances and the wider Internet.
3. **Security Groups**: Act as a network firewall to control inbound and outbound traffic to EC2 instances.
4. **Availability Zones**: Utilized two availability zones to enhance system reliability and fault tolerance.
5. **Public Subnets**: Used for infrastructure components like the NAT Gateway and Application Load Balancer to allow external access.
6. **EC2 Instance Connect Endpoint**: Implemented for secure connections to assets within both public and private subnets.
7. **Private Subnets**: Hosted web servers (EC2 instances) within private subnets for enhanced security.
8. **NAT Gateway**: Enabled instances in both application and data private subnets to access the Internet.
9. **Application Load Balancer & Target Group**: For evenly distributing web traffic across an Auto Scaling Group of EC2 instances.
10. **Auto Scaling Group**: Automatically manages EC2 instances to ensure the website's availability and scalability.
11. **GitHub**: Stored web files for version control and collaboration.
12. **Certificate Manager**: Secured application communications.
13. **Simple Notification Service (SNS)**: Configured to alert about activities within the Auto Scaling Group.
14. **Route 53**: Registered the domain name and set up DNS records for the website.

## Deployment Script

Below is a bash script used to deploy the web application on an EC2 instance:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Getting Started

To replicate this project, ensure you have an AWS account and the necessary permissions to create and manage the resources listed above. Follow the infrastructure overview to set up your environment and use the provided deployment script to host your static website.

## Contributing

Feel free to fork the repository and submit pull requests with improvements or updates to the deployment process.

---


