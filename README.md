

WordPress on AWS
This GitHub repository provides resources and scripts necessary for deploying a WordPress website on Amazon Web Services (AWS). It aims to utilize AWS's robust infrastructure to ensure high availability, scalability, and security for the WordPress application. By following this guide, you will deploy WordPress within a VPC, utilizing EC2 instances, RDS for the database, EFS for file storage, and more.

Architecture Overview
The deployment architecture ensures fault tolerance and high availability by incorporating:

Virtual Private Cloud (VPC): With public and private subnets across two Availability Zones.
Internet Gateway: For VPC internet connectivity.
Security Groups: Virtual firewalls to control traffic.
Public Subnets: Hosting the NAT Gateway and Application Load Balancer.
Private Subnets: For enhanced security of web servers.
EC2 Instance: Secure SSH access through EC2 Instance Connect.
Application Load Balancer: Distributes web traffic across EC2 instances.
Auto Scaling Group: Automatically scales EC2 instances.
Amazon RDS: Managed relational database service.
Amazon EFS: Elastic file storage.
AWS Certificate Manager: Manages SSL/TLS certificates.
AWS Simple Notification Service (SNS): For auto-scaling notifications.
Amazon Route 53: For DNS management and domain name registration.
Deployment Scripts
Initial WordPress Setup
WordPress Installation Script: Automates the setup of WordPress on EC2 instances, including installing necessary services like Apache, PHP, and MySQL, and configuring EFS for storage.
Auto Scaling Configuration
Launch Template Script: Ensures new EC2 instances within the Auto Scaling Group are appropriately configured with the WordPress setup.
Getting Started
Preparation: Clone this repository to get started with your AWS WordPress deployment.
AWS Configuration: Create the necessary AWS resources following the architecture overview. Ensure you have a VPC, subnets, and an Internet Gateway set up.
Deploy WordPress: Use the provided WordPress Installation Script to set up your initial WordPress site on an EC2 instance.
Auto Scaling Setup: Configure the Auto Scaling Group with the Launch Template Script to ensure new instances are set up correctly.
Access Your Site: Once deployed, access your WordPress site through the DNS name provided by the Application Load Balancer.
Contributing
Contributions are welcome! If you have improvements or suggestions, please fork the repository and submit a pull request.

License
This project is licensed under the MIT License. See the LICENSE file in this repository for more information.
