# Swimlane Diagram - Phân định trách nhiệm hệ thống

Sơ đồ làn bơi (Cross-functional Flowchart) giúp chúng ta thấy rõ bộ phận nào (Actor/System) chịu trách nhiệm cho các hoạt động cụ thể.

## 📊 Sơ đồ làn bơi (Swimlane Diagram)

```mermaid
graph TD
    subgraph SENSOR_DEVICE [Thiết bị Cảm biến]
        A1[Thu thập dữ liệu môi trường] --> A2[Ghi file text cục bộ]
        A2 --> A3[Upload file lên SFTP]
    end

    subgraph DATA_SERVER [SFTP Server]
        A3 --> B1[Lưu trữ file tạm thời]
    end

    subgraph BACKEND_SYSTEM [Hệ thống Backend]
        B1 --> C1[Worker quét file mới - Polling]
        C1 --> C2[Download & Parse nội dung]
        C2 --> C3[Gửi lệnh SQL lưu dữ liệu]
        
        C4[Cung cấp API REST]
    end

    subgraph DATABASE [Cơ sở dữ liệu]
        C3 --> D1[(Lưu pollution_data)]
        D1 --> C4
    end

    subgraph WEB_DASHBOARD [Giao diện Người dùng]
        C4 --> E1[Request dữ liệu 24h]
        E1 --> E2[Hiển thị biểu đồ Chart.js]
    end

    style SENSOR_DEVICE fill:#f9f,stroke:#333SRV
    style DATA_SERVER fill:#bbf,stroke:#333
    style BACKEND_SYSTEM fill:#dfd,stroke:#333
    style DATABASE fill:#ffd,stroke:#333
    style WEB_DASHBOARD fill:#fdd,stroke:#333
```

## 🔍 Ý nghĩa của sơ đồ này:
1.  **Ranh giới (Boundaries):** Nhìn vào sơ đồ, chị sẽ thấy ngay việc upload file là việc của "Thiết bị", còn việc quét file là việc của "Backend".
2.  **Điểm tích hợp (Integration points):** Những mũi tên đi xuyên qua "vách ngăn" chính là nơi hai hệ thống tương tác với nhau (ví dụ: A3 sang B1).
3.  **Điểm chết (Deadlocks):** Nếu Backend không quét, dữ liệu sẽ kẹt ở "SFTP Server". Sơ đồ này giúp chúng ta không bỏ quên bất kỳ khâu nào.
