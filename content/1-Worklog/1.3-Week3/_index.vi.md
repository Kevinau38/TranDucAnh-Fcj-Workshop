---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu tuần 3:

* Học AWS VPC và các khái niệm networking.
* Hiểu Security Groups và Network ACLs.
* Nắm vững Internet Gateway và NAT Gateway.
* Thực hành cấu hình VPC và subnets.
* Hiểu các thực hành tốt nhất về network security.
* Thực hành: Xây dựng kiến trúc mạng multi-tier.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học cơ bản VPC và các khái niệm. <br> - Hiểu CIDR blocks và IP addressing. <br> - Học về subnets (public vs private). <br> - Nghiên cứu route tables và routing.                                                                      | 26/01/2026   | 26/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html>           |
| 3   | - Học khái niệm Security Groups. <br> - Hiểu Network ACLs (NACLs). <br> - So sánh Security Groups vs NACLs. <br> - Nghiên cứu stateful vs stateless filtering.                                               | 27/01/2026   | 27/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html> |
| 4   | - Học khái niệm Internet Gateway. <br> - Hiểu NAT Gateway và NAT Instance. <br> - Nghiên cứu public vs private subnet routing. <br> - Học về Elastic IPs.                                                    | 28/01/2026   | 28/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html> |
| 5   | - **Thực hành:** Thiết lập và cấu hình VPC: <br>   + Tạo custom VPC với CIDR block. <br>   + Tạo public và private subnets. <br>   + Cấu hình route tables. <br>   + Thiết lập Internet Gateway. <br>   + Cấu hình NAT Gateway. <br>   + Test kết nối giữa các subnets.                                 | 29/01/2026   | 29/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-getting-started.html> |
| 6   | - **Dự án thực hành:** Xây dựng kiến trúc mạng multi-tier: <br>   + Thiết kế kiến trúc 3-tier (web, app, database). <br>   + Tạo VPC với nhiều subnets trên các AZs. <br>   + Cấu hình public subnets cho web tier. <br>   + Cấu hình private subnets cho app và database tiers. <br>   + Thiết lập Internet Gateway cho public access. <br>   + Cấu hình NAT Gateway cho private subnet internet access. <br>   + Tạo và cấu hình Security Groups cho mỗi tier. <br>   + Thiết lập Network ACLs cho bảo mật bổ sung. <br>   + Triển khai EC2 instances trong mỗi tier. <br>   + Test kết nối end-to-end và bảo mật.                                  | 30/01/2026   | 30/01/2026      |  |


### Kết quả đạt được tuần 3:

* **Hiểu các khái niệm AWS VPC networking:**
  * Học kiến trúc VPC và các thành phần.
  * Hiểu CIDR blocks và IP addressing schemes.
  * Học cấu hình public và private subnets.
  * Hiểu route tables và cơ chế routing.
  * Học về VPC peering và các tùy chọn kết nối.

* **Tích lũy chuyên môn về network security:**
  * Hiểu Security Groups và tính chất stateful.
  * Học Network ACLs và stateless filtering.
  * Hiểu sự khác biệt giữa Security Groups và NACLs.
  * Triển khai phương pháp bảo mật nhiều lớp.
  * Cấu hình inbound và outbound rules hiệu quả.

* **Cấu hình thành công Internet connectivity:**
  * Thiết lập Internet Gateway cho public subnet access.
  * Cấu hình NAT Gateway cho private subnet internet access.
  * Hiểu Elastic IP allocation và quản lý.
  * Học routing cho internet-bound traffic.
  * Triển khai các mẫu kết nối internet bảo mật.

* **Xây dựng kiến trúc mạng multi-tier:**
  * Thiết kế và triển khai kiến trúc 3-tier.
  * Tạo VPC với nhiều subnets trên các availability zones.
  * Cấu hình web tier trong public subnets với internet access.
  * Thiết lập app và database tiers trong private subnets.
  * Triển khai security group rules phù hợp cho mỗi tier.
  * Cấu hình Network ACLs cho lớp bảo mật bổ sung.
  * Triển khai và test EC2 instances trong mỗi tier.
  * Xác minh kết nối end-to-end và cô lập bảo mật.
  * Triển khai high availability và fault tolerance.

* **Phát triển kỹ năng AWS networking nền tảng** bao gồm thiết kế VPC, lập kế hoạch subnet, cấu hình bảo mật, và triển khai kiến trúc multi-tier.
