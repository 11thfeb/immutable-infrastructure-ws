---
title : "Cài đặt Ansible"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

## 2.2. Cài đặt Ansible

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

#### Kiểm tra cài đặt

Sau khi cài đặt Ansible, xác minh rằng cài đặt đã hoạt động bằng cách mở một cửa sổ lệnh hoặc console mới và kiểm tra xem ansible có sẵn không:

```shell
$ ansible --version
ansible [core 2.14.6]
```