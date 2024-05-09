---
title : "Viết Packer"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

Đầu tiên chúng ta tạo cấu trúc thư mục Packer như dưới.

```shell
$ tree
├── ansible
│   ├── ansible-playbook-wordpress-nginx
|.........
├── packer
│   ├── scripts
│   │   ├── ansible.sh
│   ├── template.pkr.hcl
```

Tạo moojti file ansible.sh trong scripts folder:

```bash
#!/bin/bash -eux

# Install Ansible repository.
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible

# Install Ansible.
sudo apt-get update
sudo apt-get install -y ansible
```

Tạo một file template.pkr.hcl trong packer folder:

```hcl
packer {
  required_plugins {
    amazon = {
      version = ">= 1.2.8"
      source  = "github.com/hashicorp/amazon"
    }
  }

  required_plugins {
    ansible = {
      version = "~> 1"
      source = "github.com/hashicorp/ansible"
    }
  }
}

source "amazon-ebs" "ubuntu" {
  ami_name      = "your-ami-name"
  force_deregister = true
  instance_type = "t2.micro"
  region        = "us-east-1"
  source_ami_filter {
    filters = {
      name                = "ubuntu/images/*ubuntu-jammy-22.04-amd64-server-*",
      root-device-type    = "ebs"
      virtualization-type = "hvm"
    }
    most_recent = true
    owners      = ["099720109477"]
  }
  ssh_username = "ubuntu"
}

build {
  name = "your-ami-name"
  sources = ["source.amazon-ebs.ubuntu"]

  provisioner "shell" {
    script = "scripts/ansible.sh"
  }

  provisioner "ansible-local" {
    group_vars    = "../ansible/ansible-playbook-wordpress-nginx/group_vars"
    playbook_file = "../ansible/ansible-playbook-wordpress-nginx/playbook.yml"
    role_paths    = [
      "../ansible/ansible-playbook-wordpress-nginx/roles/nginx",
      "../ansible/ansible-playbook-wordpress-nginx/roles/wordpress",
      "../ansible/ansible-playbook-wordpress-nginx/roles/php"
    ]
  }
}
```

Sau khi code xong theo mẫu trên các bạn có thể chạy lệnh sau:

```shell
## Check that a template is valid
$ packer validate

## Install missing plugins or upgrade plugins
$ packer init

## Build image(s) from template
$ packer build template.pkr.hcl
```

Trong khi chờ Packer build image, bạn có thể đi pha một tách cà phê trong khi chờ đợi.

![Connect](/immutable-infrastructure/images/6.packer/packer-console.png)

Đi tới [Amazon Machine Images (AMIs)](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Images:visibility=owned-by-me), bạn sẽ nhìn thấy image của bạn đã được tạo.

![Connect](/immutable-infrastructure/images/6.packer/packer-ami.png)