

Based on your project details, here's a README file tailored for your GitHub repository on hosting a WordPress website on AWS. This README outlines the project's infrastructure setup, including AWS services used and the script for installing WordPress.

---

# Hosting a WordPress Website on AWS

This project demonstrates the deployment of a WordPress website on Amazon Web Services (AWS), leveraging a highly available and secure architecture. This guide covers the creation of a Virtual Private Cloud (VPC), setup of EC2 instances for web servers, and configuration of various AWS services to ensure the scalability, fault tolerance, and security of the WordPress site.

## Architecture Overview

The deployment architecture incorporates the following AWS services:

1. **Virtual Private Cloud (VPC)** with public and private subnets across two Availability Zones for high availability and isolation.
2. **Internet Gateway** to allow communication between the VPC and the internet.
3. **Security Groups** to act as virtual firewalls for controlling traffic.
4. **EC2 Instances** positioned within private subnets for hosting the WordPress application, enhancing security.
5. **Application Load Balancer (ALB)** with a target group to distribute incoming web traffic evenly across EC2 instances.
6. **Auto Scaling Group** to automatically adjust the number of EC2 instances, ensuring website scalability and resilience.
7. **Amazon RDS** for a managed relational database service.
8. **Amazon EFS** for a scalable, elastic file system for storing web files.
9. **AWS Certificate Manager** for managing SSL/TLS certificates.
10. **Simple Notification Service (SNS)** for notifications related to the Auto Scaling Group activities.
11. **Amazon Route 53** for domain name registration and DNS management.

## Deployment Script

### WordPress Installation

Below is the script for setting up WordPress on an EC2 instance, including the installation of necessary components such as Apache, PHP, and MySQL, and configuring the EFS for shared file storage.

```bash
#!/bin/bash
# Become root user
sudo su

# Update installed packages
sudo yum update -y

# Create web directory
sudo mkdir -p /var/www/html

# Set EFS DNS name
EFS_DNS_NAME=fs-0a70826104fb4472b.efs.us-east-1.amazonaws.com

# Mount EFS to the web directory
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport "$EFS_DNS_NAME":/ /var/www/html

# Install Apache and start the service
sudo yum install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd

# Install PHP and necessary extensions
sudo dnf install -y php php-cli php-cgi php-curl php-mbstring php-gd php-mysqlnd php-gettext php-json php-xml php-fpm php-intl php-zip php-bcmath php-ctype php-fileinfo php-openssl php-pdo php-tokenizer

# Install MySQL and start the service
sudo wget https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
sudo dnf install -y mysql80-community-release-el9-1.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
sudo dnf install -y mysql-community-server
sudo systemctl start mysqld
sudo systemctl enable mysqld

# Set file permissions
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
sudo find /var/www -type f -exec sudo chmod 0664 {} \;
sudo chown apache:apache -R /var/www/html

# Download and install WordPress
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo cp -r wordpress/* /var/www/html/

# Configure WordPress
sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
sudo vi /var/www/html/wp-config.php

# Restart Apache
sudo service httpd restart
```

## Getting Started

To deploy your WordPress site on AWS using this setup:

1. Clone this repository to access the deployment script and reference architecture.
2. Set up the AWS environment according to the architecture overview, ensuring all services are correctly configured.
3. Run the provided WordPress installation script on your EC2 instance to set up the website.
4. Access your WordPress site through the domain configured in Route 53.

## Contributing

Contributions to improve the deployment process or any part of the project are welcome. Please fork the repository and submit a pull request with your changes.



--- 
