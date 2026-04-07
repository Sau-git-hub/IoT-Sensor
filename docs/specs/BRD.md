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
-   **Định dạng:** File Text (CSV hoặc Plain Text).
-   **Cấu trúc dòng:** `Timestamp, SensorID, Type (Air/Water), Value`.
-   **Tần suất cập nhật:** 5 phút/lần.

### 4.2. Yêu cầu chức năng (Functional Requirements)
-   **Dashboard 24h:**
    -   Hiển thị biểu đồ đường (Line Chart) diễn biến ô nhiễm không khí.
    -   Cửa sổ thời gian: 24 giờ gần nhất kể từ thời điểm xem.
    -   Khả năng so sánh tối đa 3 Sensor trên cùng một biểu đồ.
    -   Cơ chế cập nhật: Tự động tải lại dữ liệu (Auto-refresh) mỗi 5 phút.
-   **Công cụ trích xuất & Báo cáo:**
    -   Tìm kiếm dữ liệu theo Sensor ID, Loại ô nhiễm và Khoảng thời gian.
    -   Xuất báo cáo chi tiết ra file **Excel (.xlsx)**.
    -   Xuất báo cáo tóm tắt kèm biểu đồ ra file **PDF**.

### 4.3. Yêu cầu phi chức năng (Non-Functional Requirements)
-   **Tính sẵn sàng:** Hệ thống quét file và cập nhật dữ liệu liên tục 24/7.
-   **Bảo mật:** Mã hóa thông tin vị trí cảm biến và phân quyền truy cập Dashboard.

## 🟢 5. Các giả định chính (Key Assumptions)
Để đảm bảo dự án tiến hành đúng tiến độ, BA đã lập các giả định sau:
1.  **Giao thức lấy file:** Web Server có quyền truy cập vào folder chứa file trên Data Server thông qua SFTP hoặc Shared Drive.
2.  **Định dạng file:** Luôn tuân thủ đúng cấu trúc đã định nghĩa, không có dòng trống hoặc dữ liệu rác.
3.  **Hệ lưu trữ:** Dữ liệu sau khi đọc từ file text sẽ được đưa vào một cơ sở dữ liệu quan hệ (RDBMS) để tối ưu việc truy vấn và trích xuất.
