---
title : "Preparation "
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
Notes: We need to start and enable nginx using systemctl start and enable to ensure that nginx will be ready to process spontaneously.
{{% /notice %}}

In this workshop, I will be baking an AMI using Packer and doing configuration using Ansible during the baking process. A static website will be deployed. And the same Ansible code is being used to provision the static website using Nginx during this whole baking process. Tags will be assigned to AMI during baking process. It is intended to identify the latest AMI available and have it ready for EC2 instance creation. Subnet ID is supposed to be collected for Packer builder so that it is able to create AMI using the Subnet ID. Here we are going to manage our terraform code in two different sections: one is for creating VPC, subnet, and other network information, the other is for grouping EC2 instance inside our network using AMI created by the Packer previously.

### Content
- [Installing Packer](/immutable-infrastructure/2-prerequiste/2.1-install-packer/)
- [Installing Ansible](/immutable-infrastructure/2-prerequiste/2.2-install-ansible/)
- [Installing AWS CLI](/immutable-infrastructure/2-prerequiste/2.3-install-aws-cli/)
- [Installing Terraform](/immutable-infrastructure/2-prerequiste/2.4-install-terraform/)