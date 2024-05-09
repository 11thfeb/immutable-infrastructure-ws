+++
title = "Clean up resources"
date = 2022
weight = 8
chapter = false
pre = "<b>8. </b>"
+++

We will take the following this step to delete the resources we created in this exercise.

```shell
## Destroy previously-created infrastructure
terraform destroy
```

Enter "Yes".

![Connect](/immutable-infrastructure/images/8.cleanup/success.png)

#### Check EC2 Instance

1. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)

![Connect](/immutable-infrastructure/images/8.cleanup/ec2.png)

#### Check Auto Scaling Group

![Connect](/immutable-infrastructure/images/8.cleanup/auto-scaling.png)

#### Check Load Balancers
![Connect](/immutable-infrastructure/images/8.cleanup/load-balancer.png)

#### Check Target Groups
![Connect](/immutable-infrastructure/images/8.cleanup/target-group.png)