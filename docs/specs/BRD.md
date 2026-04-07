# Business Requirement Document (BRD) - Hệ thống Giám sát Môi trường ABC

## 🟢 1. Giới thiệu (Overview)
Công ty ABC triển khai hệ thống cảm biến để thu thập dữ liệu ô nhiễm môi trường (nước và không khí). Hệ thống cần một nền tảng Web để hiển thị và trích xuất dữ liệu này.

## 🟢 2. Mục tiêu dự án (Objectives)
1.  **Giám sát trực quan:** Hiển thị tình trạng ô nhiễm không khí trong 24h gần nhất.
2.  **Lưu trữ & Trích xuất:** Đảm bảo dữ liệu được lưu trữ an toàn và có khả năng trích xuất chính xác theo thời điểm lấy mẫu.

## 🟢 3. Phạm vi dự án (Scope)
-   **Đầu vào:** Các file text có cấu trúc gửi từ cảm biến mỗi 5 phút/lần.
-   **Chức năng chính:** Xử lý file, hiển thị Dashboard 24h, tính năng trích xuất dữ liệu.

## 🟢 4. Yêu cầu chi tiết (Requirements)

### 4.1. Yêu cầu về Dữ liệu (Data Requirements)
-   **Định dạng:** File Text có cấu trúc.
-   **Trường thông tin:**
    -   `Sensor ID`: Mã định danh cảm biến.
    -   `Pollution Index`: Chỉ số ô nhiễm (0.00 - 100.00).
-   **Tần suất:** 5 phút/gửi 1 lần về server cố định.

### 4.2. Yêu cầu chức năng (Functional Requirements)
-   **Dashboard 24h:** Hiển thị biểu đồ/trạng thái ô nhiễm không khí từ các điểm thử nghiệm.
-   **Công cụ trích xuất:** Cho phép người dùng chọn thời điểm/cảm biến để lấy báo cáo về tình trạng ô nhiễm nước/không khí.

## 🟢 5. Ràng buộc & Giả định (Constraints & Assumptions)
-   Dữ liệu được gửi về một Server cố định đặt tại văn phòng Công ty ABC.
-   Hệ thống Web cần khả năng đọc và xử lý file text định kỳ.
