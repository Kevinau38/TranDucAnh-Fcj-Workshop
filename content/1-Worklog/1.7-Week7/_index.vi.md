---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Triển khai các tính năng AWS WAF nâng cao: Bot Control và Rate Limiting.
* Phát triển API parameter validation và cơ chế custom response.
* Tạo tài liệu workshop AWS WAF toàn diện.
* Thực hiện kiểm thử end-to-end và tối ưu hóa hiệu suất.
* Hoàn thiện tài liệu workshop và chuẩn bị triển khai.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Triển khai cơ chế Bot Control: <br> - Cấu hình regex pattern sets cho phát hiện bot. <br> - Thiết lập giám sát và phân tích bot traffic. <br> - Tạo rules chặn bot độc hại trong khi cho phép bot hợp lệ.                                                                      | 16/03/2026   | 16/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-bot-control.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-regex-pattern-set-match.html> |
| 3   | - Cấu hình bảo vệ Rate Limiting: <br>&emsp; + Thiết lập rate-based rules cho bảo vệ DDoS <br>&emsp; + Cấu hình rate limiting dựa trên IP <br>&emsp; + Triển khai geographic rate controls <br> - Kiểm thử hiệu quả rate limiting với các công cụ load testing.                                               | 17/03/2026   | 17/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-rate-based.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-geo-match.html> |
| 4   | - Phát triển API parameter validation: <br>&emsp; + Tạo rules cho query parameter validation <br>&emsp; + Triển khai business logic constraints <br>&emsp; + Cấu hình custom HTTP response codes <br> - Kiểm thử API validation với các kịch bản input khác nhau.                                                    | 18/03/2026   | 18/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-size-constraint-match.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-custom-request-response.html> |
| 5   | - **Tài liệu Workshop:** <br>   + Tạo hướng dẫn workshop toàn diện <br>   + Tài liệu hóa tất cả các bước cấu hình với screenshots <br>   + Chuẩn bị bài tập thực hành và lời giải <br>   + Tạo hướng dẫn troubleshooting và phần FAQ.                                 | 19/03/2026   | 19/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/getting-started.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html> |
| 6   | - **Kiểm thử & Tối ưu hóa cuối cùng:** <br>   + Thực hiện walkthrough workshop end-to-end <br>   + Thực hiện kiểm thử bảo mật và xác nhận <br>   + Tối ưu hóa WAF rules cho hiệu suất <br>   + Tạo quy trình cleanup và hướng dẫn quản lý chi phí.                                  | 20/03/2026   | 20/03/2026      | <https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-testing.html> <br> <https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html> |

### Kết quả đạt được tuần 7:

* **Triển khai tính năng Bot Control nâng cao:**
  * Tạo regex pattern sets tinh vi cho nhận diện bot.
  * Cấu hình giám sát bot traffic với phân tích chi tiết.
  * Triển khai chặn bot có chọn lọc trong khi bảo toàn truy cập bot hợp lệ.
  * Phát triển cơ chế phân tích và báo cáo hành vi bot.

* **Triển khai bảo vệ Rate Limiting toàn diện:**
  * Cấu hình rate-based rules cho giảm thiểu tấn công DDoS.
  * Triển khai rate limiting dựa trên IP với ngưỡng động.
  * Thiết lập geographic rate controls cho tuân thủ và bảo mật.
  * Xác nhận hiệu quả rate limiting qua stress testing.

* **Phát triển API parameter validation mạnh mẽ:**
  * Tạo business logic validation rules cho API endpoints.
  * Triển khai query parameter constraints và data type validation.
  * Cấu hình custom HTTP response codes cho validation failures.
  * Kiểm thử API validation trên nhiều kịch bản tấn công và edge cases.

* **Tạo tài liệu workshop toàn diện:**
  * Phát triển hướng dẫn workshop từng bước với giải thích chi tiết.
  * Chụp 118 screenshots tài liệu hóa mọi bước cấu hình.
  * Tạo bài tập thực hành với các cấp độ khó tăng dần.
  * Chuẩn bị hướng dẫn troubleshooting và phần FAQ toàn diện.

* **Hoàn thành kiểm thử và tối ưu hóa cuối cùng:**
  * Thực hiện kiểm thử xác nhận workshop end-to-end đầy đủ.
  * Thực hiện kiểm thử bảo mật toàn diện chống OWASP Top 10.
  * Tối ưu hóa hiệu suất WAF rules và giảm false positives.
  * Tạo quy trình cleanup chi tiết và tài liệu quản lý chi phí.

* **Hoàn thành workshop AWS WAF sẵn sàng triển khai:**
  * Hoàn thiện tài liệu workshop song ngữ (Tiếng Anh/Tiếng Việt).
  * Chuẩn bị CloudFormation templates sẵn sàng triển khai.
  * Tạo hướng dẫn toàn diện cho giảng viên và tài liệu cho học viên.
  * Thiết lập quy trình bảo trì và cập nhật workshop.
