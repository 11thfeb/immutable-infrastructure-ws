---
title : "Tạo user, policy & access key."
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

Trong bước này, chúng ta sẽ cần tạo 1 user test cho bài lab này.

### Tạo user, policy & access key.

1. Đi tới [IAM service management console](https://console.aws.amazon.com/iamv2/home?#/home), nhấp vào nút “Create user” để tạo người dùng của bạn.

![Connect](/immutable-infrastructure/images/3.create-user/iam-console.png)

2. Nhập tên người dùng của bạn và nhấp vào nút “Next” để chuyển sang bước tiếp theo.

![Connect](/immutable-infrastructure/images/3.create-user/specify-user-details.png)

3. Chọn “Attach policies directly”, sau đó bạn có thể tìm kiếm trong thanh tìm kiếm “AdministratorAccess” và “EC2FullAccess”, chọn và nhấp vào nút “Next” để chuyển sang bước tiếp theo.

![Connect](/immutable-infrastructure/images/3.create-user/permission-1.png)

![Connect](/immutable-infrastructure/images/3.create-user/permission-3.png)

4. Bạn có thể xem cấu hình cho tài khoản của mình, nhấp vào nút “Create user” để tạo người dùng của bạn.

![Connect](/immutable-infrastructure/images/3.create-user/review.png)

5. Đi tới [Access Management console](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/users)

![Connect](/immutable-infrastructure/images/3.create-user/create-access-key.png)

6. Chọn “Create access key” để tạo khóa truy cập của bạn.

![Connect](/immutable-infrastructure/images/3.create-user/choose.png)

7. Chọn “Command Line Interface (CLI)”.

![Connect](/immutable-infrastructure/images/3.create-user/accept.png)

8. Chọn “I understand the above recommendation and want to proceed to create an access key” checkbox và click vào “Next” để chuyển sang bước tiếp theo.

![Connect](/immutable-infrastructure/images/3.create-user/input-tag.png)

9. Nhập tên khóa truy cập của bạn và nhấp vào nút “Create access key” để tạo khóa truy cập của bạn.

![Connect](/immutable-infrastructure/images/3.create-user/done.png)

10. Bạn có thể thấy khóa truy cập và khóa bí mật của mình trên màn hình. Bạn nên lưu lại access key và secret key của mình cho bước tiếp theo.
