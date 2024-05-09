---
title : "Installing AWS CLI"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

## 2.3. Installing AWS CLI

[https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

```shell
$ sudo apt-get update
$ sudo apt-get install python3-pip
$ sudo pip install awscli
```

#### Verifying the Installation

After installing AWS CLI, verify the installation worked by opening a new command prompt or console, and checking that AWS CLI is available:

```shell
## Verify Installation
$ aws --version
```