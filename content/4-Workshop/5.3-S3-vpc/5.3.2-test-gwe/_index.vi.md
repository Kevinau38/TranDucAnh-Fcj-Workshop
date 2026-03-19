---
title : "Bảo vệ Đường dẫn Tùy chỉnh"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 4.3.2. </b> "
---

#### Tổng quan

Phần này triển khai custom AWS WAF rules để bảo vệ các đường dẫn ứng dụng cụ thể khỏi truy cập trái phép. Trước khi giải quyết lỗ hổng bot traffic, chúng ta cần bảo mật các thư mục nhạy cảm chứa file cấu hình và server-side scripts.

---

### Kịch bản Bảo mật

#### Tình huống Thực tế

Website có thư mục `/includes` chứa các file cấu hình và server-side scripts chỉ nên được truy cập bởi server processes. Tuy nhiên, các file này hiện có thể được truy cập trực tiếp từ Internet, tạo ra rủi ro lộ thông tin nhạy cảm như:

- Database credentials
- API keys
- Internal configurations
- Server-side scripts

#### Yêu cầu Bảo mật

- Chặn tất cả requests trực tiếp từ Internet đến thư mục `/includes`
- Áp dụng URL decoding để ngăn chặn các nỗ lực bypass
- Duy trì chức năng ứng dụng hợp lệ
- Không có false positives với traffic bình thường

#### Giải pháp Custom Rule

Sử dụng custom AWS WAF rule để chặn requests có paths bắt đầu bằng `/includes`. Để đảm bảo các requests đã encode (ví dụ: `/inc%6Cudes`) không bị bỏ sót, áp dụng URL decoding transformations trước khi kiểm tra.

---

### Tạo và Cấu hình Custom Rule

#### Bước 1: Truy cập Web ACL và Tạo Rule Mới

Mở phần Web ACL, chọn tab Rules, sau đó click "Add rules" và chọn "Add my own rules and rule groups":

![Tạo custom rule](/images/5-Workshop/5.3-S3-vpc/diagram47.png)

#### Bước 2: Cấu hình Chi tiết Rule

Thiết lập thông tin cơ bản cho rule:

![Cấu hình chi tiết rule](/images/5-Workshop/5.3-S3-vpc/diagram48.png)

**Cấu hình Rule:**
- **Rule type**: Rule builder (visual editor)
- **Name**: path-block
- **Type**: Regular rule (không phải rate-based)

#### Bước 3: Định nghĩa Statement

Cấu hình điều kiện matching cho rule:

![Cấu hình statement](/images/5-Workshop/5.3-S3-vpc/diagram49.png)

**Cấu hình Statement:**
- **If a request**: Matches the statement
- **Inspect**: URI path
- **Match type**: Starts with string
- **String to match**: /includes
- **Text transformation**: URL decode

**Lý do Text Transformation:**
- URL decode transformation xử lý các ký tự đã encode
- Ngăn chặn các nỗ lực bypass như `/inc%6Cudes` hoặc `/%69ncludes`
- Đảm bảo bảo vệ toàn diện

#### Bước 4: Thiết lập Match Action

Định nghĩa action khi rule được kích hoạt:

![Thiết lập block action](/images/5-Workshop/5.3-S3-vpc/diagram50.png)

**Cấu hình Action:**
- **Action**: Block
- **Response**: Default 403 Forbidden
- Click "Add rule" ở cuối trang

---

### Hoàn thành Cấu hình và Xác minh

#### Thiết lập Rule Priority

Trên trang "Set rule priority", thiết lập priority cho custom rule:

![Thiết lập rule priority](/images/5-Workshop/5.3-S3-vpc/diagram51.png)

**Cấu hình Priority:**
- **path-block**: Priority sau managed rules (ví dụ: Priority 2)
- **Lý do**: Managed rules đánh giá trước, custom rules sau
- Click "Save" để hoàn thành

#### Xác nhận Rule Đã Thêm

Quay lại tab Rules và xác minh rule "path-block" đã được liệt kê thành công:

![Xác nhận custom rule](/images/5-Workshop/5.3-S3-vpc/diagram52.png)

**Trạng thái Web ACL:**
- Total rules: 3 (Core Rule Set + SQL Database + path-block)
- Custom rules: 1
- path-block: Active, Priority 2

---

### Xác minh Hiệu quả Bảo vệ

#### Kiểm thử Thủ công

Thực hiện kiểm thử thủ công để xác nhận requests đến thư mục `/includes` trả về 403 Forbidden:

```
curl -I https://d1aty6dsjre298.cloudfront.net/includes/config.php
```

![Kết quả kiểm thử](/images/5-Workshop/5.3-S3-vpc/diagram53.png)

**Kết quả Kiểm thử:**
- **HTTP Status**: 403 Forbidden
- **Server**: CloudFront
- **x-cache**: Error from cloudfront (bị chặn trước origin)
- **Protection**: Đang hoạt động

#### Các Test Cases Bổ sung

Kiểm thử encoded path:

```
curl -I https://d1aty6dsjre298.cloudfront.net/inc%6Cudes/config.php
# Kỳ vọng: 403 Forbidden (URL decode bắt được)
```

Kiểm thử normal path:
```
curl -I https://d1aty6dsjre298.cloudfront.net/
# Kỳ vọng: 200 OK (không bị ảnh hưởng)
```

---

### Phân tích Kỹ thuật và Kết quả

#### Thuật toán String Matching

- **Prefix matching algorithm**: Kiểm tra URI path có bắt đầu bằng `/includes` không
- **URL decoding transformation**: Xử lý ký tự đã encode để ngăn bypass
- **Time complexity**: O(n) cho so sánh string với n là độ dài URI path
- **Space complexity**: O(1) - không gian hằng số

#### Quy trình Text Transformation

1. **Input**: Raw URI path từ HTTP request
2. **Transform**: URL decode (ví dụ: %6C → l)
3. **Match**: So sánh path đã transform với `/includes`
4. **Action**: Block nếu khớp

#### Hiệu quả Bảo mật

- ✅ **Truy cập trực tiếp**: Bị chặn (`/includes/config.php`)
- ✅ **Encoded bypass**: Bị chặn (`/inc%6Cudes/config.php`)
- ✅ **Case variations**: Bị chặn (URL decode chuẩn hóa)
- ✅ **False positives**: Không có (đường dẫn hợp lệ không bị ảnh hưởng)

#### Kết quả Đạt được

- ✅ Bảo vệ thành công thư mục `/includes` khỏi truy cập bên ngoài
- ✅ Ngăn chặn lộ thông tin nhạy cảm (file cấu hình, credentials)
- ✅ Tăng cường bảo mật ứng dụng web tổng thể
- ✅ Không ảnh hưởng đến chức năng ứng dụng hợp lệ

#### Tác động Hiệu suất

- **Latency**: < 1ms mỗi request (string matching)
- **Capacity**: Sử dụng WCU tối thiểu
- **Scalability**: Xử lý lượng request cao

---

### Tóm tắt

**Thành tựu:**
- ✅ Custom rule triển khai thành công để bảo vệ đường dẫn nhạy cảm
- ✅ URL decoding ngăn chặn các nỗ lực bypass
- ✅ Không có false positives với traffic hợp lệ
- ✅ Tác động hiệu suất tối thiểu

**Bước Tiếp theo:**
- Giải quyết lỗ hổng bot traffic thông qua chiến lược bảo vệ bot toàn diện trong phần 4.3.3
