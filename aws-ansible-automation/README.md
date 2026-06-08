# AWS Ansible Automation Lab

## Overview

In this lab, I used Amazon Web Services (AWS) and Ansible to automate the configuration of Linux web servers. The goal was to create an Ansible control node that could securely manage two separate EC2 web servers. I also configured AWS Security Groups and SSH Agent Forwarding to secure access between the servers.

This project helped me gain hands-on experience with cloud infrastructure, Linux administration, automation, and AWS security concepts.

## Technologies Used

* Amazon Web Services (AWS)
* Amazon EC2
* Ubuntu Linux
* Ansible
* SSH Agent Forwarding
* AWS Security Groups
* GitHub

## Project Architecture

The environment consisted of:

* 1 Ansible Control Node
* 2 Linux Web Servers
* AWS Security Groups for access control
* SSH Agent Forwarding for secure administration

The Ansible node was used to connect to and manage both web servers without storing private keys directly on the servers.

## Objectives

* Deploy multiple Linux EC2 instances in AWS
* Configure Security Groups to restrict access
* Set up SSH Agent Forwarding
* Install and configure Ansible
* Automate server configuration using Ansible playbooks
* Practice secure cloud administration techniques

## Skills Demonstrated

### AWS Cloud Infrastructure

* Launched and managed EC2 instances
* Configured Security Groups
* Managed cloud-hosted Linux servers

### Linux Administration

* Connected to remote servers using SSH
* Managed server access and permissions
* Performed system configuration tasks

### Automation

* Installed and configured Ansible
* Executed playbooks against multiple servers
* Automated server management tasks

### Security

* Implemented Security Group rules
* Used SSH key authentication
* Configured SSH Agent Forwarding

## Challenges Encountered

One of the biggest challenges was understanding how SSH Agent Forwarding works and how it allows the Ansible node to securely connect to other servers without copying private keys. I also spent time troubleshooting Security Group rules to ensure the servers could communicate while remaining secure.

## What I Learned

This lab taught me how infrastructure automation can reduce manual configuration work and improve consistency across multiple servers. It also reinforced the importance of Linux administration skills, network security, and proper access control in cloud environments.

Through this project, I gained practical experience with AWS EC2, Security Groups, SSH, Linux, and Ansible automation, which are commonly used in cloud and infrastructure engineering roles.

## Future Improvements

If I expanded this project further, I would:

* Use Terraform to deploy the infrastructure
* Add CloudWatch monitoring and alerts
* Place web servers in private subnets
* Implement a Load Balancer
* Explore CI/CD integration with GitHub Actions
