# 📋 Questionnaire & Standard Research - Dự án IoT Sensor ABC

Tài liệu này tổng hợp bộ câu hỏi chuyên sâu phục vụ bước **Elicitation** và các đề xuất kỹ thuật dựa trên tiêu chuẩn quốc tế.

---

## 🌍 1. Nghiên cứu tiêu chuẩn AQI (Air Quality Index)
Dựa trên tiêu chuẩn quốc tế (U.S. EPA), dưới đây là các ngưỡng cảnh báo đề xuất cho hệ thống Web của Công ty ABC:

| Chỉ số AQI | Phân loại | Ý nghĩa sức khỏe | Hành động đề xuất |
| :--- | :--- | :--- | :--- |
| **0 - 50** | Tốt (Good) | Không có rủi ro | Hoạt động bình thường |
| **51 - 100** | Trung bình (Moderate) | Chấp nhận được | Nhạy cảm nên lưu ý |
| **101 - 150** | Kém (Unhealthy for Sensitive) | Ảnh hưởng nhóm nhạy cảm | Hạn chế ra ngoài |
| **151 - 200** | Xấu (Unhealthy) | Ảnh hưởng sức khỏe cộng đồng | Đeo khẩu trang |
| **201 - 300** | Rất Xấu (Very Unhealthy) | Cảnh báo khẩn cấp | Ở trong nhà |
| **301+** | Nguy hại (Hazardous) | Nguy hiểm nghiêm trọng | Đóng cửa, dùng máy lọc khí |

---

## ❓ 2. Bộ câu hỏi khơi gợi chuyên sâu (15 Câu hỏi)

### 📊 Nhóm 1: Dữ liệu (Data)
1.  **Lưu trữ file thô:** Sau khi xử lý, file text sẽ được xóa, di chuyển sang folder "Processed" hay giữ nguyên?
2.  **Kiểm soát lỗi:** Làm thế nào để nhận biết file bị lỗi hoặc ghi dở dang?
3.  **Khả năng mở rộng:** Số lượng sensor tối đa dự kiến trong 5 năm tới là bao nhiêu?
4.  **Bảo mật dữ liệu:** File text có cần mã hóa khi truyền tải từ Sensor về server không?

### ⚙️ Nhóm 2: Chức năng (Function)
5.  **So sánh đa điểm:** Có cần tính năng so sánh chỉ số giữa các chi nhánh khác nhau không?
6.  **Cảnh báo tức thời:** Có cần gửi Email/SMS/Telegram ngay khi chỉ số > 300 không?
7.  **Phân quyền:** Ai được quyền xóa/sửa dữ liệu lịch sử?
8.  **Tùy biến báo cáo:** Chức năng trích xuất PDF có cần phần Ghi chú cho chuyên gia nhận xét không?

### 🛡️ Nhóm 3: Phi chức năng (NFR)
9.  **Hiệu năng:** Dashboard phải load xong trong tối đa bao nhiêu giây (ví dụ < 2s)?
10. **Hệ thống dự phòng:** Nếu server sập, dữ liệu bị mất trong bao lâu là chấp nhận được (RPO)?
11. **Xác thực:** Có cần dùng tài khoản AD nội bộ để đăng nhập không?
12. **Tính linh hoạt:** Hệ thống có cần hiển thị tốt trên máy tính bảng/mobile không?

### 🎯 Nhóm 4: Mục tiêu kinh doanh (Business Goals)
13. **Giá trị thương hiệu:** Dự án dùng để công bố dữ liệu ra bên ngoài (PR) hay chỉ dùng nội bộ?
14. **Thương mại hóa:** Công ty có định đóng gói hệ thống này để bán cho bên khác không?
15. **Tuân thủ pháp luật:** Có quy chuẩn môi trường nhà nước nào cụ thể mà công ty buộc phải tuân theo không?
