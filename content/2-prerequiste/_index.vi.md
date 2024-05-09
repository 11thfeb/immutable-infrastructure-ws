---
title : "Các bước chuẩn bị"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
Ghi chú: Chúng ta cần bắt đầu và kích hoạt nginx bằng cách sử dụng systemctl start và enable để đảm bảo rằng nginx sẽ sẵn sàng xử lý tự động.
{{% /notice %}}

Trong workshop này, chúng ta sẽ tạo một AMI bằng cách sử dụng Packer và thực hiện cấu hình bằng cách sử dụng Ansible trong quá trình tạo. Một trang web tĩnh sẽ được triển khai. Và cùng một mã Ansible được sử dụng để cung cấp trang web tĩnh bằng cách sử dụng Nginx trong suốt quá trình tạo này. Các thẻ sẽ được gán cho AMI trong quá trình này. Mục đích là để xác định AMI mới nhất có sẵn và sẵn sàng cho việc tạo instance EC2. ID của Subnet sẽ được thu thập để Packer builder có thể tạo AMI bằng ID của Subnet. Ở đây, chúng ta sẽ quản lý mã terraform của mình trong hai phần khác nhau: một phần để tạo VPC, subnet và thông tin mạng khác, phần còn lại để nhóm instance EC2 trong mạng của chúng ta bằng AMI được tạo bởi Packer trước đó.

### Nội dung
- [Cài đặt Packer](/immutable-infrastructure/2.1-install-packer/)
- [Cài đặt Ansible](/immutable-infrastructure/2.2-createiamrole/)
- [Cài đặt AWS CLI](/immutable-infrastructure/2.3-install-aws-cli/)
- [Cài đặt Terraform](/immutable-infrastructure/2.4-install-terraform/)