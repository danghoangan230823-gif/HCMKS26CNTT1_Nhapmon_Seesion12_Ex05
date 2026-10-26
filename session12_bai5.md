# Bài 5 : Chuẩn hóa quy trình báo cáo sự cố an ninh mạng

## Phần 1. Phân tích: Cơ chế "Google Search của bảng tính" (AutoFilter)

Tính năng AutoFilter trong hệ thống nhật ký sự cố NetGuard được ví như "Google Search" nhờ các điểm cốt lõi:

* **Truy vấn tức thời:** Khoanh vùng chính xác địa chỉ IP độc hại, mã độc hoặc thời điểm tấn công trong tích tắc.
* **Lọc đa điều kiện:** Kết hợp nhiều tiêu chí (ví dụ: Critical + Error 404 + Trojan) để cô lập nguồn gốc sự cố nhanh chóng.
* **Phát hiện bất thường:** Nhìn ra xu hướng đột biến của gói tin hoặc lượt truy cập trực tiếp trên giao diện trực quan.

---

## Phần 2. Triển khai: Báo cáo NetGuard hoàn chỉnh

### 1. Xử lý dữ liệu Excel: Hàm VLOOKUP bọc TRIM

* **Vấn đề:** Dữ liệu thô chứa khoảng trắng thừa gây lỗi `#N/A` khi tra cứu.
* **Giải pháp:** Dùng hàm `TRIM` để làm sạch mã định danh trước khi dò tìm.
* **Công thức chuẩn:**
`=VLOOKUP(TRIM(A2), 'Cơ sở dữ liệu virus'!$A$2:$B$500, 2, FALSE)`

### 2. Thiết kế tài liệu Word: Navigation Pane và Auto TOC

* **Navigation Pane:** Sử dụng định dạng `Heading` (1, 2, 3) để bật bảng điều hướng, giúp nhảy đến các mục cấu phần ngay lập tức.
* **Auto TOC:** Tự động cập nhật số trang chính xác cho tài liệu dài qua tính năng *Update Table* mà không cần sửa thủ công.

### 3. Trình bày Slide PowerPoint: Chiến lược phòng thủ 3 tầng

* **Font chữ:** Dùng font không chân hiện đại, nét đều (như Montserrat hoặc Inter) để tối ưu hiển thị trên máy chiếu.
* **Sơ đồ 3 tầng phòng thủ:**
1. **Tầng 1 - Vành đai ngoài (Perimeter Defense):** NGFW, IPS, WAF (chặn DDoS và quét lỗ hổng).
2. **Tầng 2 - Mạng nội bộ & Điểm cuối (Internal & Endpoint):** EDR, phân tách phân vùng mạng, SIEM.
3. **Tầng 3 - Dữ liệu cốt lõi & Sao lưu (Data & Backup):** Mã hóa AES-256, sao lưu lạnh theo nguyên tắc 3-2-1 chống Ransomware.