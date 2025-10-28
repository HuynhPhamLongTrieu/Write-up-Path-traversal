## 🔐 Câu 1: Path Traversal (Simple) — Đọc /etc/passwd
### 🎯 Mục tiêu
Khai thác lỗ hổng Path Traversal tại tham số filename để đọc nội dung tệp hệ thống /etc/passwd.
<div align="center">
  <img src="img/img1.jpg" alt="Giao diện trang web - Điểm tấn công path traversal" width="600">
  <br>
  <em>Hình 1: Giao diện trang web và các điểm có thể bị tấn công Path Traversal</em>
</div>
### 🔍 Quá trình thực hiện

#### 🔸 Bước 1: Truy cập trang lab, mở Burp Suite để bắt request liên quan hình ảnh (điều chỉnh Filter settings để thấy các request tĩnh).
Giao diện Burp suite
<div align="center">
  <img src="img/img2.jpg" alt="Minh họa" width="600">
  <br>
  <em>Hình 2: Minh họa kết quả</em>
</div>
Điều chỉnh filter trong Burp suite
<div align="center">
  <img src="img/img3.jpg" alt="Minh họa" width="600">
  <br>
  <em>Hình 3: Minh họa kết quả</em>
</div>

#### 🔸 Bước 2: Xác định tham số dễ tổn thương
- ✅ Tìm request kiểu: GET /image?filename=24.jpg HTTP/2.
- ✅ Suy luận: nếu server nối filename vào đường dẫn thư mục ảnh mà không chuẩn hóa, có thể dùng ../ để “chui” ra ngoài.
<div align="center">
  <img src="img/img5.jpg" alt="Minh họa" width="600">
  <br>
  <em>Hình 4: Kết quả trả về</em>
</div>

> **📊 Kết quả:**
- ✅ Xuất hiện phản hồi chứa dòng kiểu root:x:0:0:root:/root:/bin/bash → chứng tỏ đọc được /etc/passwd

### 🎯 Kết luận
> ⚠️ **Cảnh báo nghiêm trọng:** Đã thành công khai thác lỗ hổng Path Traversal để đọc được /etc/passwd.

---

