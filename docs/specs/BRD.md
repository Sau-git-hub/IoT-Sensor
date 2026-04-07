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

## 🟢 6. Phân tích các bên liên quan (Stakeholder Matrix)
| Stakeholder | Vai trò | Mức độ ảnh hưởng | Kỳ vọng chính |
| ----------- | ------- | ---------------- | ------------- |
| Ban Giám đốc | Chủ dự án | Rất cao | Có báo cáo chính xác để ra quyết định môi trường. |
| Nhân viên Vận hành| Người dùng cuối | Cao | Giao diện Dashboard dễ dùng, cập nhật nhanh. |
| Đội Kỹ thuật IoT | Nhà cung cấp dữ liệu | Trung bình | Hệ thống Web hoạt động ổn định, không làm nghẽn Server. |

## 🟢 7. Chân dung người dùng (User Personas)
1.  **Anh Bình (Nhân viên Vận hành):** Cần theo dõi biểu đồ 24h hàng ngày để phát hiện các chỉ số bất thường và báo cáo kịp thời.
2.  **Chị An (Quản lý dự án):** Cần trích xuất dữ liệu hàng tuần sang Excel để lưu hồ sơ công ty.

## 🟢 8. Danh sách User Stories & Tiêu chí nghiệm thu (Acceptance Criteria)
| ID | User Story | Tiêu chí nghiệm thu (AC) |
| -- | ---------- | ----------------------- |
| US1 | Là nhân viên vận hành, tôi muốn xem biểu đồ 24h để biết diễn biến ô nhiễm. | Biểu đồ hiển thị đúng 24 mốc giờ, tự động refresh mỗi 5 phút. |
| US2 | Là quản lý, tôi muốn trích xuất file Excel để lưu trữ. | File Excel chứa đầy đủ các cột: Thời điểm, Mã sensor, Chỉ số. |
| US3 | Là quản lý, tôi muốn so sánh các sensor để biết khu vực nào ô nhiễm hơn. | Cho phép chọn cùng lúc >=2 sensor trên cùng 1 biểu đồ. |

## 🟢 9. Chỉ số thành công (Success Metrics/KPIs)
-   **Độ trễ dữ liệu:** Dữ liệu từ file text phải xuất hiện trên Web trong vòng tối đa 30 giây sau khi file được gửi.
-   **Độ chính xác:** Chỉ số trên Web phải khớp 100% với giá trị trong file text.
-   **Tính ổn định:** Hệ thống hoạt động 24/7 với tỷ lệ uptime > 99%.

## 🟢 10. Thuật ngữ (Glossary)
-   **Pollution Index (PI):** Chỉ số đo lường mức độ ô nhiễm (0 là sạch, 100 là ô nhiễm nặng).
-   **Sampling Time:** Thời điểm cảm biến ghi nhận giá trị và ghi vào file.

## 🟢 11. Xử lý trường hợp ngoại lệ (Edge Cases & Exceptions)
| Tình huống | Hành động của hệ thống |
| ---------- | ---------------------- |
| Sensor mất kết nối > 15p | Hiển thị trạng thái "Offline" trên Dashboard và gửi cảnh báo nhẹ cho Admin. |
| Dữ liệu đột biến (Anomaly) | Ghi nhận kèm dấu chấm hỏi (?) để yêu cầu kiểm tra sensor vật lý. |
| Trùng tên file gửi về | Yêu cầu đổi tên theo chuẩn `SensorID_YYYYMMDD_HHMM.txt` để ghi đè hoặc tạo mới. |
| Sai lệch thời gian | Ưu tiên lấy `Timestamp` trong nội dung file thay vì giờ của Server. |

## 🟢 12. Lộ trình phát triển (Future Roadmap)
- **Phase 2 (Tích hợp):** Cung cấp Public API (REST) cho các bên thứ 3.
- **Phase 3 (Điều khiển):** Tự động kích hoạt máy lọc khí/quạt thông gió khi AQI > 300 thông qua module Relay.
- **Phase 4 (AI):** Dự báo xu hướng ô nhiễm dựa trên dữ liệu lịch sử và điều kiện thời tiết.
