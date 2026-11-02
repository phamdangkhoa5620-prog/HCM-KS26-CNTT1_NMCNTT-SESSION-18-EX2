## 1\. Phân tích

### 1.1. Persistent Cookies và Session Cookies

* **Session Cookies:** Bị xóa khi đóng trình duyệt, phải đăng nhập lại.
* **Persistent Cookies:** Lưu trong thời gian quy định, giúp duy trì đăng nhập sau khi đóng trình duyệt.

**Giải pháp:** Sử dụng Persistent Cookies để ghi nhớ phiên đăng nhập và giỏ hàng.

### 1.2. So sánh Cache và Cookies

* **Cache (MB/GB):** Lưu hình ảnh, CSS, JavaScript để tăng tốc độ tải trang.
* **Cookies (\~4KB):** Lưu Token và thông tin phiên đăng nhập.

**Kết luận:** Cache tăng tốc website, Cookies duy trì trạng thái người dùng.

## 2\. Triển khai

### 2.1. Cấu trúc Cookie

```http
Set-Cookie: session\_token=abc123xyz; Max-Age=604800; Path=/; HttpOnly; Secure; SameSite=Lax
```

**Ý nghĩa:**

* `session\_token`: Token xác thực.
* `Max-Age=604800`: Có hiệu lực 7 ngày.
* `HttpOnly`: Ngăn JavaScript truy cập Cookie.
* `Secure`: Chỉ gửi qua HTTPS.
* `SameSite=Lax`: Hạn chế gửi Cookie trong yêu cầu liên trang.

### 2.2. Bảo mật

* Không lưu mật khẩu trực tiếp trong Cookie.
* Dùng Token ngẫu nhiên, khó đoán.
* Bật `HttpOnly`, `Secure`.
* Khi đăng xuất, xóa Cookie và thu hồi phiên trên Server.

## 3\. Kiểm thử

Nếu giao diện vẫn hiển thị màu cũ do Cache, thực hiện **Hard Reload**:

* Windows: `Ctrl + Shift + R` hoặc `Ctrl + F5`.
* macOS: `Cmd + Shift + R`.

Trình duyệt sẽ tải lại tài nguyên thay vì sử dụng Cache cũ.

