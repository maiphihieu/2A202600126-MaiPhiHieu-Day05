# UX exercise — MoMo Moni AI

## Sản phẩm: MoMo — Moni AI Assistant (phân loại chi tiêu)

## 4 paths

### 1. AI đúng
- User chi tiêu 50k tại Circle K → Moni gợi ý "Ăn uống"
- User thấy tag đúng, không cần làm gì thêm
- UI: hiện tag + icon category, không hỏi confirm

### 2. AI không chắc (Low-confidence)
- User chuyển tiền 200k cho bạn → Moni không tag hoặc tag "Khác"
- UI: không hiện gợi ý nào, user phải tự vào chỉnh
- Vấn đề: không có cơ chế "bạn muốn phân loại giao dịch này không?" để hỏi user khi AI không 확 chắn.

### 3. AI sai (Failure)
- User mua sách trên Shopee → Moni tag "Mua sắm" thay vì "Học tập"
- User phát hiện ra lỗi khi xem báo cáo tháng.
- Sửa lỗi: Cần vào chi tiết giao dịch → đổi category → mất đến 3 bước.
- Vấn đề: không rõ AI có học từ correction này không (Feedback loop không minh bạch).

### 4. User mất niềm tin (Trust loss)
- Sau nhiều lần tag sai, user không còn tin vào báo cáo chi tiêu tự động nữa.
- Không có option "tắt auto-tag" hoặc "tag thủ công trước".
- Không có fallback rõ ràng ngoài việc phải đi rà soát và sửa từng giao dịch.

## Path yếu nhất: Path 3 + 4
- Khi AI sai, recovery flow (luồng khắc phục) mất quá nhiều bước.
- Không có learning signal (feedback loop) rõ ràng — user sửa nhưng không biết AI có đang học từ lỗi đó hay không.
- Không có cửa ra (exit/fallback) cho user mất niềm tin.

## Gap marketing vs thực tế
- Marketing hứa hẹn: "Moni giúp quản lý chi tiêu thông minh, tự động và nhàn rỗi".
- Thực tế trải nghiệm: auto-tag chỉ đúng khoảng ~70% đối với các giao dịch phổ biến siêu thị/ăn uống. Đối với các trường hợp khó (chuyển tiền, mua sắm online hỗn hợp), thường bị tag sai hoặc không nhận diện được.
- Gap lớn nhất nằm ở chỗ marketing không mảy may nhắc đến trường hợp khi AI sai — dẫn đến user mang kỳ vọng độ chính xác 100%, gây ức chế khi sản phẩm hoạt động thiếu chính xác.

## Hướng thiết kế bản Sketch
*(Ảnh đính kèm: sketch.jpg)*
- **As-is (Hiện tại):** User Giao dịch → Hệ thống Auto-tag → User thấy kết quả → Nếu sai, user phải tự mò mẫm vào chỉnh sửa thủ công nhiều bước.
- **To-be (Tương lai/Cải tiến):** User Giao dịch → Hệ thống Auto-tag → Nếu độ tự tin (confidence) thấp: UI hiện ngay thông báo "Bạn muốn phân loại?" trực quan → User chọn tag → AI ghi nhận correction bằng popup "Đã học, lần sau mình sẽ để ý hơn!".
