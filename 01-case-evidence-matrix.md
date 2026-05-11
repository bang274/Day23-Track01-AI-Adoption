# Case Evidence Matrix

## 1. Thông tin chung
| Trường | Trả lời |
|---|---|
| Người phân tích | Bang Tran |
| Case được giao | Morgan Stanley - AI Assistant cho Financial Advisors |
| Phân loại | Thành công / Tín hiệu tốt |

## 2. Phân tích Case
- **AI được dùng trong workflow nào?**  
  AI Assistant được dùng để tìm kiếm, trích xuất thông tin từ kho lưu trữ báo cáo nghiên cứu và tài liệu khổng lồ của Morgan Stanley, nhằm phục vụ cho các cố vấn tài chính (Financial Advisors) trong quá trình tư vấn khách hàng.

- **Họ đo metric gì?**  
  1. Tỉ lệ cố vấn tài chính áp dụng AI trong công việc hàng ngày (Adoption rate).
  2. Thời gian trung bình để tìm kiếm thông tin cho một truy vấn phức tạp (Time-to-information).
  3. Mức độ hài lòng của cố vấn tài chính (CSAT từ nhân sự nội bộ).

- **Metric đó chứng minh được gì?**  
  Chứng minh được hệ thống thực sự tiết kiệm thời gian (Productivity tăng mạnh), giảm bớt công việc tra cứu thủ công, và có độ phủ ứng dụng cao trong tập nhân sự mục tiêu (Adoption tốt).

- **Metric đó chưa chứng minh được gì?**  
  Chưa chứng minh được AI có trực tiếp làm tăng doanh thu hay không (AUM - Assets Under Management có tăng nhờ lời khuyên từ AI hay không), và mức độ tin tưởng tuyệt đối của khách hàng cuối (Client Trust).

- **Còn thiếu metric nào?**  
  - Tỉ lệ lỗi (Hallucination rate) trong các câu trả lời do AI tạo ra.
  - Tỉ lệ cố vấn tài chính phải kiểm tra chéo lại với nguồn gốc (Rework rate/Fact-check rate).

- **Bài học nào áp dụng được vào dashboard của nhóm?**  
  Khi xây dựng FreeTax AI, không chỉ đo số lượng hồ sơ thuế được AI xử lý hoặc tốc độ (Productivity), mà cần bắt buộc đo lường Tỉ lệ lỗi/kiểm tra lại từ nhân viên kế toán (Quality/Trust) để tránh việc AI đưa ra thông tin thuế sai lệch gây rủi ro pháp lý.
