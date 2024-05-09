---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
## Why Immutable Servers?

The DevOps community has embraced the immutable server concept, with good reason. Immutable servers are fully provisioned by automated tooling, and an engineer never needs to access the server to configure it manually. This results in predictable systems – the way a server is configured can be predicted near-exactly by what is in your source control. Immutable servers are faster to deploy, because computers can type more quickly than people.

They can also be more secure. When servers are predictable and fast to re-deploy, sysadmins don’t have much incentive to leave them running for long periods of time. If you’re in the habit of re-provisioning your servers daily, (or even hourly, in the case of some companies who deploy multiple times a day) then an intruder who does make it onto your machine won’t have as much time to set up shop and explore. Long running servers are risky: the Equifax breach occurred over a period of 76 days.  Immutable servers with a short lifespan are a great addition to a strong defense in depth strategy.

![ConnectPrivate](/immutable-infrastructure/images/1.introduction/packer-ansible-terraform.png)

## What are the DevOps tools?

There are many approaches to creating immutable servers. When I joined my current project at company, I encountered a new-to-me stack used to create immutable servers in the Amazon Web Services (AWS) GovCloud. While familiar with Terraform, I hadn’t used either Packer or Ansible before. Now that I’ve spent the good part of the year working with this stack, I’m a convert. While the stack is a bit complex to setup (at least compared to the good old “bash script that runs on new nodes” paradigm) the reliability, fast deployment speeds, and visibility afforded by this stack make the initial pain of setup well worth it.

## Packer

[https://www.packer.io](https://www.packer.io/)

Packer is a Hashicorp product. In their words, “Packer is an open source tool for creating identical machine images for multiple platforms from a single source configuration.” We use Packer to take US Government approved Amazon Machine Images (AMIs)  running Red Hat 7 and produce new versions of these AMIs that have all the configuration and software we need to run our application securely in AWS.

Packer supports multiple “provisioners,” which handle the actual server configuration. These can be simple shell scripts, or can be a more robust tool like Ansible. Packer handles the creation of the VM and packaging as an AMI, Ansible handles the configuration of the virtual machine.

## Ansible

[https://www.ansible.com](https://www.ansible.com/)

Ansible was created by Red Hat as a configuration management tool. It automates all software installation, package management, and configuration on our AWS EC2 hosts. Ansible ensures that any software, config file change, or cron job is installed the same way every time.

Ansible is agentless, so your build toolchain has fewer moving parts. (Probably the worst part of DevOps is becoming a sysadmin for the tools you build to replace you as a sysadmin.) The YAML syntax is incredible and well-documented. The Ansible Galaxy ecosystem is well-stocked with playbooks for all kinds of server management tasks, from deploying an Apache server to [complying with federal system security guidelines](https://madeintandem.com/blog/automating-security-compliance-ansible-devsecops-made-easy/).

## Terraform

https://www.terraform.io/

Terraform is a Hashicorp product. It allows us to “safely and predictably create, change, and improve infrastructure.” The term infrastructure refers to components like EC2 instances, load balancers, databases, and networking. Terraform integrates with AWS APIs to translate and run configuration code into AWS API calls that provision our architecture – everything from the networking to the app servers and S3 buckets. Once we’ve “baked” an AMI using Packer and Ansible, we use Terraform to deploy that AMI as an EC2 instance into our cloud environment. This results in a live server in under 3 minutes.