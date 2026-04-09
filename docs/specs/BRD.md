# 📑 Consolidated Project Specification - IoT Sensor System (ABC Corp)

Tài liệu này là bản hợp nhất cuối cùng từ giai đoạn Khám phá (Discovery) và Khơi gợi yêu cầu (Elicitation). Đây là căn cứ chính thức để tiến hành thiết kế kiến trúc và lập trình.

## 🟢 1. Tổng quan & Mục tiêu (Overview & Goals)
-   **Chủ dự án:** Công ty ABC.
-   **Mục tiêu:** Xây dựng hệ thống Web Dashboard giám sát ô nhiễm nước và không khí từ các bộ cảm biến IoT tập trung.
-   **KPI chính:** Hiển thị dữ liệu chính xác 100% so với file thô, độ trễ hiển thị < 30 giây, thời gian load trang < 2 giây.

## 🟢 2. Các bên liên quan (Stakeholder Matrix)
| Vai trò | Kỳ vọng chính |
| ------- | ------------- |
| **Ban Giám đốc** | Báo cáo chính xác để ra quyết định chiến lược về môi trường. |
| **Nhân viên Vận hành** | Dashboard 24h trực quan, so sánh được các sensor, có cảnh báo. |
| **Quản lý (PO)** | Trích xuất báo cáo Excel (thô) và PDF (tổng hợp) mỗi kỳ. |
| **Admin IT** | Quản lý danh mục sensor, cấu hình hệ thống dễ dàng. |

## 🟢 3. Yêu cầu chi tiết (Detailed Requirements)

### 3.1. Dữ liệu & Kết nối (Data & Integration)
-   **Định dạng:** File Text (`.txt` hoặc `.csv`).
-   **Cấu trúc:** `Timestamp, SensorID, Type (Air/Water), Value`.
-   **Tần suất:** Sensor gửi file 5 phút/lần về SFTP Server.
-   **Giao thức:** Backend chạy Worker quét SFTP folder định kỳ.
-   **Tiêu chuẩn AQI:** Áp dụng 6 ngưỡng màu sắc (Xanh -> Nâu) theo chuẩn U.S. EPA.

### 3.2. Chức năng chính (Functional)
-   **Dashboard Real-time:** Tự động cập nhật dữ liệu (Auto-refresh) mỗi 5 phút.
-   **Biểu đồ 24h:** Hiển thị diễn biến chỉ số ô nhiễm trong 24 giờ gần nhất.
-   **So sánh đa điểm:** Cho phép chọn tối đa 3 Sensor để vẽ lên cùng 1 biểu đồ.
-   **Bản đồ vị trí:** Ghim vị trí Sensor trên bản đồ (Leaflet/Google Maps).
-   **Chế độ Đêm (Dark Mode):** Hỗ trợ nhân viên trực ca đêm.
-   **Báo cáo & Trích xuất:**
    -   Xuất **Excel**: Chứa dữ liệu thô để phân tích sâu.
    -   Xuất **PDF**: Chứa biểu đồ và nhận xét tóm tắt.

### 3.3. Phi chức năng (Non-Functional)
-   **Bảo mật:** Tích hợp Firebase Auth (Login Google). Mã hóa thông tin vị trí Sensor.
-   **Lưu trữ:** Dữ liệu thô lưu 2 năm (Active), sau đó nén vào Cold Storage.
-   **Đa ngôn ngữ:** Hỗ trợ song ngữ Việt - Anh.

## 🟢 4. Xử lý kịch bản ngoại lệ (Edge Case Handling)
Hệ thống được thiết kế để chịu lỗi (Fault-tolerant):
-   **Sensor Offline:** Nếu mất dữ liệu > 15p, hiển thị trạng thái "Offline" và cảnh báo Admin.
-   **Dữ liệu ảo (Anomaly):** Các chỉ số nhảy vọt bất thường sẽ được đánh dấu (?) để kiểm tra vật lý.
-   **Xung đột file:** Tuân thủ quy tắc đặt tên `SensorID_YYYYMMDD_HHMM.txt`.
-   **Time Sync:** Ưu tiên `Timestamp` bên trong file thay vì giờ của Server nhận.

## 🟢 5. Lộ trình tương lai (Roadmap)
- **Phase 2:** Cung cấp Public API cho đối tác.
- **Phase 3:** Điều khiển thiết bị ngoại vi (Quạt gió, máy lọc) qua module Relay.
- **Phase 4:** Ứng dụng AI dự báo xu hướng ô nhiễm theo thời tiết.

---
*Bản quyền dữ liệu thuộc về Công ty ABC. Tài liệu do Antigravity BA Agent soạn thảo.*
