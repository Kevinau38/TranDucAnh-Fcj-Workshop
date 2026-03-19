---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Triển khai hạ tầng AWS WAF sử dụng CloudFormation.
* Deploy và cấu hình AWS Managed Rules cho bảo vệ OWASP.
* Tạo custom WAF rules cho bảo vệ ứng dụng cụ thể.
* Kiểm thử hiệu quả WAF chống lại các cuộc tấn công web phổ biến.
* Giám sát và phân tích WAF logs và metrics.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tạo CloudFormation template cho hạ tầng WAF. <br> - Deploy S3 bucket, CloudFront distribution, và Lambda function. <br> - Thiết lập ứng dụng web cơ bản để kiểm thử. <br> - Cấu hình CloudWatch logging.                                                                      | 09/03/2026   | 09/03/2026      | <https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/logging.html> |
| 3   | - Tạo AWS WAF Web ACL. <br> - Deploy AWS Managed Rules: <br>&emsp; + Core Rule Set <br>&emsp; + Known Bad Inputs <br>&emsp; + SQL Database <br> - Liên kết Web ACL với CloudFront distribution.                                               | 10/03/2026   | 10/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-creating.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups.html> |
| 4   | - Kiểm thử bảo vệ SQL injection: <br>&emsp; + Tạo các SQL payloads độc hại <br>&emsp; + Xác minh hành vi chặn của WAF <br>&emsp; + Phân tích logs các request bị chặn <br> - Kiểm thử bảo vệ XSS với các vector tấn công khác nhau.                                                    | 11/03/2026   | 11/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-sqli-match.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-xss-match.html> |
| 5   | - Tạo custom WAF rules: <br>   + Rules bảo vệ dựa trên path <br>   + Rules chặn dựa trên IP <br>   + Hạn chế theo vị trí địa lý <br>   + Lọc user-agent <br> - Cấu hình rule priorities và actions.                                 | 12/03/2026   | 12/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rules.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statements.html> |
| 6   | - **Giám sát & Phân tích:** <br>   + Thiết lập CloudWatch dashboards cho WAF metrics. <br>   + Cấu hình phân tích WAF logs. <br>   + Tạo alerts cho các sự kiện bảo mật. <br>   + Tài liệu hóa kết quả kiểm thử và hiệu quả rules.                                  | 13/03/2026   | 13/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/monitoring-cloudwatch.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/logging-management.html> |

### Kết quả đạt được tuần 6:

* **Triển khai thành công hạ tầng WAF:**
  * Tạo CloudFormation template toàn diện cho môi trường workshop.
  * Deploy S3 bucket với cấu hình static website hosting.
  * Thiết lập CloudFront distribution với custom domain và SSL.
  * Cấu hình Lambda function cho việc tạo nội dung động.

* **Triển khai bảo vệ AWS Managed Rules:**
  * Tạo Web ACL với thứ tự đánh giá rules phù hợp.
  * Deploy Core Rule Set cho bảo vệ OWASP Top 10.
  * Cấu hình rule group Known Bad Inputs cho phát hiện payload độc hại.
  * Triển khai rule group SQL Database cho phòng chống tấn công injection.

* **Xác nhận hiệu quả bảo mật qua kiểm thử:**
  * Thực hiện tấn công SQL injection và xác minh hành vi chặn.
  * Kiểm thử XSS payloads trên các vector tấn công khác nhau.
  * Phân tích WAF logs để hiểu các mẫu rule matching.
  * Tài liệu hóa attack signatures và các response actions của WAF.

* **Tạo custom protection rules nâng cao:**
  * Triển khai rules dựa trên path để bảo vệ các thư mục nhạy cảm.
  * Tạo rules chặn dựa trên IP cho các nguồn độc hại đã biết.
  * Cấu hình hạn chế theo vị trí địa lý cho yêu cầu tuân thủ.
  * Thiết lập lọc user-agent để chặn các công cụ tự động.

* **Thiết lập giám sát toàn diện:**
  * Xây dựng CloudWatch dashboards cho WAF metrics thời gian thực.
  * Cấu hình log streaming đến CloudWatch Logs để phân tích.
  * Thiết lập alerts tự động cho các sự kiện bảo mật rủi ro cao.
  * Tạo tài liệu cho quy trình giám sát bảo mật liên tục.
