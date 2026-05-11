# Reflection cá nhân sau lớp

Qua buổi học và quá trình phân tích FreeTax AI, một metric quan trọng nhất mà tôi đã quyết định thay đổi trong hệ thống đo lường ROI là cách định nghĩa về "Năng suất" (Productivity). 

Ban đầu, tôi dự định dùng metric "Thời gian trung bình để AI tạo ra bản nháp tờ khai thuế" (Time to generate draft). Tuy nhiên, tôi nhận ra đây là một cái bẫy đo lường điển hình. Metric này chỉ chứng minh được tốc độ xử lý của server và thuật toán, chứ không phản ánh giá trị thực sự cho tổ chức. Nếu bản nháp được tạo ra trong 3 giây nhưng chứa đầy sai sót, kế toán viên sẽ phải tốn hàng giờ để dò lỗi và làm lại (Rework). Khi đó, "năng suất" thực chất đang giảm xuống chứ không hề tăng.

Vì vậy, tôi đã sửa giả định này và thay đổi metric thành "Thời gian từ lúc tạo nháp đến khi hoàn tất Review cuối cùng" (Time from Draft to Final Review). Sự thay đổi này giúp tôi nhìn nhận AI Adoption một cách thực tế hơn: AI không thay thế toàn bộ quy trình, mà nó phải phối hợp nhịp nhàng với con người (Human-in-the-loop). Đo lường End-to-end mới cho thấy được tốc độ thực tế mà con người được giải phóng, và đảm bảo rằng chúng ta không mù quáng đánh đổi chất lượng pháp lý (Quality) để lấy những con số tốc độ viển vông.
