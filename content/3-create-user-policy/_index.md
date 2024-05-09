---
title : "Create user, policy & access key"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

In this step, we will create a user for this lab

### Create user, policy & access key.

1. Go to [IAM service management console](https://console.aws.amazon.com/iamv2/home?#/home), click “Create user” button to create your user.

![Connect](/immutable-infrastructure/images/3.create-user/iam-console.png)

2. Input your user name, and click on the “Next” button to proceed to the next step.

![Connect](/immutable-infrastructure/images/3.create-user/specify-user-details.png)

3. Choose “Attach policies directly”, after that you can search in the search bar “AdministratorAccess” and “EC2FullAccess”, choose it and click on the “Next” button to proceed to the next step.

![Connect](/immutable-infrastructure/images/3.create-user/permission-1.png)

![Connect](/immutable-infrastructure/images/3.create-user/permission-3.png)

4. You can see the configuration for your account in the review tag, click on the “Create user” button to create your user.

![Connect](/immutable-infrastructure/images/3.create-user/review.png)

5. Go to [Access Management console](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/users)

![Connect](/immutable-infrastructure/images/3.create-user/create-access-key.png)

6. Click on the “Create access key” button to create your access key.

![Connect](/immutable-infrastructure/images/3.create-user/choose.png)

7. Click on the “Command Line Interface (CLI)”.

![Connect](/immutable-infrastructure/images/3.create-user/accept.png)

8. Choose “I understand the above recommendation and want to proceed to create an access key” checkbox and “Next” button to proceed to the next step.

![Connect](/immutable-infrastructure/images/3.create-user/input-tag.png)

9. Input your access key name and click “Create access key” button to create your access key.

![Connect](/immutable-infrastructure/images/3.create-user/done.png)

10. You can see your acesskey and secret key in the screen. You should save your access key and secret key for the next step.