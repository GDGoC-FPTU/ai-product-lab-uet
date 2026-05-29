# 📖 Báo Cáo Nhóm — Lab 02: AI Product Deep-Dive (Vin Smart Future)

- **Tên nhóm:** UET
- **Thành viên nhóm:**
  1.  Cao Đặng Quốc Vương - MSSV: 2A202600738 - Lớp: C401
  2.  Hoàng Trung Quân - MSSV: 2A202600720 - Lớp: C401
  3.  Đỗ Trung Đức - MSSV: 2A202600918 - Lớp: C401
  4.  Vương Nguyệt Bình - MSSV: 2A202600932 - Lớp C401

---

## 🗳️ Quyết định lựa chọn bài toán làm Deep-Dive

Nhóm chúng tôi quyết định lựa chọn bài toán: **"GSM (Xanh SM) — Tự động phát hiện và hiệu chỉnh tọa độ điểm đón bị lệch dựa trên mô tả văn bản của khách hàng"** để tiến hành Deep-Dive.

### Lý do lựa chọn và loại bỏ các thẻ bài toán khác:

- **Lý do chọn bài toán GSM:** Lệch điểm ghim đón (pickup pin) là một "nỗi đau" cực kỳ phổ biến và nhức nhối trong thực tế vận hành hàng ngày của Xanh SM tại các khu đô thị lớn, ảnh hưởng trực tiếp đến trải nghiệm khách hàng và hiệu suất của tài xế. Việc giải quyết bài toán này mang lại giá trị kinh tế tức thì và nâng cao rõ rệt chỉ số hài lòng (CSAT).
- **Loại bỏ Vinhomes (Khiếu nại cư dân):** Việc tự động hóa phản hồi khiếu nại mang tính chất nhạy cảm pháp lý, đòi hỏi quy trình đối chiếu quy chế phức tạp và rủi ro tranh chấp cao nếu AI phản hồi không chuẩn xác.
- **Loại bỏ Vinmec (Bệnh sử lâm sàng):** Tác vụ safety-critical ảnh hưởng trực tiếp đến sức khỏe con người, cần sự kiểm định y khoa cực kỳ khắt khe và tích hợp phức tạp vào hệ thống EHR chuẩn quốc tế nên khó khả thi cho một prototype nhanh.

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)

**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:

- 🔴 **Bottleneck:** Bước 4 & 5 — Gọi điện hỏi đường để mô tả địa hình và tài xế phải di chuyển dò dẫm tìm kiếm khách hàng thủ công.
- 🔄 **Handoff:** Khách hàng ghim vị trí và nhập ghi chú địa chỉ trên App (Bước 1) → Hệ thống chuyển thông tin chuyến đi cho tài xế (Bước 2) → Tài xế và khách hàng trực tiếp gọi điện thoại giao tiếp hỏi đường (Bước 4).
- Ghi rõ thời gian vận hành trung bình: **Tổng cộng = 13 phút/lượt**.

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách đặt xe │ ──→ │ Hệ thống tạo │ ──→ │ Tài xế đến   │ ──→ │ Gọi điện     │
│ & ghim vị trí│     │ chuyến đi    │     │ điểm ghim    │     │ hỏi đường    │
│ Ai: Khách    │     │ Ai: App/GPS  │     │ Ai: Tài xế   │     │ Ai: TX & KH  │
│ ⏱ 1 phút     │     │ ⏱ 1 phút   │     │ ⏱ 5 phút     │     │ ⏱ 1 phút 🔴  │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                       │
                                                                       ▼
                                                                ┌──────────────┐
                                                                │ Bước 5       │
                                                                │ Tài xế di    │
                                                                │ chuyển tìm   │
                                                                │ kiếm khách   │
                                                                │ Ai: Tài xế   │
                                                                │ ⏱ 5 phút 🔴  │
                                                                └──────────────┘
```

## 3.2. Problem Statement (6-field) & Metrics (15 min)

Điền đầy đủ 6 trường thông tin của bài toán:

| Field                       | Nội dung chi tiết                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Actor / Operator**     | Tài xế Xanh SM (mất thời gian đi tìm khách) và Khách hàng (bực bối vì chờ đợi lâu).                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| **2. Current Workflow**     | Khách hàng đặt xe trên App Xanh SM và ghim vị trí đón. Nếu ghim bị lệch (do ngõ sâu, khu chung cư nhiều sảnh phức tạp như Vinhomes Ocean Park/Times City, hoặc định vị GPS bị trôi), tài xế di chuyển đến đúng điểm ghim nhưng không thấy khách. Hai bên phải liên tục gọi điện thoại mô tả vị trí thực tế, sau đó tài xế lái xe tìm kiếm khách hàng thủ công. Quy trình mất khoảng 9.5 phút/lượt.                                                                                                                        |
| **3. Bottleneck**           | Bước 4 & 5 (mất ~5 phút): Việc gọi điện giao tiếp hỏi đường thủ công rất dễ gây hiểu lầm do mô tả địa hình không rõ ràng và tài xế phải di chuyển dò dẫm trong các khu vực phức tạp mà không có định vị chính xác trên bản đồ.                                                                                                                                                                                                                                                                                            |
| **4. Business Impact**      | Tỷ lệ lệch ghim tại các đô thị lớn chiếm ~25% tổng số chuyến đi. Gây thất thoát doanh thu đáng kể (tài xế chạy ít chuyến hơn trong ca làm việc, tỷ lệ hủy chuyến do khách chờ lâu tăng 12%). Lãng phí chi phí cuộc gọi hỏi đường của tài xế và làm giảm đáng kể mức độ hài lòng (CSAT) của khách hàng đối với dịch vụ Xanh SM.                                                                                                                                                                                            |
| **5. Success Metric**       | 1. Giảm thời gian tài xế tìm kiếm khách hàng từ trung bình 5 phút xuống dưới 1 phút.<br>2. Giảm 90% số lượng cuộc gọi hỏi đường/mô tả địa hình giữa tài xế và khách hàng.<br>3. Giảm tỷ lệ khách hàng hủy chuyến do lệch ghim từ 12% xuống dưới 2%.                                                                                                                                                                                                                                                                       |
| **6. Operational Boundary** | AI được phép đọc hiểu ghi chú địa chỉ dạng văn bản của khách hàng (VD: "đón ở sảnh S2.12 Vinhomes Ocean Park"), đối chiếu với cơ sở dữ liệu các sảnh tòa nhà và tọa độ thực tế để đề xuất dịch chuyển điểm ghim (pickup pin offset) trên bản đồ.<br>**CẤM:** AI không được tự ý đổi điểm ghim mà không hiển thị thông báo xác nhận rõ ràng cho khách hàng duyệt (HITL trên App khách hàng). AI không được dịch chuyển điểm ghim lệch quá 500m so với vị trí GPS ban đầu của khách hàng để tránh lỗi định vị nghiêm trọng. |

## 3.3. Future-State Flow & AI Fit (25 min)

- **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [x] LLM Feature [ ] Agentic Loop.
- **Vẽ Future-State Flow:** Đánh dấu rõ:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách đặt xe │ ──→ │ 🔵 AI phân   │ ──→ │ 🟢 Khách xác │ ──→ │ Tài xế đến   │
│ & ghi chú    │     │ tích ghi chú │     │ nhận điểm    │     │ điểm ghim    │
│ địa chỉ      │     │ và sửa ghim  │     │ ghim mới     │     │ chính xác    │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                       │
                                                                       ▼
                                                                ↩️ Fallback:
                                                                Nếu AI đề xuất
                                                                sai hoặc lỗi,
                                                                giữ nguyên ghim
                                                                GPS ban đầu &
                                                                tài xế gọi điện.
```

- 🔵 **AI Step:** Bước 2 — Hệ thống sử dụng LLM để phân tích ghi chú text không cấu trúc của khách hàng (VD: "đón ở sảnh S2.12 Vinhomes Ocean Park"), đối chiếu với cơ sở dữ liệu sảnh tòa nhà để tính toán tọa độ chính xác và đề xuất dịch chuyển điểm ghim đón trên App.
- 🟢 **Human Step (HITL):** Bước 3 — Khách hàng xác nhận gợi ý của AI: "Có phải bạn muốn đón ở sảnh S2.12?" trước khi cập nhật chính thức điểm ghim đón chính xác cho tài xế.
- ↩️ **Fallback:** Nếu mô hình LLM không thể phân tích được ghi chú (hoặc độ tự tin thấp < 85%) hoặc hệ thống gặp lỗi kỹ thuật → giữ nguyên điểm ghim GPS ban đầu của khách hàng và tài xế chủ động gọi điện hỗ trợ như quy trình cũ.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:

1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? → Có: Logs lịch sử chat của tài xế và tọa độ ghim ban đầu so với tọa độ đón thực tế trong lịch sử chuyến đi của Xanh SM.
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? → Có: Khách hàng xác nhận ghim đề xuất trước khi cập nhật + giới hạn khoảng cách dịch ghim < 500m để tránh lỗi định vị nghiêm trọng.
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? → Có: Cả tài xế và khách hàng đều rất mong muốn giải quyết triệt để vấn đề lệch ghim đón phiền toái này.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp (thử nghiệm trước tại các khu đô thị lớn như Vinhomes Ocean Park và Vinhomes Times City).
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**

> 1. **Tính khả thi kỹ thuật:** Sử dụng mô hình LLM nhẹ (Gemini 2.5 Flash) để phân tích văn bản ghi chú tiếng Việt không cấu trúc của khách hàng rất nhanh chóng (thời gian phản hồi < 1.5s, độ chính xác cao nhờ fine-tune nhẹ hoặc few-shot với danh mục địa điểm nội bộ).
> 2. **Hiệu quả kinh tế:** Giảm thời gian chờ đợi và tìm khách giúp mỗi tài xế chạy thêm được 1-2 chuyến/ngày, giảm tỷ lệ hủy chuyến, tăng đáng kể doanh thu của GSM và nâng cao chỉ số hài lòng CSAT của khách hàng.
> 3. **Mức độ an toàn cao:** Có sự xác nhận của khách hàng (HITL) cùng với rào cản kỹ thuật giới hạn bán kính dịch chuyển điểm ghim dưới 500m giúp ngăn ngừa mọi sự cố định vị sai lệch sang khu vực khác.
