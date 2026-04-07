# System Architecture & Data Flow - IoT Sensor System

Hệ thống được thiết kế theo kiến trúc Micro-services đơn giản để đảm bảo tính module và dễ mở rộng.

## 🔄 1. Luồng dữ liệu (Data Flow Diagram)

```mermaid
sequenceDiagram
    participant S as Sensor Device
    participant SRV as Data Server (SFTP)
    participant WK as Backend Worker (Parser)
    participant DB as Database (RDBMS)
    participant API as Backend API (Express)
    participant WEB as React Dashboard

    S->>SRV: Gửi file text (mỗi 5 phút)
    WK->>SRV: Quét folder tìm file mới
    SRV-->>WK: Trả về nội dung file
    WK->>WK: Parse dữ liệu (CSV/Text)
    WK->>DB: Lưu vào bảng pollution_data
    WK->>SRV: Di chuyển file sang folder /processed
    
    WEB->>API: Yêu cầu dữ liệu 24h (Sensor ID)
    API->>DB: Query dữ liệu kèm Filter
    DB-->>API: Trả về tập dữ liệu (JSON)
    API-->>WEB: Trả về mảng dữ liệu cho biểu đồ
    WEB->>WEB: Render biểu đồ Chart.js
```

## 🏗️ 2. Tầng Công nghệ đề xuất (Proposed Tech Stack)

-   **Backend (Core):** Node.js + TypeScript (để đảm bảo kiểu dữ liệu an toàn).
-   **File Scraper:** Node-cron + SSH2-SFTP-Client.
-   **Database:** PostgreSQL (Mạnh mẽ, hỗ trợ Time-series tốt thông qua TimescaleDB nếu cần).
-   **Frontend:** React + Vite + Tailwind CSS + Shadcn/UI.
-   **State Management:** TanStack Query (để xử lý Auto-refresh 5 phút mượt mà).

## 🛡️ 3. Bảo mật (Security)
-   **API:** Sử dụng JWT hoặc API Key để bảo vệ các Endpoint.
-   **Database:** Đặt trong mạng nội bộ (VPC), không public ra ngoài.
-   **SFTP:** Sử dụng Private/Public Key để kết nối lấy file.
