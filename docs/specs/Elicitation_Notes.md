# 📋 Elicitation Notes & Assumptions - Dự án IoT Sensor ABC

Dưới đây là các câu hỏi chuyên sâu do BA đặt ra và các **giả định (Assumptions)** để chúng ta có thể tiến hành thiết kế hệ thống ngay lập tức.

## 1. Nhóm Kỹ thuật (Technical & Data)
- **Q:** Cấu trúc chính xác của file text là gì?
- **Giả định:** File CSV hoặc Plain Text, mỗi dòng là một bản ghi: `Timestamp, SensorID, Type (Air/Water), Value`.
- **Q:** Cách thức Web server lấy file từ Data server?
- **Giả định:** Web server sẽ chạy một "Cron Job" hoặc "Worker" để quét folder qua giao thức SFTP mỗi 5 phút.

## 2. Nhóm Chức năng (Functional)
- **Q:** Dashboard 24h cần hiển thị dữ liệu theo thời gian thực (Real-time) hay load lại trang?
- **Giả định:** Sử dụng cơ chế Auto-refresh hoặc WebSocket để cập nhật biểu đồ mà không cần load lại trang.
- **Q:** Có cần tính năng so sánh dữ liệu giữa các Sensor không?
- **Giả định:** Có. Người dùng có thể chọn tối đa 3 Sensor để so sánh chỉ số ô nhiễm trên cùng một biểu đồ.

## 3. Nhóm Phi chức năng (Non-Functional)
- **Q:** Hệ thống cần chịu tải bao nhiêu người dùng cùng lúc?
- **Giả định:** Khoảng 10-20 nhân viên vận hành và quản lý cấp cao.
- **Q:** Dữ liệu có cần mã hóa khi lưu trữ không?
- **Giả định:** Cần mã hóa các thông tin nhạy cảm về vị trí cảm biến để đảm bảo an ninh hạ tầng.

## 4. Nhóm Kinh doanh (Business & Reporting)
- **Q:** Định dạng xuất báo cáo ưu tiên?
- **Giả định:** Xuất file Excel (.xlsx) với đầy đủ các cột dữ liệu thô và một file PDF tóm tắt biểu đồ.
- **Q:** Thời gian lưu trữ dữ liệu (Data Retention)?
- **Giả định:** Dữ liệu thô lưu trong 2 năm, dữ liệu tổng hợp lưu vĩnh viễn.

---
**💡 Ghi chú BA:** Việc tự giả định câu trả lời giúp dự án không bị đình trệ. Tuy nhiên, BA phải luôn ghi chú lại các giả định này để khách hàng xác nhận (Sign-off) sau này.
