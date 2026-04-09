# Activity Diagram - Quy trình xử lý dữ liệu IoT

Sơ đồ này mô tả chi tiết các hoạt động (Activities) diễn ra trong hệ thống, từ khi cảm biến thu thập dữ liệu cho đến khi hiển thị lên Web Dashboard.

## 📊 Sơ đồ hoạt động (Activity Diagram)

```mermaid
graph TD
    Start((Bắt đầu)) --> Generate[Cảm biến thu thập dữ liệu]
    Generate --> WriteFile[Ghi vào file text tạm]
    WriteFile --> Upload[Upload file lên SFTP Server]
    
    Upload --> Poll{Worker quét folder?}
    Poll -- Không có file --> Wait[Đợi 5 phút]
    Wait --> Poll
    
    Poll -- Có file mới --> Download[Download file về Backend]
    Download --> Parse[Phân tích nội dung file]
    
    Parse --> Valid{Dữ liệu hợp lệ?}
    Valid -- Không --> LogErr[Ghi Log lỗi & Move sang /failed]
    Valid -- Có --> SaveDB[Lưu vào Database]
    
    SaveDB --> MoveProc[Di chuyển file sang /processed]
    MoveProc --> Notify[Cập nhật Real-time Cache]
    
    subgraph Web_Dashboard
        Request[User mở Dashboard] --> GetAPI[API trả về dữ liệu 24h]
        GetAPI --> Render[Render biểu đồ Chart.js]
    end
    
    Notify -.-> GetAPI
    Render --> End((Kết thúc))
    LogErr --> End
```

## 🔍 Giải thích các bước quan trọng:
1.  **Vòng lặp (Wait 5 min):** Đảm bảo hệ thống không quét liên tục gây quá tải server (Polling mechanism).
2.  **Kiểm tra tính hợp lệ (Valid?):** Đây là bước quan trọng nhất của BA để đảm bảo dữ liệu "rác" không lọt vào database.
3.  **Phân vùng file (Failed/Processed):** Giúp quản trị viên dễ dàng theo dõi và xử lý lại các file bị lỗi.
