# Case Comparison

Tóm tắt bài học từ case study để dùng cho dashboard.

| Trường | Case thành công / tín hiệu tốt | Case cảnh báo / thất bại |
|---|---|---|
| **Case** | Morgan Stanley - AI cho Financial Advisors | MD Anderson - IBM Watson Oncology |
| **AI được dùng trong workflow nào?** | Tìm kiếm, trích xuất thông tin, hỗ trợ tổng hợp báo cáo tài chính cho các cố vấn. | Đưa ra phác đồ điều trị ung thư dựa trên dữ liệu bệnh án và y văn. |
| **Người dùng chính là ai?** | Cố vấn tài chính nội bộ. | Bác sĩ điều trị ung thư. |
| **Họ đo metric gì?** | Tỉ lệ sử dụng (Adoption rate), Thời gian tra cứu (Resolution time/Productivity). | Độ chính xác của phác đồ (Accuracy), Thời gian huấn luyện AI. |
| **Metric đó chứng minh được gì?** | Chứng minh hệ thống giúp tăng tốc độ làm việc và được nhân viên đón nhận tốt. | Chứng minh AI có khả năng đọc y văn tốt nhưng trong môi trường lab (môi trường kiểm soát). |
| **Metric đó chưa chứng minh được gì?** | Chưa chứng minh giá trị cuối cùng về doanh thu (AUM) hay mức độ tin tưởng của khách hàng cuối. | Chưa chứng minh được độ an toàn thực tế trên lâm sàng (Trust) và khả năng áp dụng linh hoạt trên bệnh nhân thật. |
| **Thiếu metric nào?** | Tỉ lệ cần check lại nguồn (Fact-check rate), Tỉ lệ AI hallucination. | Tỉ lệ bác sĩ phải override phác đồ của AI (Override rate), Thời gian để bác sĩ sửa lỗi do AI đề xuất. |
| **Bài học cho dashboard nhóm** | Cần đo thời gian tiết kiệm được nhưng phải gắn chặt với Quality (không đánh đổi chất lượng). | Khi AI tham gia quy trình rủi ro cao (y tế, thuế, pháp lý), metric quan trọng nhất là Override rate và Error escalation rate, không phải tốc độ. |

**Bài học nhóm sẽ áp dụng vào dashboard:**

```markdown
1. Không đo tốc độ xử lý (Productivity) một cách cô lập. Tốc độ phải luôn đi kèm với Quality (tỉ lệ lỗi/rework rate) để đảm bảo chất lượng không giảm sút.
2. Với FreeTax AI (tương tự như y tế), phải có cơ chế Human-in-the-loop (HITL). Dashboard bắt buộc phải có metric đo lường % hồ sơ cần con người (kế toán viên) override hoặc sửa lại.
3. Không để AI chạy "auto-pilot" hoàn toàn trên các case phức tạp. Chia luồng: Case cơ bản -> AI xử lý nhiều; Case phức tạp -> AI chỉ tóm tắt, con người quyết định.
```
