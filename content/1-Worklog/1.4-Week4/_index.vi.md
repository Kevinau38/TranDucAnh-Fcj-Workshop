---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu tuần 4:

* Học AWS IAM fundamentals.
* Hiểu users, groups, và roles.
* Nắm vững policies và permissions.
* Thực hành MFA setup và security best practices.
* Hiểu nguyên tắc least privilege.
* Thực hành: Xây dựng môi trường multi-user bảo mật.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học IAM fundamentals và các khái niệm. <br> - Hiểu IAM users và groups. <br> - Nghiên cứu authentication vs authorization. <br> - Học về access keys và console access.                                                                      | 02/02/2026   | 02/02/2026      | <https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html> <br> <https://docs.aws.amazon.com/prescriptive-guidance/latest/modernization-net-applications-security/authentication.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html>            |
| 3   | - Học khái niệm IAM roles. <br> - Hiểu các loại policy (managed vs inline). <br> - Nghiên cứu cấu trúc và cú pháp policy. <br> - Học về trust policies.                                               | 03/02/2026   | 03/02/2026      | <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-custom.html> |
| 4   | - Học MFA (Multi-Factor Authentication). <br> - Hiểu password policies. <br> - Nghiên cứu nguyên tắc least privilege. <br> - Học về IAM best practices.                                                    | 04/02/2026   | 04/02/2026      | <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started-reduce-permissions.html> <br> <https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html> |
| 5   | - **Thực hành:** Tạo IAM infrastructure: <br>   + Tạo IAM users với console access. <br>   + Tạo IAM groups (Admin, Developer, ReadOnly, S3-Users, EC2-Users, VPC-Users). <br>   + Gắn managed policies vào groups. <br>   + Thiết lập MFA cho users. <br>   + Cấu hình password policy. <br>   + Tạo IAM role cho EC2.                                 | 05/02/2026   | 05/02/2026      | <https://docs.aws.amazon.com/network-manager/latest/infrastructure-performance/identity-access-management.html> |
| 6   | - **Dự án thực hành:** Xây dựng môi trường multi-user bảo mật: <br>   + Tạo 6 user groups với permissions khác nhau. <br>   + Tạo nhiều IAM users và gán vào groups. <br>   + Triển khai least privilege access. <br>   + Thiết lập cross-service access sử dụng roles.                                  | 06/02/2026   | 06/02/2026      |  |


### Kết quả đạt được tuần 4:

* **Hiểu AWS IAM fundamentals:**
  * Học kiến trúc IAM và các thành phần.
  * Hiểu users, groups, và roles.
  * Học các khái niệm authentication vs authorization.
  * Hiểu access keys và các phương thức console access.

* **Tích lũy chuyên môn về IAM policies:**
  * Hiểu các loại policy (managed vs inline).
  * Học cấu trúc policy và cú pháp JSON.
  * Hiểu trust policies và assume role.
  * Triển khai các thực hành tốt nhất về policy.

* **Tạo thành công IAM infrastructure:**
  * Tạo IAM users với console access.
  * Tạo IAM groups (Admin, Developer, ReadOnly, S3-Users, EC2-Users, VPC-Users).
  * Gắn managed policies vào groups.
  * Thiết lập MFA cho users.
  * Cấu hình password policy.
  * Tạo IAM role cho EC2.

* **Xây dựng môi trường multi-user bảo mật:**
  * Tạo 6 user groups với permissions khác nhau.
  * Tạo nhiều IAM users và gán vào groups.
  * Triển khai least privilege access.
  * Thiết lập cross-service access sử dụng roles.

* **Phát triển kỹ năng AWS security nền tảng** bao gồm identity management, access control, và security auditing.
