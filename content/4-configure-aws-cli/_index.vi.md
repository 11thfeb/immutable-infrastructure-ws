---
title : "Cấu hình AWS CLI"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

Ở bước trước, bạn đã tạo một tài khoản và nhận được access key & secret key. Ở bước này, bạn cần sử dụng access key & secret key để định cấu hình AWS CLI.

Kích hoạt CLI của bạn và nhập lệnh sau:

```shell
$ aws configure
AWS Access Key ID [********************]:
AWS Secret Access Key [********************]:
Default region name [us-east-1]:
Default output format [None]:
```

Bạn sẽ được nhắc nhập ID access key AWS, secret key AWS, default region và default output format.

Sau khi định cấu hình thành công AWS CLI, bạn có thể bắt đầu sử dụng nó để quản lý các dịch vụ AWS của mình.

### Các lệnh thường được sử dụng trong AWS CLI.

1. Mô tả một phiên bản ec2.

```shell
aws ec2 describe-instances
```

2. List IAM User.

```shell
aws iam list-users
```
