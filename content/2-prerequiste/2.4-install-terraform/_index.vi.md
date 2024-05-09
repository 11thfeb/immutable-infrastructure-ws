---
title : "Cài đặt Terraform"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

## 2.4. Cài đặt Terraform

[https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

Đảm bảo hệ thống của bạn được cập nhật và bạn đã cài đặt các gói gnupg, software-properties-common, và curl. Bạn sẽ sử dụng các gói này để xác minh chữ ký GPG của HashiCorp và cài đặt kho lưu trữ gói Debian của HashiCorp.

```shell
$ sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```

Cài đặt khóa GPG của HashiCorp.

```shell
$ wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```

Xác minh GPG key.

```shell
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```

Lệnh ***gpg*** sẽ báo cáo dấu vân tay của khóa:

```shell
/usr/share/keyrings/hashicorp-archive-keyring.gpg
-------------------------------------------------
pub   rsa4096 XXXX-XX-XX [SC]
AAAA AAAA AAAA AAAA
uid           [ unknown] HashiCorp Security (HashiCorp Package Signing) <security+packaging@hashicorp.com>
sub   rsa4096 XXXX-XX-XX [E]
```

Thêm kho lưu trữ chính thức của HashiCorp vào hệ thống của bạn. Lệnh lsb_release -cs sẽ tìm mã phân phối cho hệ thống hiện tại của bạn, chẳng hạn như buster, groovy, hoặc sid.

```shell
$ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```

Tải về & Cài đặt Terraform.

```shell
$ sudo apt update
$ sudo apt-get install terraform
```

#### Kiểm tra cài đặt

Sau khi cài đặt Terraform, xác minh rằng cài đặt đã hoạt động bằng cách mở một cửa sổ lệnh hoặc console mới và kiểm tra xem Terraform có sẵn không:

```shell
$ terraform -help
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.
#...
```