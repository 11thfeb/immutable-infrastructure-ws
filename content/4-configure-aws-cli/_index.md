---
title : "Configure AWS CLI"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

In the previous step, you created an account and obtained an access key and secret key. In this step, you need to use the access key and secret key to configure the AWS CLI.

Fire up your CLI and enter the following command:

```shell
$ aws configure
AWS Access Key ID [********************]:
AWS Secret Access Key [********************]:
Default region name [us-east-1]:
Default output format [None]:
```

You will be prompted to enter your AWS Access Key ID, AWS Secret Access Key, Default region name, and Default output format.

After you have successfully configured AWS CLI, you can start using it to manage your AWS services.

### Commands Frequently Used in AWS CLI.

1. To describe the EC2 instance.

```shell
aws ec2 describe-instances
```

2. To list all the IAM user.

```shell
aws iam list-users
```