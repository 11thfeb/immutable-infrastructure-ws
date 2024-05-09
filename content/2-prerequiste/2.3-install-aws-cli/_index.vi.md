---
title : "Cài đặt AWS CLI"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

## 2.3. Install AWS CLI

[https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

```shell
$ sudo apt-get update
$ sudo apt-get install python3-pip
$ sudo pip install awscli
```

#### Kiểm tra cài đặt

Sau khi cài đặt AWS CLI, xác minh rằng cài đặt đã hoạt động bằng cách mở một cửa sổ lệnh hoặc console mới và kiểm tra xem AWS CLI có sẵn không:

```shell
## Verify Installation
$ aws --version
```