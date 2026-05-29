# 01-problem-scan.md

## Thông tin cá nhân

- **Họ và tên:** Đỗ Trung Đức
- **MSSV:** 2A202600918
- **Lab:** Lab 02 — AI Product Scoping
- **Vai trò giả định:** AI Product Engineer tại Vin Smart Future
- **Mục tiêu cá nhân:** Quét các bài toán vận hành trong hệ sinh thái Vingroup, chọn 3 bài toán có tiềm năng ứng dụng AI và đánh giá nhanh bằng Quick Problem Cards.

---

# Phase 1 — SCAN: Danh sách bài toán vận hành cá nhân

## Bảng quét cơ hội

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinFast** | **Repetitive** | Nhân viên chăm sóc khách hàng phải đọc thủ công mô tả lỗi xe điện từ khách hàng và phân loại lỗi vào các nhóm như pin, sạc, phần mềm, điều hòa, phanh, cảm biến trước khi chuyển cho bộ phận kỹ thuật. |
| 2 | **Vinmec** | **Time-consuming** | Điều dưỡng và nhân viên quầy tiếp nhận phải hỏi bệnh nhân nhiều thông tin lặp lại trước khám, sau đó nhập lại vào hệ thống bệnh án; quá trình này tốn thời gian và dễ thiếu thông tin quan trọng. |
| 3 | **Vinhomes** | **Stakeholder Pain** | Ban quản lý phải xử lý nhiều phản ánh của cư dân về tiếng ồn, vệ sinh, thang máy, gửi xe, an ninh; việc đọc từng phản ánh và chuyển đúng bộ phận còn thủ công, gây chậm SLA. |
| 4 | **Vinpearl / VinWonders** | **AI-upgrade** | Nhân viên tư vấn phải trả lời lặp lại các câu hỏi của khách về lịch trình vui chơi, giờ mở cửa, combo vé, nhà hàng, show diễn và gợi ý lịch trình phù hợp với gia đình có trẻ em/người lớn tuổi. |
| 5 | **VinFast** | **Time-consuming** | Bộ phận bảo hành phải đọc lịch sử sửa chữa, log lỗi và mô tả từ khách hàng để soạn bản tóm tắt tình trạng xe trước khi kỹ thuật viên kiểm tra thực tế. |
| 6 | **Vinhomes** | **Repetitive** | Nhân viên vận hành phải tổng hợp báo cáo cuối ngày từ nhiều nguồn như phản ánh cư dân, sự cố thang máy, vệ sinh, an ninh, bãi xe; việc gom thông tin và viết báo cáo đang mất nhiều thời gian. |

---

## Nhận xét sau khi SCAN

Sau khi quét các bài toán trên, tôi nhận thấy các bài toán phù hợp với AI nhất thường có các đặc điểm:

1. **Đầu vào là ngôn ngữ tự nhiên**, ví dụ mô tả lỗi, phản ánh cư dân, câu hỏi khách hàng.
2. **Quy trình hiện tại đang có bước đọc hiểu, phân loại, tóm tắt hoặc soạn phản hồi**.
3. **AI không cần tự ra quyết định cuối cùng**, mà chỉ tạo nháp hoặc gợi ý để con người duyệt.
4. **Metric có thể đo được rõ**, ví dụ giảm thời gian xử lý, tăng tỉ lệ phân loại đúng, giảm SLA trễ.

Tôi chọn 3 bài toán tiềm năng nhất để đánh giá nhanh:

- Card #1: VinFast — AI phân loại mô tả lỗi xe điện từ khách hàng.
- Card #2: Vinhomes — AI phân loại và route phản ánh cư dân.
- Card #3: Vinmec — AI tạo phiếu tóm tắt trước khám từ thông tin bệnh nhân.

---

# Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

---

## QUICK PROBLEM CARD #1 — VinFast AI phân loại mô tả lỗi xe điện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Khách hàng VinFast mô tả lỗi xe bằng ngôn ngữ tự nhiên,     │
│ nhân viên CSKH phải đọc thủ công và phân loại lỗi trước     │
│ khi chuyển cho đúng bộ phận kỹ thuật.                       │
│                                                             │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên chăm sóc khách hàng VinFast, kỹ thuật viên bảo    │
│ hành và khách hàng đang chờ phản hồi.                       │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách gửi mô tả lỗi qua app/hotline/email              │
│   ──> 2. CSKH đọc nội dung và hỏi lại thông tin còn thiếu   │
│   ──> 3. CSKH phân loại lỗi: pin/sạc/phần mềm/cơ khí/...    │
│   ──> 4. CSKH tạo ticket và chuyển cho bộ phận phù hợp      │
│   ──> 5. Kỹ thuật viên đọc lại ticket trước khi xử lý       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-3: đọc mô tả lỗi và phân loại lỗi                    │
│ (⏱ khoảng 6-8 phút/ticket).                                 │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI hỗ trợ ở bước 2-3: trích xuất triệu chứng, hỏi lại       │
│ thông tin còn thiếu, gợi ý nhóm lỗi và mức độ ưu tiên.      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian phân loại ticket từ 8 phút xuống dưới        │
│ 2 phút/ticket; đạt ≥ 90% ticket được gợi ý đúng nhóm lỗi    │
│ trong top-2 categories.                                     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Lý do chọn Card #1

Bài toán này phù hợp với LLM vì đầu vào là mô tả lỗi bằng ngôn ngữ tự nhiên, có nhiều cách diễn đạt khác nhau từ khách hàng. Rule-based có thể xử lý một số từ khóa như “sạc”, “pin”, “màn hình”, nhưng dễ sai khi khách hàng mô tả gián tiếp, ví dụ “xe báo không nhận điện”, “đi được một lúc thì tụt pin nhanh”, “ứng dụng báo lỗi nhưng xe vẫn chạy”. AI nên đóng vai trò **gợi ý phân loại và tạo nháp ticket**, không tự kết luận nguyên nhân kỹ thuật cuối cùng.

### Ranh giới vận hành đề xuất

AI được phép:
- Trích xuất triệu chứng từ mô tả của khách hàng.
- Gợi ý nhóm lỗi và mức độ ưu tiên.
- Đề xuất câu hỏi cần hỏi thêm.
- Tạo nháp ticket cho nhân viên CSKH duyệt.

AI không được phép:
- Tự kết luận nguyên nhân hỏng xe chắc chắn.
- Tự hứa hẹn bảo hành/đổi xe/hoàn tiền.
- Tự gửi ticket sang kỹ thuật nếu chưa có nhân viên xác nhận.
- Đưa hướng dẫn sửa chữa nguy hiểm cho khách hàng tự làm.

---

## QUICK PROBLEM CARD #2 — Vinhomes AI phân loại và route phản ánh cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Cư dân Vinhomes gửi nhiều phản ánh trên app, ban quản lý    │
│ phải đọc thủ công, phân loại nội dung và chuyển cho đúng    │
│ bộ phận xử lý.                                              │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên ban quản lý tòa nhà, bộ phận kỹ thuật, vệ sinh,   │
│ an ninh và cư dân đang chờ phản hồi.                        │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Cư dân gửi phản ánh qua app/call center                │
│   ──> 2. Nhân viên ban quản lý đọc nội dung                 │
│   ──> 3. Phân loại: thang máy/vệ sinh/an ninh/bãi xe/...    │
│   ──> 4. Chuyển phản ánh cho bộ phận phụ trách              │
│   ──> 5. Theo dõi trạng thái xử lý và phản hồi cư dân       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-4: đọc, phân loại và route phản ánh                  │
│ (⏱ khoảng 5-10 phút/phản ánh, lâu hơn vào giờ cao điểm).    │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI hỗ trợ ở bước 2-4: tóm tắt phản ánh, phân loại mức độ    │
│ khẩn cấp, gợi ý bộ phận xử lý và tạo nháp phản hồi ban đầu. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ 85% phản ánh được phân loại và gợi ý route trong dưới       │
│ 30 giây; giảm SLA trễ từ 20% xuống dưới 8%.                 │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Lý do chọn Card #2

Bài toán này có volume lớn và lặp lại hằng ngày. Nhiều phản ánh của cư dân có dạng ngôn ngữ tự nhiên, đôi khi cảm xúc cao, thiếu thông tin hoặc chứa nhiều vấn đề trong một tin nhắn. LLM có thể giúp tóm tắt, phân loại, gợi ý độ ưu tiên và tạo phản hồi nháp lịch sự. Tuy nhiên, quyết định xử lý cuối cùng vẫn cần ban quản lý duyệt, nhất là các trường hợp liên quan đến tranh chấp, chi phí, an ninh hoặc an toàn.

### Ranh giới vận hành đề xuất

AI được phép:
- Tóm tắt phản ánh của cư dân.
- Phân loại chủ đề và mức độ khẩn cấp.
- Gợi ý bộ phận xử lý.
- Tạo nháp phản hồi ban đầu.

AI không được phép:
- Tự cam kết bồi thường, miễn phí dịch vụ hoặc xử lý pháp lý.
- Tự đóng ticket khi chưa có nhân viên xác nhận.
- Tự đưa thông tin cá nhân cư dân cho bộ phận không liên quan.
- Tự xử lý các case an ninh nghiêm trọng mà không báo con người.

---

## QUICK PROBLEM CARD #3 — Vinmec AI tạo phiếu tóm tắt trước khám

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Trước khi khám, nhân viên Vinmec phải hỏi và nhập lại       │
│ nhiều thông tin của bệnh nhân, khiến thời gian tiếp nhận    │
│ kéo dài và bác sĩ vẫn phải đọc lại nhiều dữ liệu rời rạc.   │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên tiếp nhận, điều dưỡng, bác sĩ và bệnh nhân đang   │
│ chờ khám.                                                   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Bệnh nhân đến quầy hoặc đặt lịch qua app               │
│   ──> 2. Nhân viên hỏi lý do khám, triệu chứng, tiền sử     │
│   ──> 3. Nhân viên nhập thông tin vào hệ thống              │
│   ──> 4. Điều dưỡng/bác sĩ đọc lại thông tin trước khám     │
│   ──> 5. Bác sĩ hỏi lại để xác nhận thông tin còn thiếu     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-4: thu thập, nhập và đọc lại thông tin               │
│ (⏱ khoảng 10-15 phút/bệnh nhân).                            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI hỗ trợ ở bước 2-4: tạo phiếu tóm tắt trước khám, liệt    │
│ kê triệu chứng chính, tiền sử liên quan và câu hỏi cần hỏi. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian tiếp nhận và tóm tắt trước khám từ 15 phút   │
│ xuống dưới 5 phút/bệnh nhân; 95% phiếu có đủ trường thông   │
│ tin bắt buộc sau khi nhân viên xác nhận.                    │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Lý do chọn Card #3

Bài toán này có giá trị vận hành lớn vì giảm thời gian chờ khám và giúp bác sĩ có bản tóm tắt dễ đọc hơn. Tuy nhiên, đây là bài toán nhạy cảm vì liên quan đến y tế. Vì vậy AI chỉ nên làm nhiệm vụ **hỗ trợ hành chính và tóm tắt thông tin**, không được chẩn đoán, kê đơn hoặc đưa lời khuyên y khoa độc lập.

### Ranh giới vận hành đề xuất

AI được phép:
- Tạo nháp phiếu tóm tắt trước khám.
- Trích xuất triệu chứng, thời gian xuất hiện, tiền sử liên quan.
- Đề xuất câu hỏi cần hỏi thêm để hoàn thiện hồ sơ.
- Đánh dấu thông tin còn thiếu.

AI không được phép:
- Tự chẩn đoán bệnh.
- Tự kê đơn thuốc hoặc đề xuất điều trị.
- Tự phân luồng cấp cứu nếu không có nhân viên y tế xác nhận.
- Tự lưu hồ sơ cuối cùng khi chưa được nhân viên Vinmec duyệt.

---

# Tổng kết lựa chọn cá nhân

## Bảng so sánh nhanh 3 bài toán

| Tiêu chí | Card #1 VinFast lỗi xe | Card #2 Vinhomes phản ánh cư dân | Card #3 Vinmec trước khám |
|---|---:|---:|---:|
| Workflow rõ ràng | Cao | Cao | Cao |
| Có nhiều dữ liệu ngôn ngữ tự nhiên | Cao | Cao | Cao |
| Metric dễ đo | Cao | Cao | Trung bình - Cao |
| Rủi ro nếu AI sai | Trung bình | Trung bình | Cao |
| Cần Human-in-the-loop | Có | Có | Bắt buộc |
| Phù hợp làm prototype prompt | Cao | Cao | Trung bình |
| Khả năng chọn cho bài nhóm | Rất tốt | Rất tốt | Cần thận trọng |

## Đề xuất cá nhân cho nhóm

Tôi đề xuất nhóm cân nhắc chọn **Card #1 — VinFast AI phân loại mô tả lỗi xe điện từ khách hàng** để làm Deep-Dive.

Lý do:

1. Bài toán có workflow vận hành rõ và dễ vẽ sơ đồ.
2. Đầu vào là ngôn ngữ tự nhiên nên LLM có vai trò hợp lý.
3. Có thể thiết kế prototype prompt đơn giản nhưng vẫn thể hiện được ranh giới an toàn.
4. Metric đo được rõ: thời gian phân loại ticket, độ chính xác phân loại, tỉ lệ cần hỏi lại.
5. Rủi ro thấp hơn bài toán y tế vì AI chỉ tạo nháp ticket và không tự kết luận kỹ thuật cuối cùng.

Nếu nhóm muốn chọn hướng ít rủi ro pháp lý/y tế và dễ làm trong lab, Card #1 là lựa chọn phù hợp nhất.
