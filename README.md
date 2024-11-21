# AWS DevSecOps React App: Secure CI/CD Pipeline with Terraform

## Table of Contents
- [Introduction](#introduction)
- [Project Overview](#project-overview)
- [Security Best Practices](#security-best-practices)
- [Prerequisites](#prerequisites)
- [Project Setup and Execution](#project-setup-and-execution)
- [Jenkins Setup and Access](#jenkins-setup-and-access)
- [SonarQube Setup](#sonarqube-setup)
- [React Application Setup](#react-application-setup)
- [Conclusion](#conclusion)
- [Resources](#resources)

## Introduction
This comprehensive guide demonstrates how to deploy a secure and scalable AWS DevSecOps project utilizing Jenkins, SonarQube, and a React application. The goal is to implement Infrastructure as Code (IaC) practices using Terraform while adhering to AWS best security practices as of November 2024. This guide will help you deploy your applications and services on AWS EC2 instances, following security protocols and configurations that make the system production-ready.

## Project Overview
In this project, we will deploy the following services:
- **Jenkins**: A popular automation server for continuous integration and continuous delivery (CI/CD).
- **SonarQube**: A tool for continuous inspection of code quality, ensuring clean, secure code.
- **React**: A modern JavaScript library for building user interfaces.

Each of these services will be deployed on its own EC2 instance, ensuring that the resources stay within the AWS free tier. We’ll use Terraform to manage the infrastructure, creating and configuring the EC2 instances, security groups, and associated resources.

## Security Best Practices
This project adheres to several key security principles:
- **Least Privilege**: The project uses IAM roles with the minimum required permissions for EC2 instances and Terraform operations.
- **SSH Access Control**: SSH access to EC2 instances is restricted by security groups, ensuring only authorized IPs can access the instances.
- **Sensitive Data Handling**: Credentials, including the Jenkins admin password, are securely retrieved from EC2 instances and not exposed in public documentation.
- **Encryption**: Any sensitive information, such as SSH keys and credentials, is stored securely using AWS IAM and encrypted S3 buckets (if applicable).
- **State Management**: Terraform state files are securely managed, with an optional remote backend for better security and collaboration.

## Prerequisites
Before you start, ensure you have the following tools and accounts:
- **AWS Account**: Set up an AWS account if you don’t already have one.
- **Terraform**: Install Terraform to manage your AWS infrastructure.
  - [Terraform Installation](https://learn.hashicorp.com/terraform/getting-started/install.html)
- **AWS CLI**: AWS command-line tool for interacting with AWS services.
  - [AWS CLI Installation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- **SSH Key Pair**: Generate an SSH key pair to access your EC2 instances securely.
  - [Generating SSH Keys in AWS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)

## Project Setup and Execution
Clone the repository and navigate to the project directory.
```sh
git clone https://github.com/yourusername/aws-devsecops-project.git
cd aws-devsecops-project
```
**Initialize Terraform:**
Initialize your Terraform environment with the following command:
```sh
terraform init
```
**Plan the Infrastructure:**
Review the planned infrastructure with the command:
```sh
terraform plan
```
**Apply the Configuration:**
Apply the configuration to provision the infrastructure:
```sh
terraform apply
```
After a successful deployment, Terraform will output the public IP addresses of the instances where you can access your services.

## Jenkins Setup and Access
After the Jenkins EC2 instance is deployed, you need to access it to complete the setup process.

**Steps to Get the Jenkins Administrator Password:**
1. **Connect to the EC2 Instance**: Use EC2 Instance Connect from the AWS console to access the Jenkins instance or SSH into it directly. Make sure your security group allows SSH access from your IP address.
2. **Retrieve the Administrator Password**: After logging into the instance, retrieve the Jenkins administrator password by running the following command:
   ```sh
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```
3. **Login to Jenkins**:
   Open your browser and visit `http://<public_ip>:8080`.
   Use the retrieved password for the first login.
4. **Complete Setup**:
   After logging in, Jenkins will prompt you to install suggested plugins.
   You can then configure Jenkins by creating an admin user.

## SonarQube Setup
1. **Access the SonarQube EC2 Instance**: SSH into the SonarQube instance using the public IP provided by Terraform.
2. **Start SonarQube**: On the instance, ensure that SonarQube is running on port 9000, and navigate to it in your browser at `http://<public_ip>:9000`.
3. **Configure SonarQube**:
   - Set up the initial admin account.
   - Configure project-specific quality gates, rules, and dashboards.

## React Application Setup
1. **Access the React EC2 Instance**: SSH into the React application instance.
2. **Build and Run the Application**: Run the following commands to install dependencies and start the React app:
   ```sh
   npm install
   npm run build
   npm start
   ```
3. **Access the React App**: The app will be available at `http://<public_ip>:3000`.

## Conclusion
This project deploys a secure, scalable AWS DevSecOps environment for Jenkins, SonarQube, and React using Terraform. By following the security best practices outlined, you ensure that your cloud infrastructure is both effective and safe. This setup offers a robust foundation for building, testing, and deploying applications securely within AWS.

## Resources
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/index.html)
- [Terraform Documentation](https://www.terraform.io/docs/index.html)
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/index.html)
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [SonarQube Documentation](https://docs.sonarqube.org/)
