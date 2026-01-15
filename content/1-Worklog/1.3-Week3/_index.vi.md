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
* Hiểu Internet Gateway và NAT Gateway.
* Thực hành cấu hình VPC và subnets.
* Hiểu các thực hành tốt nhất về network security.
* Thực hành: Xây dựng kiến trúc mạng multi-tier.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học cơ bản VPC và các khái niệm. <br> - Hiểu CIDR blocks và IP addressing. <br> - Học về subnets (public vs private). <br> - Nghiên cứu route tables và routing.                                                                      | 26/01/2026   | 26/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-cidr-blocks.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html>           |
| 3   | - Học khái niệm Security Groups. <br> - Hiểu Network ACLs (NACLs). <br> - So sánh Security Groups vs NACLs. <br> - Nghiên cứu stateful vs stateless filtering.                                               | 27/01/2026   | 27/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html> <br> <https://tutorialsdojo.com/understanding-security-groups-and-network-access-control-lists-nacls-in-aws/> <br> <https://medium.com/@subhampradhan966/aws-security-groups-and-network-access-control-lists-nacls-4add51916150> |
| 4   | - Học khái niệm Internet Gateway. <br> - Hiểu NAT Gateway và NAT Instance. <br> - Nghiên cứu public vs private subnet routing. <br> - Học về Elastic IPs.                                                    | 28/01/2026   | 28/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/route-table-options.html> <br> <https://docs.aws.amazon.com/vpc/latest/userguide/vpc-eip-overview.html> |
| 5   | - **Thực hành:** Tạo hạ tầng VPC cơ bản: <br>   + Tạo custom VPC với CIDR block (10.0.0.0/16). <br>   + Tạo public subnet cho web tier. <br>   + Tạo private subnet cho app tier. <br>   + Cấu hình route tables cho mỗi subnet. <br>   + Thiết lập Internet Gateway và gắn vào VPC. <br>   + Cấu hình NAT Gateway trong public subnet. <br>   + Test kết nối cơ bản.                                 | 29/01/2026   | 29/01/2026      | <https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html> |
| 6   | - **Dự án thực hành:** Mở rộng thành kiến trúc mạng multi-tier: <br>   + Thêm database subnet vào VPC hiện tại. <br>   + Cấu hình subnets trên 2 Availability Zones. <br>   + Tạo Security Groups cho web, app, và database tiers. <br>   + Cấu hình Security Group rules (web → app → database). <br>   + Triển khai EC2 instances trong web tier (public subnet). <br>   + Triển khai EC2 instances trong app tier (private subnet). <br>   + Test kết nối giữa các tiers. <br>   + Xác minh cô lập bảo mật và truy cập internet.                                  | 30/01/2026   | 30/01/2026      | <https://docs.google.com/document/d/1nwBTqOeRZsW1ho1h78MJtGFqTB6Y77_IRJ-lFG3-rMQ/edit?usp=sharing> |


### Kết quả đạt được tuần 3:

* **Hiểu các khái niệm AWS VPC networking:**
  * Học kiến trúc VPC và các thành phần.
  * Hiểu CIDR blocks và IP addressing schemes.
  * Học cấu hình public và private subnets.
  * Hiểu route tables và cơ chế routing.

* **Tích lũy chuyên môn về network security:**
  * Hiểu Security Groups và tính chất stateful.
  * Học Network ACLs và stateless filtering.
  * Hiểu sự khác biệt giữa Security Groups và NACLs.
  * Triển khai phương pháp bảo mật nhiều lớp.
  * Cấu hình inbound và outbound rules hiệu quả.

* **Tạo thành công hạ tầng VPC cơ bản:**
  * Tạo custom VPC với CIDR block 10.0.0.0/16.
  * Cấu hình public subnet cho web tier.
  * Cấu hình private subnet cho app tier.
  * Thiết lập Internet Gateway và gắn vào VPC.
  * Cấu hình NAT Gateway trong public subnet cho private subnet internet access.
  * Cấu hình route tables để điều hướng traffic đúng cách.
  * Test kết nối cơ bản giữa các subnets.

* **Mở rộng VPC thành kiến trúc mạng multi-tier:**
  * Thêm database subnet vào hạ tầng VPC hiện tại.
  * Cấu hình subnets trên 2 Availability Zones cho high availability.
  * Tạo Security Groups cho web, app, và database tiers.
  * Cấu hình Security Group rules cho giao tiếp giữa các tiers (web → app → database).
  * Triển khai EC2 instances trong web tier (public subnet).
  * Triển khai EC2 instances trong app tier (private subnet).
  * Test kết nối giữa các tiers.
  * Xác minh cô lập bảo mật và truy cập internet đúng cách.
  * Triển khai kiến trúc multi-tier với phân đoạn mạng phù hợp.

* **Phát triển kỹ năng AWS networking nền tảng** bao gồm thiết kế VPC, lập kế hoạch subnet, cấu hình bảo mật, và triển khai kiến trúc multi-tier.
