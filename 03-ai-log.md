# 03-ai-log.md

# AI Log — Vương Nguyệt Bình

## 1. AI đã giúp gì?

Trong quá trình làm Lab 02, tôi sử dụng AI như một thought-partner để brainstorm các bài toán vận hành trong hệ sinh thái Vingroup. AI hỗ trợ tôi so sánh các bài toán thuộc Xanh SM, VinFast, Vinhomes và Vinmec, từ đó chọn bài toán phù hợp nhất với yêu cầu lab là “Trợ lý điều phối Xanh SM xử lý sự cố xe điện pin yếu/hết pin thực địa”.

AI cũng giúp tôi viết nháp Problem Statement 6-field, xác định bottleneck, đề xuất metric đo thành công và thiết kế operational boundary cho hệ thống.

## 2. AI đã sai hoặc chưa tốt ở đâu?

Một số gợi ý ban đầu của AI có xu hướng mở rộng bài toán quá mức, ví dụ đề xuất xây dựng agent tự động điều phối xe hoàn toàn. Điều này không phù hợp vì bài toán có rủi ro vận hành cao: nếu AI đề xuất sai trạm sạc hoặc tự gửi hướng dẫn khi chưa được duyệt, tài xế có thể bị hết pin giữa đường.

AI cũng có lúc đề xuất dùng LLM để quyết định ngưỡng pin an toàn, trong khi điều kiện “pin dưới 5% thì không đi trạm xa hơn 5km” nên được xử lý bằng rule cứng.

## 3. Tôi đã sửa prompt như thế nào?

Tôi bổ sung ranh giới rõ ràng vào system prompt:
- Mọi output phải bắt đầu bằng `[DRAFT_ONLY]`.
- AI không được tự gửi tin nhắn.
- Nếu pin dưới 5%, AI không được đề xuất trạm sạc xa hơn 5km.
- Trong tình huống pin nguy cấp, AI phải trả về action `dispatch_mobile_charger`.

Tôi cũng thêm adversarial test cases để kiểm tra xem mô hình có bị dụ bỏ qua boundary hay không.

## 4. Bài học rút ra

Tôi nhận ra AI hữu ích nhất khi hỗ trợ phân tích, viết nháp và kiểm thử ý tưởng. Tuy nhiên, trong bài toán vận hành thực tế, đặc biệt liên quan đến an toàn xe điện, cần kết hợp LLM với rule-based safety, human-in-the-loop và fallback thủ công. Không nên dùng AI tự trị hoàn toàn khi rủi ro sai sót có thể ảnh hưởng đến vận hành thực địa.