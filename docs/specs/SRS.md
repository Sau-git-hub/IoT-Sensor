# Software Requirement Specification (SRS) - IoT Sensor Project

## 1. Giới thiệu (Introduction)
### 1.1 Mục đích
Tài liệu này đặc tả chi tiết các yêu cầu kỹ thuật cho hệ thống Giám sát Cảm biến IoT, phục vụ cho đội ngũ phát triển (Developers) và kiểm thử (QA).

### 1.2 Phạm vi hệ thống
Hệ thống bao gồm bộ nạp dữ liệu (Data Ingestion), Cơ sở dữ liệu (Database), API và Web Dashboard.

## 2. Mô tả tổng quát (Overall Description)
### 2.1 Các chức năng chính
-   **Data Ingestion:** Tự động đọc file từ SFTP, kiểm tra định dạng và lưu vào DB.
-   **Visualization:** Hiển thị biểu đồ 24h với khả năng so sánh đa điểm.
-   **Reporting:** Trích xuất báo cáo định dạng Excel và PDF.

### 2.2 Đối tượng người dùng
-   Nhân viên vận hành (Cần biểu đồ thời gian thực).
-   Quản lý dự án (Cần báo cáo tổng hợp).
-   Quản trị viên hệ thống (Cấu hình sensor).

## 3. Các yêu cầu cụ thể (Specific Requirements)

### 3.1 Giao diện người dùng (User Interfaces)
-   **Trang Dashboard:** Chứa Line Chart (Chart.js), bộ lọc Sensor (Dropdown), và nút Refresh.
-   **Trang Báo cáo:** Lịch chọn khoảng thời gian, checkbox chọn Sensor, nút Export.
-   **Bản đồ:** Tích hợp Leaflet hiển thị icon sensor kèm trạng thái màu sắc theo AQI.

### 3.2 Yêu cầu chức năng (Functional Requirements)
-   **FR1: Xử lý file dữ liệu**
    -   Hệ thống phải quét folder `/uploads` mỗi 300 giây.
    -   Phải parse được cấu trúc: `YYYY-MM-DD HH:mm:ss, SensorID, Type, Value`.
    -   Di chuyển file sang `/processed` sau khi hoàn tất.
-   **FR2: Biểu đồ giám sát**
    -   Vẽ biểu đồ đường với trục X là thời gian (24h) và trục Y là giá số ô nhiễm.
    -   Hỗ trợ hiển thị tối đa 3 đường biểu đồ cùng lúc.
-   **FR3: Xuất dữ liệu**
    -   Excel: Phải bao gồm các sheet dữ liệu thô và sheet tổng hợp trung bình theo giờ.
    -   PDF: Phải bao gồm ảnh chụp biểu đồ (Snapshot) và bảng thông số.

### 3.3 Yêu cầu hiệu năng (Performance Requirements)
-   **Thời gian phản hồi API:** < 500ms cho các truy vấn dữ liệu 24h.
-   **Tốc độ xử lý file:** < 5 giây cho file chứa 1000 bản ghi.

### 3.4 Bảo mật & Tin cậy (System Attributes)
-   **Xác thực:** Sử dụng Firebase Auth / JWT.
-   **Sao lưu:** Database thực hiện backup tự động mỗi ngày vào 0:00 AM.
-   **Tính sẵn sàng:** Hệ thống phải hoạt động ổn định 24/7.

## 4. Các ràng buộc thiết kế (Design Constraints)
-   Ngôn ngữ: Node.js (Backend), React (Frontend).
-   Cơ sở dữ liệu: PostgreSQL / SQLite.
-   Trình duyệt hỗ trợ: Chrome, Edge, Safari (Latest versions).
