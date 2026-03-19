---
title : "Khắc Phục"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 4.3. </b> "
---

#### Tổng quan

Trong phần này, bạn sẽ triển khai các biện pháp bảo mật toàn diện để bảo vệ ứng dụng web của mình bằng AWS WAF. Quá trình khắc phục được chia thành nhiều giai đoạn, mỗi giai đoạn giải quyết các vấn đề bảo mật cụ thể.

#### Các Giai đoạn Khắc phục

Phần này bao gồm việc triển khai bảo mật hoàn chỉnh từ hoàn thiện hạ tầng đến các cơ chế bảo vệ nâng cao:

**Giai đoạn 1: Hoàn thiện Hạ tầng & Managed Rules**
- Hoàn thiện thiết lập hạ tầng ứng dụng
- Triển khai AWS Managed Rules để bảo vệ chống lại các mối đe dọa phổ biến
- Xác minh bảo mật cơ bản với bảo vệ SQL injection và XSS

**Giai đoạn 2: Bảo vệ Đường dẫn Tùy chỉnh**
- Tạo custom rules để bảo vệ các đường dẫn ứng dụng cụ thể
- Chặn truy cập trái phép vào các thư mục nhạy cảm
- Triển khai kiểm soát bảo mật dựa trên URL

**Giai đoạn 3: Quản lý Lưu lượng Bot**
- Giám sát các mẫu lưu lượng bot bằng regex pattern sets
- Xác định hành vi bot hợp pháp và độc hại
- Triển khai các cơ chế kiểm soát bot

**Giai đoạn 4: Chặn Bad Bots**
- Tạo custom rules để chặn các bot độc hại đã biết
- Sử dụng phát hiện dựa trên user-agent
- Ngăn chặn các cuộc tấn công tự động và scraping

**Giai đoạn 5: Giới hạn Tốc độ**
- Triển khai rate-based rules để ngăn chặn lạm dụng
- Bảo vệ chống lại các cuộc tấn công DDoS
- Kiểm soát tốc độ requests từ các địa chỉ IP cụ thể

**Giai đoạn 6: Xác thực Tham số API**
- Xác thực các tham số query API bằng regex patterns
- Ngăn chặn các cuộc tấn công thao túng tham số
- Đảm bảo tính toàn vẹn dữ liệu cho các API endpoints

#### Kiến trúc Bảo mật

Quá trình khắc phục triển khai phương pháp defense-in-depth với nhiều lớp bảo mật:

1. **Lớp Managed Rules**: Các rules do AWS duy trì cho các lỗ hổng phổ biến
2. **Lớp Custom Rules**: Các rules bảo vệ cụ thể cho ứng dụng
3. **Lớp Bot Control**: Phát hiện và chặn mối đe dọa tự động
4. **Lớp Rate Limiting**: Ngăn chặn lạm dụng và bảo vệ DDoS
5. **Lớp Input Validation**: Xác thực tham số API và dữ liệu

#### Kết quả Kỳ vọng

Đến cuối phần này, bạn sẽ có:

- ✅ Ứng dụng web hoạt động đầy đủ với bảo vệ WAF toàn diện
- ✅ AWS Managed Rules bảo vệ chống lại các lỗ hổng OWASP Top 10
- ✅ Custom rules bảo vệ các đường dẫn ứng dụng nhạy cảm
- ✅ Cơ chế bot control xác định và chặn các bot độc hại
- ✅ Rate limiting ngăn chặn lạm dụng và cạn kiệt tài nguyên
- ✅ Xác thực tham số API đảm bảo tính toàn vẹn dữ liệu
- ✅ CloudWatch metrics giám sát các sự kiện bảo mật theo thời gian thực

#### Nội dung

1. [Hoàn thiện Hạ tầng & Managed Rules](4.3.1-managed-rules/)
2. [Bảo vệ Đường dẫn Tùy chỉnh](4.3.2-custom-path/)
3. [Giám sát Lưu lượng Bot](4.3.3-bot-monitoring/)
4. [Chặn Bad Bots](4.3.4-block-bots/)
5. [Giới hạn Tốc độ](4.3.5-rate-limiting/)
6. [Xác thực Tham số API](4.3.6-api-validation/)