# Database Schema - IoT Sensor System

Dựa trên yêu cầu từ BRD, chúng ta cần một cơ sở dữ liệu quan hệ (RDBMS) để lưu trữ và truy vấn dữ liệu hiệu quả.

## 🗄️ 1. Bảng `sensors` (Thông tin thiết bị)
Lưu trữ danh sách các cảm biến được lắp đặt.

| Column | Type | Constraints | Description |
| ------ | ---- | ----------- | ----------- |
| `id` | VARCHAR(50) | PRIMARY KEY | Mã ID duy nhất của Sensor. |
| `name` | VARCHAR(100) | NOT NULL | Tên gợi nhớ (VD: Sensor Tòa nhà A). |
| `type` | ENUM('AIR', 'WATER') | NOT NULL | Loại cảm biến. |
| `location` | VARCHAR(255) | | Vị trí lắp đặt. |
| `created_at` | TIMESTAMP | DEFAULT NOW() | Ngày khởi tạo. |

## 🗄️ 2. Bảng `pollution_data` (Dữ liệu ô nhiễm)
Lưu trữ các bản ghi đo lường định kỳ mỗi 5 phút.

| Column | Type | Constraints | Description |
| ------ | ---- | ----------- | ----------- |
| `id` | SERIAL | PRIMARY KEY | ID bản ghi tự tăng. |
| `sensor_id` | VARCHAR(50) | FOREIGN KEY | Liên kết với bảng `sensors`. |
| `value` | DECIMAL(5,2) | NOT NULL | Chỉ số ô nhiễm (0.00 - 100.00). |
| `timestamp` | TIMESTAMP | NOT NULL | Thời điểm lấy mẫu (từ nội dung file). |
| `received_at` | TIMESTAMP | DEFAULT NOW() | Thời điểm hệ thống nhận được file. |

## 🚀 Chiến lược tồi ưu (Performance Strategy)
-   **Indexing:** Đánh index trên cột `timestamp` và `sensor_id` để tăng tốc độ truy vấn biểu đồ 24h.
-   **Partitioning:** Nếu số lượng sensor tăng lên hàng ngàn, chúng ta sẽ thực hiện Partition table theo tháng dựa trên cột `timestamp`.
