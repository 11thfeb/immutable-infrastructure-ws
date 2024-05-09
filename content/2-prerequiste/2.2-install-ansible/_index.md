---
title : "Installing Ansible"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

## 2.2. Installing Ansible

[https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

```shell
# Install Ansible repository.
$ sudo apt-get update && sudo apt-get upgrade -y
$ sudo apt-get install -y software-properties-common
$ sudo apt-add-repository -y ppa:ansible/ansible

# Install Ansible.
$ sudo apt-get update
$ sudo apt-get install -y ansible
```

#### Verifying the Installation

After installing Ansible, verify the installation worked by opening a new command prompt or console, and checking that ansible is available:

```shell
$ ansible --version
ansible [core 2.14.6]
```