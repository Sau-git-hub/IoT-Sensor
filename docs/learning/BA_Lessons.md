# 🎓 BA Learning Log - Bài học từ dự án IoT Sensor

## 📍 Bài học 2: Phân tích Ngữ cảnh (Context Analysis)
Khi nhận được một tấm hình hoặc một văn bản mô tả từ khách hàng, BA không nên vội code ngay. BA cần thực hiện kỹ thuật **"Bóc tách thực thể"**:

1.  **Chủ thể (Actors/Entities):** Công ty ABC, Cảm biến, Server, Người dùng Web.
2.  **Luồng dữ liệu (Data Flow):** Sensor -> Text File -> Server -> Web System.
3.  **Tần suất (Metrics):** 5 phút/lần. Đây là thông số quan trọng để thiết kế cơ sở dữ liệu (performance).

## 📍 Bài học 3: Đặc tả yêu cầu (Specification)
Từ những gạch đầu dòng ngắn gọn, BA cần chuyển hóa thành các đề mục chuẩn trong file **BRD.md**:
-   **Mục tiêu (Objectives):** Trả lời câu hỏi "Làm để làm gì?".
-   **Phạm vi (Scope):** Vẽ ra ranh giới, cái gì làm và cái gì không làm (Tránh "Scope Creep" - phình to yêu cầu).
-   **Yêu cầu chức năng (Functional):** Hệ thống sẽ *làm* gì?
-   **Yêu cầu phi chức năng (Non-functional):** Hệ thống sẽ *như thế nào*? (Ví dụ: tốc độ xử lý file, bảo mật).

---
*Ghi chú cho học viên:* Hãy so sánh hình ảnh bạn gửi và nội dung tôi soạn trong file `docs/specs/BRD.md` để thấy cách BA "dịch" ngôn ngữ đời thường sang ngôn ngữ dự án.
