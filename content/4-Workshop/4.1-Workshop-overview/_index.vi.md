---
title : "Giới thiệu"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

#### Giới thiệu AWS WAF

**AWS Web Application Firewall (WAF)** là dịch vụ tường lửa ứng dụng web cung cấp khả năng phòng thủ cho các ứng dụng web và API để bảo vệ chúng khỏi các cuộc tấn công web phổ biến có thể ảnh hưởng đến tính khả dụng và tiêu tốn quá nhiều tài nguyên.

Một ứng dụng web được bảo mật theo chiều sâu với tường lửa ứng dụng web. Cụ thể, WAF có thể ngăn chặn kẻ tấn công khai thác các lỗ hổng phổ biến trong OWASP Top 10, chẳng hạn như [SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection) và [Cross-Site Scripting](https://owasp.org/www-community/attacks/xss/). Hơn nữa, bạn có thể tạo các rules tùy chỉnh trong WAF để lọc hoặc chặn lưu lượng HTTP(S) đến hoặc đi.

#### Các Tính năng Chính của AWS WAF

+ **Managed Rules**: Các nhóm rules được cấu hình sẵn do AWS và các nhà cung cấp AWS Marketplace duy trì để bảo vệ chống lại các mối đe dọa phổ biến.
+ **Custom Rules**: Tạo các rules của riêng bạn để khớp với các mẫu cụ thể trong web requests và kiểm soát cách chúng được xử lý.
+ **Bot Control**: Xác định và quản lý lưu lượng bot để bảo vệ ứng dụng của bạn khỏi các mối đe dọa tự động.
+ **Rate Limiting**: Kiểm soát tốc độ requests từ các địa chỉ IP cụ thể để ngăn chặn lạm dụng và tấn công DDoS.
+ **Real-time Visibility**: Giám sát và phân tích các mẫu lưu lượng web bằng cách sử dụng AWS WAF logs và metrics.

#### Tổng quan Workshop

Trong workshop này, bạn sẽ học cách:

+ Triển khai và cấu hình **AWS WAF** để bảo vệ ứng dụng web được lưu trữ trên AWS.
+ Triển khai **AWS Managed Rules** để phòng thủ chống lại các cuộc tấn công web phổ biến như SQL injection và XSS.
+ Tạo **custom security rules** để bảo vệ các đường dẫn và endpoints cụ thể của ứng dụng.
+ Cấu hình **Bot Control** để xác định và chặn lưu lượng tự động độc hại.
+ Thiết lập **rate limiting** để ngăn chặn lạm dụng và cạn kiệt tài nguyên.
+ Giám sát các sự kiện bảo mật bằng cách sử dụng **AWS CloudWatch** và phân tích WAF logs.

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)