---
title : "Cài đặt Packer"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

## 2.1. Cài đặt Packer

[https://developer.hashicorp.com/packer/install?product_intent=packer](https://developer.hashicorp.com/packer/install?product_intent=packer)

```shell
$ wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt-get update && sudo apt-get install packer
```

#### Kiểm tra cài đặt

Sau khi cài đặt Packer, hãy xác minh quá trình cài đặt đã hoạt động bằng cách mở dấu nhắc lệnh hoặc bảng điều khiển mới và kiểm tra xem trình đóng gói có sẵn không:

```shell
$ packer --version
Packer v1.10.3
```
