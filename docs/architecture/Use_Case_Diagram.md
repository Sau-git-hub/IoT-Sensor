# Use Case Diagram - Các chức năng hệ thống IoT

Sơ đồ này giúp xác định ai (Actors) sẽ sử dụng những chức năng gì (Use Cases) trong hệ thống Giám sát Môi trường.

## 📊 Sơ đồ ca sử dụng (Use Case Diagram)

```mermaid
graph LR
    subgraph Actors
        OP[Nhân viên Vận hành]
        MGR[Quản lý / PO]
        ADM[Quản trị viên]
        SYS[Worker Hệ thống]
    end

    subgraph IoT_Sensor_System
        UC1((Xem Dashboard 24h))
        UC2((So sánh Cảm biến))
        UC3((Trích xuất báo cáo Excel))
        UC4((Xuất báo cáo PDF))
        UC5((Quản lý danh mục Sensor))
        UC6((Xử lý file dữ liệu))
    end

    OP --- UC1
    OP --- UC2
    
    MGR --- UC1
    MGR --- UC3
    MGR --- UC4
    
    ADM --- UC5
    
    SYS --- UC6
    
    UC1 -.-> UC6 : << include >>
```

## 🔍 Mô tả các Actor & Use Case chính:

1.  **Nhân viên Vận hành:** Quan tâm đến các con số tức thời và diễn biến biểu đồ để kịp thời báo cáo sự cố ô nhiễm.
2.  **Quản lý (PO):** Cần dữ liệu tổng hợp để làm hồ sơ và báo cáo cuối kỳ.
3.  **Quản trị viên (Admin):** Cấu hình hệ thống, thêm/bớt sensor khi công ty ABC mở rộng thêm chi nhánh.
4.  **Hệ thống (SYS):** Đây là một "Actor tự động", thực hiện việc quét file và đổ dữ liệu vào database định kỳ.
