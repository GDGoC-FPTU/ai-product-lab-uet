# 01-problem-scan.md

# Phase 1 — SCAN

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | Xanh SM | Tốn thời gian | Điều phối viên xử lý thủ công các sự cố xe điện pin yếu/hết pin của tài xế, phải tra cứu vị trí, trạm sạc và soạn tin nhắn hướng dẫn. |
| 2 | Xanh SM | Stakeholder Pain | Phân tích lý do khách hàng hủy chuyến từ ghi chú tài xế và cuộc gọi CSKH để tìm nguyên nhân phổ biến gây rò rỉ cuốc. |
| 3 | VinFast | AI-upgrade | Hỗ trợ khách hàng tìm trạm sạc phù hợp với dòng xe, loại cổng sạc và tình trạng pin hiện tại. |
| 4 | Vinhomes | Lặp lại | Phân loại và điều hướng phản ánh cư dân như mất nước, hỏng đèn, tiếng ồn đến đúng ban quản lý hoặc đội kỹ thuật. |
| 5 | Vinmec | Tốn thời gian | Hỗ trợ bác sĩ soạn thảo tóm tắt hồ sơ xuất viện từ bệnh án, xét nghiệm và ghi chú điều trị. |

---

# Phase 2 — QUICK-ASSESS

## QUICK PROBLEM CARD #1

**Bài toán:** Tài xế Xanh SM báo xe điện pin yếu hoặc gần hết pin, cần điều phối viên hỗ trợ tìm trạm sạc gần nhất hoặc gọi xe sạc pin di động.

**Công ty thành viên:** Xanh SM

**Ai đang đau?**  
Tài xế Xanh SM và điều phối viên trung tâm vận hành.

**Workflow thủ công hiện tại:**
1. Tài xế gọi hoặc nhắn về trung tâm điều vận khi xe báo pin yếu.
2. Điều phối viên kiểm tra biển số xe, vị trí GPS và mức pin hiện tại.
3. Điều phối viên tra cứu thủ công trạm sạc VinFast gần nhất còn khả dụng.
4. Điều phối viên soạn tin nhắn hướng dẫn tài xế đi đến trạm sạc.
5. Nếu pin quá thấp, điều phối viên gọi đội xe sạc pin di động/cứu hộ.

**Bước tốn thời gian/lỗi nhất:**  
Bước 3–4: tra cứu trạm sạc và soạn hướng dẫn, mất khoảng 10–12 phút/lượt.

**AI có thể hỗ trợ ở bước nào?**  
AI hỗ trợ tóm tắt tình huống, kiểm tra rule an toàn, đề xuất hành động và soạn nháp tin nhắn cho tài xế.

**Metric đo thành công:**  
Giảm thời gian xử lý sự cố từ khoảng 15 phút xuống dưới 3 phút/lượt.

**Quick Architecture:**  
LLM Feature + Rule + Human-in-the-loop.

---

## QUICK PROBLEM CARD #2

**Bài toán:** Phân loại và điều hướng phản ánh cư dân Vinhomes đến đúng bộ phận xử lý.

**Công ty thành viên:** Vinhomes

**Ai đang đau?**  
Ban quản lý tòa nhà và cư dân.

**Workflow thủ công hiện tại:**
1. Cư dân gửi phản ánh qua app hoặc hotline.
2. Nhân viên đọc nội dung phản ánh.
3. Nhân viên xác định nhóm vấn đề: điện, nước, vệ sinh, an ninh, tiếng ồn.
4. Nhân viên chuyển phản ánh đến bộ phận phụ trách.
5. Bộ phận xử lý phản hồi lại cư dân.

**Bước tốn thời gian/lỗi nhất:**  
Bước 2–4, mất khoảng 5–10 phút/phản ánh, dễ route sai nếu nội dung không rõ.

**AI có thể hỗ trợ ở bước nào?**  
LLM phân loại nội dung phản ánh, tóm tắt vấn đề và đề xuất bộ phận xử lý.

**Metric đo thành công:**  
85% phản ánh được phân loại trong dưới 30 giây, giảm thời gian phản hồi ban đầu từ 10 phút xuống dưới 2 phút.

**Quick Architecture:**  
LLM Feature + Rule.

---

## QUICK PROBLEM CARD #3

**Bài toán:** Hỗ trợ bác sĩ Vinmec soạn thảo tóm tắt hồ sơ xuất viện.

**Công ty thành viên:** Vinmec

**Ai đang đau?**  
Bác sĩ điều trị và bệnh nhân chờ hồ sơ xuất viện.

**Workflow thủ công hiện tại:**
1. Bác sĩ mở bệnh án điện tử.
2. Bác sĩ đọc lại chẩn đoán, xét nghiệm, thuốc và diễn biến điều trị.
3. Bác sĩ viết tóm tắt xuất viện.
4. Điều dưỡng hoặc bộ phận hành chính kiểm tra thông tin.
5. Bệnh nhân nhận hồ sơ xuất viện.

**Bước tốn thời gian/lỗi nhất:**  
Bước 2–3, mất khoảng 20–30 phút/bệnh nhân.

**AI có thể hỗ trợ ở bước nào?**  
AI trích xuất thông tin chính và tạo bản nháp tóm tắt xuất viện.

**Metric đo thành công:**  
Giảm thời gian soạn tóm tắt từ 30 phút xuống dưới 10 phút/bệnh nhân.

**Quick Architecture:**  
LLM Feature + Human-in-the-loop.