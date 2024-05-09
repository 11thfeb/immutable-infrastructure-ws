---
title : "Write Packer"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

First, let's create the Packer directory structure as shown below.

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

Create a file ansible.sh in scripts folder:

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

Create a file template.pkr.hcl in packer folder:

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

After you have finished coding according to the template above, you can run the following command.

```shell
## Check that a template is valid
$ packer validate

## Install missing plugins or upgrade plugins
$ packer init

## Build image(s) from template
$ packer build template.pkr.hcl
```

While waiting for Packer to build the image, you can go and make a cup of coffee while you wait.

![Connect](/immutable-infrastructure/images/6.packer/packer-console.png)

Go to [Amazon Machine Images (AMIs)](https://us-east-1.console.aws.amazon.com/ec2/home?region=us-east-1#Images:visibility=owned-by-me), you can see your image created.

![Connect](/immutable-infrastructure/images/6.packer/packer-ami.png)