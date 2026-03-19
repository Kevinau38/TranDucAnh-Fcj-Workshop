---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Học kiến thức cơ bản về AWS WAF và các khái niệm bảo mật ứng dụng web.
* Hiểu OWASP Top 10 vulnerabilities và các chiến lược giảm thiểu.
* Nghiên cứu các thành phần AWS WAF: Web ACLs, Rules, và Rule Groups.
* Tìm hiểu AWS Managed Rules và tạo custom rules.
* Bắt đầu lên kế hoạch triển khai workshop AWS WAF.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Học kiến thức cơ bản và kiến trúc AWS WAF. <br> - Hiểu các mối đe dọa bảo mật ứng dụng web. <br> - Nghiên cứu WAF vs tường lửa truyền thống. <br> - Học về giá cả và mô hình triển khai AWS WAF.                                                                      | 02/03/2026   | 02/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/how-aws-waf-works.html> |
| 3   | - Nghiên cứu OWASP Top 10 vulnerabilities: <br>&emsp; + SQL Injection <br>&emsp; + Cross-Site Scripting (XSS) <br>&emsp; + Broken Authentication <br>&emsp; + Security Misconfiguration <br> - Học các chiến lược giảm thiểu cho từng vulnerability.                                               | 03/03/2026   | 03/03/2026      | <https://owasp.org/www-project-top-ten/> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html> |
| 4   | - Học các thành phần AWS WAF: <br>&emsp; + Web ACLs (Access Control Lists) <br>&emsp; + Rules và Rule Groups <br>&emsp; + Conditions và Statements <br> - Hiểu thứ tự đánh giá rules và các actions.                                                    | 04/03/2026   | 04/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/web-acl.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rules.html> |
| 5   | - Nghiên cứu AWS Managed Rules: <br>   + Core Rule Set (CRS) <br>   + Known Bad Inputs <br>   + SQL Database <br>   + Linux Operating System <br>   + POSIX Operating System <br> - Học về rule group priorities và exceptions.                                 | 05/03/2026   | 05/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups.html> |
| 6   | - **Nghiên cứu:** Lên kế hoạch workshop AWS WAF: <br>   + Xác định phạm vi và mục tiêu workshop. <br>   + Thiết kế các kịch bản thực hành cho các cuộc tấn công phổ biến. <br>   + Lên kế hoạch thiết lập hạ tầng với CloudFormation. <br>   + Phác thảo các bài tập tạo custom rules.                                  | 06/03/2026   | 06/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/getting-started.html> |

### Kết quả đạt được tuần 5:

* **Nắm vững kiến thức cơ bản AWS WAF:**
  * Hiểu kiến trúc WAF và các mô hình triển khai.
  * Học cách AWS WAF tích hợp với CloudFront, ALB, và API Gateway.
  * Nghiên cứu sự khác biệt giữa WAF và tường lửa truyền thống.
  * Hiểu cấu trúc giá AWS WAF và tối ưu hóa chi phí.

* **Tích lũy kiến thức sâu về bảo mật ứng dụng web:**
  * Nghiên cứu chi tiết OWASP Top 10 vulnerabilities.
  * Học các vector tấn công SQL injection và cách phòng chống.
  * Hiểu các loại tấn công XSS và chiến lược giảm thiểu.
  * Khám phá các kỹ thuật bypass authentication và biện pháp đối phó.

* **Tích lũy chuyên môn về các thành phần AWS WAF:**
  * Học cấu trúc và cấu hình Web ACL.
  * Hiểu các loại rules: rate-based, regular, và group rules.
  * Nghiên cứu logic đánh giá rules và thứ tự ưu tiên actions.
  * Học về rule conditions và match statements.

* **Khám phá AWS Managed Rules:**
  * Nghiên cứu Core Rule Set cho bảo vệ OWASP Top 10.
  * Học khả năng của rule group Known Bad Inputs.
  * Hiểu SQL Database và các rule groups dành riêng cho OS.
  * Khám phá tùy chỉnh rule group và xử lý exceptions.

* **Lên kế hoạch workshop AWS WAF toàn diện:**
  * Xác định mục tiêu học tập và kết quả đầu ra của workshop.
  * Thiết kế các kịch bản tấn công thực tế cho học tập thực hành.
  * Lên kế hoạch tự động hóa hạ tầng với CloudFormation.
  * Phác thảo các cấp độ khó tăng dần cho bài tập tạo rules.
