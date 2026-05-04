# Reflection

**Anti-pattern:** Bỏ qua kiểm soát cấu trúc dữ liệu từ đầu (Bypassing Schema Enforcement).

**Lý do team dễ vướng phải:**
Trong các dự án thực tế, đặc biệt là giai đoạn đầu (Proof of Concept) hoặc khi làm việc với các nguồn dữ liệu bên thứ ba (như API logs, sự kiện tracking), team thường chịu áp lực ưu tiên tốc độ đưa dữ liệu vào Data Lake để nhanh chóng có báo cáo. Điều này dễ dẫn đến thói quen "cứ nạp thẳng dữ liệu thô vào, xử lý kiểu dữ liệu sau", vô tình bỏ qua hoặc tắt tính năng Schema Enforcement.

**Hậu quả & Bài học:**
Anti-pattern này tạo ra lỗi rất lớn ở các tầng sau (Silver/Gold). Khi dữ liệu không đồng nhất (ví dụ: cột `age` lẫn lộn giữa số `30` và chuỗi `"thirty"` như ở Notebook 1), các truy vấn tổng hợp sẽ liên tục bị lỗi, hệ thống pipeline đổ vỡ. Chi phí và thời gian để "truy vết" và làm sạch các dữ liệu rác ở cuối nguồn lớn hơn rất nhiều so với việc kiểm tra chặt chẽ ngay từ đầu. Delta Lake mặc định bật Schema Enforcement chính là để chặn đứng rủi ro này ngay tại cửa ngõ Bronze.
