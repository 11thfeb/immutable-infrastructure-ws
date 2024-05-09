---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
## Tại sao sử dụng Immutable Servers?

Cộng đồng DevOps đã chấp nhận khái niệm Immutable Server với lý do chính đáng. Immutable servers được triển khai hoàn toàn bằng các công cụ tự động hóa, và một DevOps không cần phải truy cập vào máy chủ để tự cấu hình nó bằng cách thủ công. Điều này dẫn đến hệ thống dễ dự đoán được - cách mà một máy chủ được cấu hình có thể được dự đoán gần như chính xác bằng những gì có trong bản kiểm soát mã nguồn của bạn (Source Control). Immutable servers triển khai nhanh hơn, vì máy tính có thể thao tác nhanh hơn con người.

Chúng cũng có thể an toàn hơn. Khi máy chủ dự đoán và nhanh chóng triển khai lại, các sysadmin không cần có nhiều động cơ để chúng chạy trong thời gian dài. Nếu bạn thường xuyên triển khai lại các máy chủ hàng ngày (hoặc thậm chí hàng giờ, trong trường hợp của một số công ty triển khai nhiều lần trong một ngày), thì một kẻ xâm nhập nào đó có thể không có nhiều thời gian để thiết lập và khám phá. Các máy chủ chạy lâu là một rủi ro: việc xâm nhập vào Equifax đã xảy ra trong khoảng thời gian 76 ngày. Immutable servers với tuổi thọ ngắn là một phần quan trọng của một chiến lược phòng ngự chặt chẽ.

![ConnectPrivate](/immutable-infrastructure/images/1.introduction/packer-ansible-terraform.png)

## Công cụ DevOps là gì?

Có nhiều cách tiếp cận để tạo ra các máy chủ bất biến. Khi tham gia dự án hiện tại của mình tại công ty, tôi đã gặp phải một ngăn xếp mới được sử dụng để tạo các immutable servers trong GovCloud của Amazon Web Services (AWS). Khi đã quen với Terraform, trước đây tôi chưa từng sử dụng Packer hoặc Ansible. Bây giờ tôi đã dành phần lớn thời gian trong năm để làm việc với hệ thống này. Mặc dù việc thiết lập ngăn xếp hơi phức tạp (ít nhất là so với mô hình "bash script chạy trên các nút mới") nhưng độ tin cậy, tốc độ triển khai nhanh và khả năng hiển thị mà ngăn xếp này mang lại khiến cho công sức thiết lập ban đầu trở nên xứng đáng.

## Packer

[https://www.packer.io](https://www.packer.io/)

Packer là sản phẩm của Hashicorp. Theo cách nói của họ, “Packer là một công cụ nguồn mở để tạo các images giống hệt nhau cho nhiều nền tảng từ một cấu hình nguồn duy nhất”. Tôi sử dụng Packer để lấy Hình ảnh máy Amazon (AMI) nhằm tạo ra các phiên bản mới của những AMI này có tất cả cấu hình và phần mềm mà chúng tôi cần để chạy ứng dụng của mình một cách an toàn trong AWS.

Packer hỗ trợ nhiều “provisioners xử lý cấu hình máy chủ thực tế. Đây có thể là các tập lệnh shell đơn giản hoặc có thể là một công cụ mạnh mẽ hơn như Ansible. Packer xử lý việc tạo VM và đóng gói dưới dạng AMI, Ansible xử lý cấu hình của máy ảo.

## Ansible

[https://www.ansible.com](https://www.ansible.com/)

Ansible được Red Hat tạo ra như một công cụ quản lý cấu hình. Nó tự động hóa tất cả cài đặt phần mềm, quản lý gói và cấu hình trên máy chủ AWS EC2 của chúng tôi. Ansible đảm bảo rằng mọi phần mềm, thay đổi tệp cấu hình hoặc công việc định kỳ đều được cài đặt theo cùng một cách.

Ansible không có tác nhân, vì vậy chuỗi công cụ xây dựng của bạn có ít bộ phận chuyển động hơn. (Có lẽ phần tồi tệ nhất của DevOps là trở thành quản trị viên hệ thống cho các công cụ bạn xây dựng để thay thế bạn làm quản trị viên hệ thống.) Cú pháp YAML thật đáng kinh ngạc và được ghi chép đầy đủ. Hệ sinh thái Ansible Galaxy có rất nhiều sách hướng dẫn cho tất cả các loại nhiệm vụ quản lý máy chủ, từ việc triển khai máy chủ Apache [tuân thủ các nguyên tắc bảo mật hệ thống](https://madeintandem.com/blog/automating-security-compliance-ansible-devsecops-made-easy/).

## Terraform

https://www.terraform.io/

Terraform là một sản phẩm của Hashicorp. Nó cho phép chúng tôi “tạo, thay đổi và cải thiện cơ sở hạ tầng một cách an toàn và có thể dự đoán được”. Thuật ngữ cơ sở hạ tầng đề cập đến các thành phần như phiên bản EC2, bộ cân bằng tải, cơ sở dữ liệu và kết nối mạng. Terraform tích hợp với API AWS để dịch và chạy mã cấu hình thành các lệnh gọi API AWS nhằm cung cấp kiến ​​trúc của chúng tôi – mọi thứ từ kết nối mạng đến máy chủ ứng dụng và bộ chứa S3. Sau khi tạo AMI bằng Packer và Ansible, chúng tôi sẽ sử dụng Terraform để triển khai AMI đó dưới dạng phiên bản EC2 vào môi trường đám mây của mình.