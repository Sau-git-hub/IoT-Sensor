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
## 📍 Bài học 4: Kỹ thuật Khơi gợi yêu cầu (Elicitation)
BA không chỉ hỏi "Bạn muốn gì?", mà phải hỏi **Đúng người - Đúng việc**. Kỹ thuật này gọi là **Stakeholder Analysis**.

### 1. Phân loại Stakeholder (Các bên liên quan):
Trong dự án này, chúng ta có 3 nhóm chính:
-   **Technical Team:** Những người nắm "ruột gan" của sensor và server.
-   **End-Users:** Những người trực tiếp dùng web mỗi ngày.
-   **Decision Makers (Sếp/Quản lý):** Những người chi tiền và cần báo cáo cuối tháng.

### 2. Kỹ thuật đặt câu hỏi:
-   **Câu hỏi mở (Open-ended):** "Quy trình hiện tại sếp đang lấy dữ liệu như thế nào?" (Để tìm hiểu hiện trạng).
-   **Câu hỏi đóng (Closed-ended):** "Server có hỗ trợ kết nối SSH không?" (Để chốt thông số kỹ thuật).

---
## 📍 Bài học 6: Xử lý trường hợp ngoại lệ (Edge Cases & Exceptions)
BA giỏi là người không chỉ thiết kế cho "Luồng hạnh phúc" (Happy Path - khi mọi thứ đều chạy đúng), mà phải lường trước các "Cơn ác mộng":

1.  **Happy Path:** Sensor gửi file -> Web hiển thị -> Xong.
2.  **Edge Case/Exception:** 
    -   Sensor mất điện đột ngột.
    -   File gửi về bị trống hoặc sai định dạng.
    -   Sever hết dung lượng lưu trữ.

---
## 📍 Bài học 8: Từ "Cái gì" sang "Như thế nào" (Strategy & Architecture)
Giai đoạn này là bước chuyển mình từ BA sang Architect (Kiến trúc sư):

1.  **Phase 1 (BA):** Tập trung vào **"Cái gì"** (What). Người dùng cần gì? Hệ thống làm được gì?
2.  **Phase 2 (Architect):** Tập trung vào **"Như thế nào"** (How). Lưu trữ ở đâu? Luồng dữ liệu chạy ra sao?

**🔍 Tại sao cần Sơ đồ (Diagrams)?** 
Vì hình ảnh có giá trị bằng ngàn lời nói. Sơ đồ **Mermaid** giúp lập trình viên biết họ cần viết API gì, và QA biết cần test luồng nào.

---
## 📍 Bài học 9: Sơ đồ hoạt động (Activity Diagram)
Nếu **System Flow** cho ta cái nhìn tổng quan về các thành phần, thì **Activity Diagram** cho ta cái nhìn chi tiết về **Logic xử lý**:

1.  **Nodes:** Các ô chữ nhật mô tả hành động (Action).
2.  **Decisions:** Hình kim cương thể hiện các điều kiện Rẽ nhánh (If/Else).
3.  **Flows:** Các mũi tên chỉ thứ tự thực hiện.

**🔍 Tại sao BA cần vẽ cái này?**
Để lập trình viên biết họ cần xử lý bao nhiêu trường hợp ngoại lệ (Error handling) và luồng nào là luồng chính.

---
## 📍 Bài học 10: Sơ đồ ca sử dụng (Use Case Diagram)
Đây là sơ đồ "vỡ lòng" của BA dùng để trả lời câu hỏi: **"Ai dùng cái gì?"**

1.  **Actors (Tác nhân):** Là người hoặc hệ thống bên ngoài tương tác với Web của mình.
2.  **Use Cases (Ca sử dụng):** Là những tính năng/hành động mà Actor thực hiện.
3.  **Boundary (Phạm vi):** Cái hộp bao quanh các Use Case, xác định những gì thuộc về hệ thống của mình.

**🔍 Tại sao cần vẽ cái này?**
Để đảm bảo BA không bỏ sót một nhóm người dùng nào (Ví dụ: Suýt nữa chúng ta quên mất ông Admin cần quản lý danh sách Sensor).

---
## 📍 Bài học 11: Sơ đồ làn bơi (Swimlane Diagram)
Đây là phiên bản nâng cấp của **Activity Diagram**, chuyên dùng để phân định **Trách nhiệm (Accountability)**.

1.  **Swimlanes (Làn bơi):** Mỗi làn đại diện cho một phòng ban, một Actor hoặc một thành phần kỹ thuật.
2.  **Hành động:** Được đặt vào đúng "làn" của người thực hiện nó.

**🔍 Tại sao BA cần vẽ cái này?**
Để tránh tình trạng "cha chung không ai khóc". Khi nhìn vào sơ đồ, chị sẽ biết ngay nếu dữ liệu không hiện trên Web thì lỗi nằm ở làn nào (Sensor chưa upload hay Backend chưa quét?).

---
## 📍 Bài học 12: Chuẩn hóa với BPMN (Business Process Model and Notation)
Nếu "chị" muốn làm việc ở các tập đoàn lớn hoặc ngân hàng, BPMN là ngôn ngữ bắt buộc.

1.  **Sự kiện (Events):** Dùng hình tròn. (Bắt đầu, Kết thúc, Hẹn giờ).
2.  **Cổng logic (Gateways):** Hình thoi. Dùng để xử lý các điều kiện "Nếu... thì...".
3.  **Luồng (Flows):** Cho thấy dòng chảy của giá trị kinh doanh.

**🔍 Tại sao cần BPMN?**
Vì đây là chuẩn quốc tế. Một bản vẽ BPMN có thể dùng để trao đổi với bất kỳ chuyên gia nào trên thế giới mà không sợ hiểu lầm.

**✍️ Lời khuyên:** Hãy chú ý đến sự kiện "Hẹn giờ" (Timer). Trong IoT, hầu hết quy trình đều bắt đầu từ một sự kiện tự động theo thời gian thay vì chờ con người click chuột.
