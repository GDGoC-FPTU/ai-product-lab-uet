# 📖 Bài Cá Nhân — Lab 02: AI Product Scoping (Vin Smart Future)

*   **Họ và tên:** Cao Đặng Quốc Vương
*   **Mã số sinh viên (MSSV):** 2A202600738 
*   **Lớp:** C401
*   **Nhóm:** UET

---

# 🔍 Phase 1 — SCAN (Cá nhân)

> Liệt kê **tối thiểu 5 bài toán** thực tế tại các công ty thành viên Vingroup.
> Lens hợp lệ: `Lặp lại` · `Tốn thời gian` · `AI-upgrade` · `Stakeholder Pain`.

| # | Subsidiary | Lens | Mô tả ngắn bài toán & Bottleneck |
|---|------------|------|----------------------------------|
| 1 | VinFast | Lặp lại | Tự động kiểm tra và đối chiếu các giấy tờ đăng ký biển số xe trực tuyến của khách hàng (CCCD, hóa đơn VAT mua xe, giấy chứng nhận xuất xưởng) với cơ sở dữ liệu sản xuất của VinFast để phát hiện sai sót thông tin trước khi gửi lên cơ quan chức năng. |
| 2 | Xanh SM | Stakeholder Pain | Định vị điểm đón khách (pickup pin) không chính xác tại các khu vực phức tạp (ngõ hẻm sâu, tòa nhà nhiều sảnh, đường có dải phân cách) khiến tài xế mất trung bình 3-5 phút tìm kiếm, phải gọi điện liên tục và làm khách hàng ức chế vì chờ đợi lâu. |
| 3 | Vinhomes | Tốn thời gian | Đọc hiểu các khiếu nại phức tạp của cư dân Vinhomes trên App, đối chiếu với quy chế vận hành tòa nhà để tự động đề xuất phương án xử lý tối ưu và dự thảo phản hồi giải pháp hợp lý cho cư dân (giúp BQL giảm thời gian nghiên cứu quy định và soạn thảo thủ công). |
| 4 | Vinmec | AI-upgrade | Tự động truy vấn, phân tích và tổng hợp hàng chục trang tài liệu bệnh sử cũ, đơn thuốc và kết quả xét nghiệm cận lâm sàng của bệnh nhân khi nhập viện thành một bảng tóm tắt cấu trúc (Bệnh nền, Dị ứng, Lưu ý lâm sàng) giúp bác sĩ có cái nhìn toàn diện tức thì trước khi khám bệnh. |
| 5 | Vinpearl | Stakeholder Pain | Khách hàng bức xúc vì thủ tục trả phòng (Check-out) và đối chiếu chi phí phát sinh quá chậm. Vào giờ cao điểm trả phòng, khách hàng phải đứng chờ lễ tân 15-20 phút để nhân viên buồng phòng kiểm tra thực tế phòng (minibar, đồ dùng) và đối chiếu thủ công các hóa đơn dịch vụ ăn uống, spa khách đã ký nợ trong kỳ nghỉ, dễ gây trễ giờ ra sân bay và ức chế cho khách. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân)

> Chọn **top 3 bài toán** từ bảng SCAN và hoàn thiện 3 thẻ dưới đây.
> Metric bắt buộc phải **có con số cụ thể**.

## 🃏 QUICK PROBLEM CARD #1

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                        │
│                                                              │
│ Bài toán (1 câu): Tự động phát hiện và hiệu chỉnh tọa độ    │
│ điểm đón bị lệch dựa trên mô tả văn bản của khách hàng.     │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes   │
│                     [ ] Vinmec   [ ] Vinpearl  [ ] Khác:____  │
│                                                              │
│ Ai đang đau (Actor)?                                         │
│ - Tài xế Xanh SM (mất thời gian đi tìm khách).               │
│ - Khách hàng (bực bối vì phải chờ đợi lâu).                  │
│                                                              │
│ Workflow thủ công hiện tại (3-5 bước):                       │
│   1. Đặt xe trên app ──> 2. Điểm ghim bị lệch ──>            │
│   3. Tài xế đến điểm ghim không thấy khách ──>               │
│   4. Hai bên gọi điện hỏi đường ──> 5. Tài xế đi tìm khách   │
│                                                              │
│ Bước tốn thời gian/lỗi nhất: Bước 3 & 4 (⏱ 5 phút/lượt)      │
│ AI hỗ trợ ở bước nào: Bước 2 & 3 (LLM đọc hiểu mô tả địa chỉ │
│ của khách để tự động hiệu chỉnh điểm đón chính xác nhất).    │
│                                                              │
│ Metric đo thành công (có số):                                │
│ - Giảm thời gian tìm khách từ 5 phút xuống dưới 1 phút.      │
│ - Giảm 90% số lượng cuộc gọi hỏi đường giữa tài xế và khách. │
│                                                              │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```

## 🃏 QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                        │
│                                                              │
│ Bài toán (1 câu): Đọc hiểu và phân loại phản ánh của cư dân │
│ để tự động đề xuất giải pháp xử lý theo quy chế và soạn     │
│ dự thảo phản hồi.                                            │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes   │
│                     [ ] Vinmec   [ ] Vinpearl  [ ] Khác:____  │
│                                                              │
│ Ai đang đau (Actor)?                                         │
│ - Ban quản lý Vinhomes (quá tải xử lý ý kiến).                │
│ - Cư dân Vinhomes (chờ lâu, phản hồi rập khuôn).             │
│                                                              │
│ Workflow thủ công hiện tại (3-5 bước):                       │
│   1. Nhận phản ánh qua App ──> 2. Đọc & phân loại thủ công   │
│   ──> 3. Tra cứu quy chế tòa nhà để đề xuất giải pháp        │
│   ──> 4. Soạn thư/tin phản hồi ──> 5. Gửi kỹ thuật viên      │
│                                                              │
│ Bước tốn thời gian/lỗi nhất: Bước 3 & 4 (⏱ 10 phút/lượt)     │
│ AI hỗ trợ ở bước nào: Bước 2, 3 & 4 (LLM đọc ý kiến, tra cứu │
│ quy chế để đề xuất giải pháp và soạn dự thảo phản hồi).      │
│                                                              │
│ Metric đo thành công (có số):                                │
│ - Giảm thời gian phản hồi ban đầu từ 120 phút ──> dưới 5 phút│
│ - Tăng tỷ lệ hài lòng của cư dân với phản hồi đầu lên 90%.   │
│                                                              │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent  │
└─────────────────────────────────────────────────────────────┘
```

## 🃏 QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                        │
│                                                              │
│ Bài toán (1 câu): Trợ lý AI tự động truy vấn và tổng hợp    │
│ lịch sử bệnh án, đơn thuốc cũ thành bảng tóm tắt lâm sàng.   │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes   │
│                     [x] Vinmec   [ ] Vinpearl  [ ] Khác:____  │
│                                                              │
│ Ai đang đau (Actor)?                                         │
│ - Bác sĩ điều trị (quá tải thời gian đọc và chẩn đoán).      │
│ - Bệnh nhân (nguy cơ bị bỏ sót các thông tin dị ứng).        │
│                                                              │
│ Workflow thủ công hiện tại (3-5 bước):                       │
│   1. Bệnh nhân khám ──> 2. Bác sĩ tìm hồ sơ cũ trên EHR ──>  │
│   3. Bác sĩ đọc thủ công hàng chục trang pdf bệnh sử cũ ──>  │
│   4. Bác sĩ tự ghi chép lại các điểm lâm sàng quan trọng     │
│                                                              │
│ Bước tốn thời gian/lỗi nhất: Bước 3 & 4 (⏱ 8 phút/lượt)      │
│ AI hỗ trợ ở bước nào: Bước 2, 3 & 4 (Hệ thống RAG/Agent tự   │
│ động trích xuất cấu trúc tiền sử bệnh, dị ứng và thuốc).     │
│                                                              │
│ Metric đo thành công (có số):                                │
│ - Giảm thời gian tổng hợp bệnh sử từ 8 phút ──> dưới 1 phút. │
│ - 0% sự cố bỏ sót thông tin dị ứng thuốc nghiêm trọng.       │
│                                                              │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent  │
└─────────────────────────────────────────────────────────────┘
```
