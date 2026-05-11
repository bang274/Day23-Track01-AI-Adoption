# Product ROI Dashboard — FreeTax AI

## 0. Thông tin nhóm

| Trường | Trả lời |
|---|---|
| Nhóm | FreeTax AI Team |
| Thành viên | Bang Tran |
| Product chọn phân tích | FreeTax AI - AI assistant hỗ trợ khai thuế |
| Người dùng chính | Khách hàng cá nhân (Freelancers), Kế toán viên (Accountants) |

---

## 2. Part A — Adoption Context

| Trường | Trả lời |
|---|---|
| Product | FreeTax AI |
| Người dùng chính | Kế toán viên (Internal), Freelancers (External) |
| Bối cảnh sử dụng | Quá trình phân loại hóa đơn chứng từ và lên tờ khai thuế tốn thời gian, dễ sai sót thủ công. |
| Mục tiêu kinh doanh / vận hành | Giảm 50% thời gian xử lý hồ sơ thuế, giảm chi phí vận hành (Cost per return) trong khi duy trì độ chính xác 100% để tuân thủ pháp luật. |
| Rào cản ADKAR chính | **Ability** (Kế toán chưa quen việc review thay vì tự nhập), **Trust** (Khách hàng và nội bộ sợ rủi ro AI sai gây phạt thuế) |

### 2 workflow chính

| # | Workflow | AI làm gì? | Con người kiểm tra ở đâu? | Khi AI sai thì xử lý thế nào? |
|---|---|---|---|---|
| 1 | Document Ingestion (OCR & Phân loại) | Đọc hóa đơn, trích xuất dữ liệu, phân loại vào các nhóm chi phí hợp lệ/không hợp lệ | Kế toán review các hóa đơn có AI Confidence Score < 95% hoặc số tiền lớn | Kế toán tự phân loại lại bằng tay, gỡ cờ (unflag) và ghi chú để retrain model |
| 2 | Tax Draft Generation (Lên nháp tờ khai) | Auto-fill số liệu từ hóa đơn vào form khai thuế chuẩn | Kế toán trưởng ký duyệt nháp cuối cùng (Final Review) trước khi submit | Sửa tay trên draft, ticket được đánh dấu là "AI failure" để team Dev kiểm tra logic |

### 3 tactic tăng adoption

| Tactic | Nhắm vào rào cản nào? | Áp dụng cho workflow nào? | Người phụ trách |
|---|---|---|---|
| 1. Giới hạn tự động hóa (Confidence Threshold > 95%) | Trust | Workflow 1 | AI Lead |
| 2. Đào tạo Kế toán chuyển từ "Data Entry" sang "Reviewer" | Ability, Knowledge | Workflow 1 & 2 | Ops Lead |
| 3. Bắt buộc Human-in-the-loop (HITL) cho 100% Final Draft | Trust | Workflow 2 | Compliance Lead |

---

## 3. Part B — ROI Dashboard

### B.1 Metric toàn product

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|---|---|---:|---:|---|---|---|---|
| Activation | % eligible tax profiles được AI hỗ trợ | 0% (manual) | > 70% | System Database | Product Manager | Coverage cao che lấp tỷ lệ lỗi trong các case phức tạp | Tách report coverage theo mức độ phức tạp hồ sơ (Simple/Complex) |
| Trust / Quality | % Tax returns không bị cơ quan thuế phạt/reject | 99% (human) | > 99% | Báo cáo cơ quan thuế | Compliance Lead | Đo quá trễ (chỉ biết khi đã bị phạt) | Ghép metric này với Internal QA Pass Rate (Leading indicator) |
| Value | Cost per finalized tax return | $50 | < $20 | Finance system | CFO | Cắt giảm chi phí có thể đánh đổi bằng chất lượng hồ sơ | Monitor chặt chẽ Quality metric, nếu rớt phải scale down AI |

### B.2 Metric theo workflow

#### Workflow 1 — Document Ingestion (OCR & Phân loại)

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|---|---|---:|---:|---|---|---|---|
| Productivity | Median time to process 100 receipts | 45 mins | < 10 mins | System log | Ops Lead | AI phân loại lướt qua nhanh nhưng sai nhiều | Bắt buộc xem xét cùng với Rework rate (Quality) |
| Quality | % receipts manually re-categorized (Rework Rate) | N/A | < 15% | Database | QA Lead | Kế toán lười, tin tưởng mù quáng không thèm check lại | Audit ngẫu nhiên 5% hồ sơ để kiểm tra chéo |
| Trust | AI Confidence Score Calibration (Độ tin cậy của AI) | N/A | > 95% correct | ML logs | AI Lead | Model overconfident (tự tin cao nhưng sai) | Review hàng tuần các case bị flag, điều chỉnh logic |

#### Workflow 2 — Tax Draft Generation (Lên nháp tờ khai)

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|---|---|---:|---:|---|---|---|---|
| Productivity | Time from Draft creation to Final Review completion | 2 hours | < 30 mins | System log | Ops Lead | Draft nhanh nhưng chất lượng tệ khiến review lâu hơn | Đo tổng thời gian (End-to-end) thay vì chỉ đo lúc tạo draft |
| Quality | QA Pass rate at Final Review | 90% | > 95% | QA tools | Compliance Lead | Reviewer quá dễ dãi | Thực hiện Double-blind test định kỳ |
| Value | Thời gian tiết kiệm được cho Kế toán viên (Hours saved) | 0 | 10 hrs/week | Timesheet | HR / Ops | Tiết kiệm giờ nhưng nhân viên không làm gì thêm | Gắn hours saved với khối lượng hồ sơ hoàn thành (Throughput) |

---

## 4. Part C — Dashboard Mock

```text
┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 1: PRODUCT HEALTH             │ │ TILE 2: WORKFLOW 1 (PRODUCTIVITY)  │
│ Metric: % Profiles covered by AI   │ │ Metric: Time per 100 receipts      │
│ Current: 40%      Target: > 70%    │ │ Current: 15m       Target: < 10m   │
│ Status: AMBER                      │ │ Status: AMBER                      │
│ Action if red: Hạ threshold AI     │ │ Action if red: Kiểm tra lại OCR    │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 3: WORKFLOW 1 (QUALITY)       │ │ TILE 4: WORKFLOW 2 (TRUST/QUALITY) │
│ Metric: Rework Rate (Re-categorized│ │ Metric: QA Pass Rate at Final Rev  │
│ Current: 18%      Target: < 15%    │ │ Current: 96%       Target: > 95%   │
│ Status: RED                        │ │ Status: GREEN                      │
│ Action if red: Retrain model       │ │ Action if red: Bật 100% Human Check│
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 5: VALUE                      │ │ TILE 6: DECISION                   │
│ Metric: Cost per finalized return  │ │ Continue with HITL Guardrails      │
│ Current: $25      Target: < $20    │ │ Metric mạnh nhất: QA Pass Rate     │
│ Status: GREEN                      │ │ Before scale: Áp dụng Audit ngẫu nh│
│ Action if red: Review AWS/LLM bill │ │ Người phụ trách: Compliance Lead   │
└────────────────────────────────────┘ └────────────────────────────────────┘
```

---

## 5. Part D — Decision Memo

# Decision Memo — FreeTax AI

1. **Nhóm khuyến nghị:** Tiếp tục triển khai (Continue) nhưng đi kèm quy trình bảo vệ (Guardrails) chặt chẽ bằng Human-in-the-loop.

2. **Chỉ số mạnh nhất để bảo vệ quyết định là:**
   **QA Pass rate at Final Review (> 95%)**. Mặc dù mục tiêu là giảm chi phí (Cost per return) và tiết kiệm thời gian (Productivity), nhưng trong lĩnh vực Thuế, sai sót pháp lý là tối kỵ. QA Pass rate chứng minh rằng AI không chỉ làm nhanh mà còn làm ĐÚNG, đảm bảo không đánh đổi chất lượng lấy tốc độ.

3. **Chỉ số hoặc giả định nhóm đã sửa sau phản biện là:**
   - **V1:** Đo năng suất bằng "Thời gian AI tạo draft tờ khai".
   - **V2:** Sửa thành "Thời gian tổng từ lúc tạo Draft đến lúc Review xong (Time from Draft to Final Review)".
   - **Vì sao V1 yếu?** V1 chỉ đo được tốc độ của máy (rất vô nghĩa vì AI lúc nào cũng nhanh). Nó không phản ánh việc nếu draft tệ, kế toán phải tốn rất nhiều thời gian sửa lỗi (rework).
   - **Vì sao V2 tốt hơn?** V2 đo trải nghiệm thực tế (End-to-end), đảm bảo AI draft thực sự giúp con người làm việc nhanh hơn.

4. **Trước khi scale, nhóm phải:**
   1. Triển khai quy trình Audit ngẫu nhiên 5% hồ sơ (Tránh thiên kiến tin tưởng mù quáng vào AI) — **Phụ trách: Compliance Lead**, Deadline: Cuối tuần này.
   2. Retrain model phân loại cho các hạng mục chi phí thường bị sai (Re-categorized > 15%) — **Phụ trách: AI Lead**, Deadline: Tuần sau.
   3. Review lại chi phí API LLM xem việc auto-fill có làm lạm vốn (Cost per return bị dội) hay không — **Phụ trách: CFO**, Deadline: Đầu tháng sau.

---

## 6. Red-team và sửa v2

### Nhóm bị red-team (Mô phỏng tự phản biện)

| Rủi ro được nêu | Ai nêu? | Chỉ số / giả định liên quan | Sửa ở v2 |
|---|---|---|---|
| AI làm draft rất nhanh nhưng chất lượng tệ, kế toán phải đập đi làm lại. | Workflow Owner | Productivity: Thời gian tạo Draft | Đổi metric thành Time from Draft to Final Review (End-to-end). |
| Kế toán viên có thể lười, bấm "Approve" mọi thứ AI làm mà không thèm kiểm tra. | Risk | Quality: QA Pass Rate | Thêm quy trình Audit ngẫu nhiên 5% (Double-blind test). Thêm metric Rework rate để xem kế toán có thực sự tương tác sửa bài không. |
| Số lượng hồ sơ AI xử lý tăng nhưng thực tế toàn là các hồ sơ cực dễ, các hồ sơ khó AI vẫn trượt hết. | CFO / Risk | Activation: % eligible profiles | Cập nhật dashboard fix: Tách riêng báo cáo Coverage cho Simple vs Complex profiles. |

### Ít nhất 2 thay đổi cụ thể từ v1 sang v2

| # | V1 có vấn đề gì? | V2 sửa thành gì? | Vì sao sửa này tốt hơn? |
|---|---|---|---|
| 1 | Đo "Thời gian tạo Draft" làm thước đo năng suất, rất ảo vì tốc độ server luôn nhanh. | Đổi thành "Time from Draft to Final Review". | Đo được thời gian thực tế con người được giải phóng, phản ánh đúng nếu AI làm sai khiến người phải sửa lâu hơn. |
| 2 | Đo Quality bằng "Internal QA Pass Rate" nhưng bỏ qua yếu tố người review có thể dễ dãi. | Giữ QA Pass Rate nhưng thêm "Rework rate" ở bước Document Ingestion và quy định "Audit 5% ngẫu nhiên". | Ngăn chặn hiện tượng tin tưởng AI mù quáng (Automation bias) của người dùng nội bộ, giữ vững rào cản pháp lý. |
