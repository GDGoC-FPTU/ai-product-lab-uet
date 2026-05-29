# 03-ai-log.md

## Thông tin cá nhân

- **Họ và tên:** Đỗ Trung Đức
- **MSSV:** 2A202600918
- **Lab:** Lab 02 — AI Product Scoping
- **Vai trò giả định:** AI Product Engineer tại Vin Smart Future

---

# AI Log & Reflection

## 1. Tôi đã dùng AI để làm gì?

Trong bài cá nhân này, tôi sử dụng AI như một **thought-partner** để hỗ trợ ba việc chính:

1. **Brainstorm bài toán vận hành trong hệ sinh thái Vingroup**  
   Tôi yêu cầu AI gợi ý các pain point vận hành có thể xảy ra trong các công ty như VinFast, Vinhomes, Vinmec và Vinpearl. Mục tiêu không phải là lấy nguyên câu trả lời của AI, mà là dùng nó để mở rộng danh sách ý tưởng ban đầu.

2. **Kiểm tra xem bài toán có thật sự cần AI hay không**  
   Sau khi có danh sách ý tưởng, tôi yêu cầu AI phản biện theo góc nhìn của quản lý vận hành và CFO. Tôi tập trung vào câu hỏi: bài toán này có cần LLM không, hay chỉ cần rule-based system là đủ?

3. **Chuẩn hóa ý tưởng thành Quick Problem Cards**  
   Tôi dùng AI để kiểm tra xem mỗi card đã có đủ các thành phần chưa: actor, workflow thủ công, bottleneck, metric, bước AI can thiệp và ranh giới vận hành.

---

## 2. AI đã giúp tôi như thế nào?

AI giúp tôi ở các điểm sau:

### 2.1. Mở rộng phạm vi ý tưởng

Ban đầu tôi chỉ nghĩ đến các bài toán quen thuộc như chatbot chăm sóc khách hàng hoặc điều phối xe. Sau khi hỏi AI, tôi có thêm các hướng cụ thể hơn như:

- Phân loại mô tả lỗi xe điện tại VinFast.
- Phân loại và route phản ánh cư dân tại Vinhomes.
- Tạo phiếu tóm tắt trước khám tại Vinmec.
- Tư vấn lịch trình vui chơi cho khách Vinpearl.
- Tổng hợp báo cáo vận hành cuối ngày cho ban quản lý tòa nhà.

Điểm hữu ích là AI giúp tôi nhìn bài toán không chỉ dưới góc độ “ứng dụng AI”, mà còn dưới góc độ **workflow vận hành**: ai làm, làm bằng công cụ gì, mất thời gian ở bước nào.

### 2.2. Giúp tôi ép ý tưởng phải có metric

Khi tự nghĩ ý tưởng, tôi dễ viết chung chung như “giúp xử lý nhanh hơn” hoặc “tăng trải nghiệm khách hàng”. AI nhắc tôi phải đưa metric có số, ví dụ:

- Giảm thời gian phân loại ticket từ 8 phút xuống dưới 2 phút.
- 85% phản ánh cư dân được phân loại trong dưới 30 giây.
- Giảm thời gian tiếp nhận trước khám từ 15 phút xuống dưới 5 phút.

Nhờ vậy, các ý tưởng trở nên dễ đánh giá hơn và phù hợp với yêu cầu của lab.

### 2.3. Giúp tôi xác định ranh giới vận hành

AI cũng giúp tôi nhìn rõ rằng trong các bài toán này, hệ thống không nên tự ra quyết định cuối cùng. Ví dụ:

- Với VinFast, AI không được tự kết luận nguyên nhân hỏng xe hoặc hứa hẹn đổi xe.
- Với Vinhomes, AI không được tự cam kết bồi thường hoặc đóng ticket.
- Với Vinmec, AI không được chẩn đoán, kê đơn hoặc đưa lời khuyên điều trị.

Điều này giúp tôi thiết kế bài toán theo hướng an toàn hơn: AI chỉ tạo **draft/gợi ý**, còn con người vẫn duyệt.

---

## 3. AI đã sai hoặc chưa tốt ở đâu?

AI có một số điểm chưa tốt mà tôi phải sửa lại.

### 3.1. AI hay đề xuất bài toán quá rộng

Ở lần brainstorm đầu tiên, AI đưa ra các ý tưởng rất lớn như “xây dựng hệ thống AI tối ưu toàn bộ vận hành VinFast” hoặc “AI quản lý toàn bộ đô thị thông minh Vinhomes”. Những ý tưởng này nghe hay nhưng quá rộng, không phù hợp với lab vì khó vẽ workflow, khó đo metric và khó làm prototype prompt.

Tôi phải thu hẹp lại thành các bài toán nhỏ hơn, ví dụ:

- Không chọn “AI quản lý toàn bộ dịch vụ hậu mãi VinFast”.
- Thu hẹp thành “AI phân loại mô tả lỗi xe điện từ khách hàng trước khi tạo ticket”.

### 3.2. AI đôi khi gán số liệu quá tự tin

AI có xu hướng đưa ra các con số như số lượng ticket mỗi ngày, chi phí tiết kiệm mỗi tháng hoặc tỉ lệ lỗi hiện tại mà không có nguồn kiểm chứng. Tôi không thể dùng các số đó như sự thật. Vì vậy, tôi chuyển các con số thành **ước lượng giả định phục vụ scoping**, ví dụ thời gian 6-8 phút/ticket hoặc 10-15 phút/bệnh nhân.

Khi viết bài, tôi tránh khẳng định rằng đây là số liệu chính thức của Vingroup. Tôi chỉ dùng chúng như baseline giả định để minh họa metric.

### 3.3. AI đôi khi đề xuất Agent quá sớm

Với một số bài toán, AI gợi ý dùng Agent tự động gọi API, tự route ticket và tự gửi phản hồi. Tôi thấy cách này rủi ro vì lab yêu cầu xác định rõ operational boundary. Trong các bài toán cá nhân, tôi chuyển kiến trúc về **LLM Feature có Human-in-the-loop**, thay vì Agent tự trị.

Ví dụ với Vinhomes, AI chỉ nên:
- Tóm tắt phản ánh.
- Gợi ý category.
- Gợi ý bộ phận xử lý.
- Tạo nháp phản hồi.

Nhân viên ban quản lý vẫn là người bấm xác nhận.

---

## 4. Tôi đã sửa prompt hoặc kiểm chứng lại như thế nào?

Tôi sửa cách hỏi AI theo 3 bước.

### Bước 1: Ép AI đưa bài toán theo format vận hành

Thay vì hỏi chung chung “hãy nghĩ ý tưởng AI cho Vingroup”, tôi hỏi theo dạng:

```text
Tôi là AI Product Engineer tại Vin Smart Future. 
Hãy đề xuất các bài toán vận hành cụ thể trong VinFast/Vinhomes/Vinmec.
Mỗi bài toán phải có actor, workflow thủ công, bottleneck, metric đo được và ranh giới AI không được vượt qua.
```

Cách hỏi này làm AI trả lời sát yêu cầu hơn.

### Bước 2: Yêu cầu AI phản biện như CFO/Operations Manager

Tôi dùng prompt phản biện:

```text
Hãy đóng vai CFO và Trưởng phòng Vận hành khó tính.
Với bài toán này, hãy chỉ ra vì sao có thể không cần AI, vì sao rule-based system có thể đủ, và metric nào còn yếu.
```

Nhờ vậy tôi loại bỏ những ý tưởng quá mơ hồ hoặc không có bottleneck rõ.

### Bước 3: Kiểm tra lại bằng tiêu chí của lab

Tôi tự kiểm tra từng Quick Problem Card bằng các câu hỏi:

- Có actor cụ thể không?
- Có workflow 3-5 bước không?
- Có bước bottleneck và thời gian ước tính không?
- AI nhảy vào đúng bước có xử lý ngôn ngữ/tóm tắt/phân loại không?
- Metric có số không?
- Có ranh giới AI không được vượt qua không?

Những card chưa đạt thì tôi sửa lại trước khi đưa vào file cuối.

---

## 5. Điều tôi học được sau khi dùng AI làm thought-partner

Điều quan trọng nhất tôi học được là: **không phải bài toán nào nghe có vẻ “AI” cũng nên dùng AI**.

Một bài toán tốt cho AI Product Scoping cần có:

1. Workflow hiện tại rõ ràng.
2. Actor đang thật sự đau.
3. Bottleneck cụ thể.
4. Metric đo được.
5. Đầu vào phù hợp với AI, đặc biệt là ngôn ngữ tự nhiên hoặc thông tin bán cấu trúc.
6. Ranh giới vận hành rõ để AI không gây rủi ro.

Trong bài cá nhân này, tôi đánh giá bài toán **VinFast AI phân loại mô tả lỗi xe điện** là phù hợp nhất để đề xuất cho nhóm vì nó đủ cụ thể, có thể đo được, dễ làm prototype prompt và có rủi ro kiểm soát được nếu giữ Human-in-the-loop.

---

## 6. Kết luận cá nhân

AI hỗ trợ tôi tốt nhất ở giai đoạn brainstorm, phản biện và chuẩn hóa format. Tuy nhiên, tôi không thể dùng nguyên các đề xuất của AI vì nhiều ý tưởng còn rộng, số liệu chưa kiểm chứng và đôi khi đề xuất mức tự động hóa quá cao.

Cách dùng AI hiệu quả hơn là:

- Dùng AI để tạo nhiều lựa chọn.
- Dùng AI để phản biện chính các lựa chọn đó.
- Sau đó con người chọn lại, thu hẹp scope, chỉnh metric và đặt ranh giới vận hành.

Với cách này, AI không thay thế quá trình suy nghĩ của tôi mà đóng vai trò như một người cộng tác giúp tôi nhìn bài toán rõ hơn.
