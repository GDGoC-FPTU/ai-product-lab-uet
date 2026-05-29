# Phần 1: Quét cơ hội vận hành (Phase 1 — SCAN)

- Bài toán 1 (Vinhomes - Tốn thời gian): Ban quản lý mất nhiều công sức để đọc, phân loại và trả lời hàng trăm khiếu nại của cư dân trên ứng dụng mỗi ngày. 
- Bài toán 2 (Xanh SM - Stakeholder Pain): Tài xế và khách hàng gặp khó khăn khi điểm đón trên GPS bị lệch tại các khu vực như sảnh trung tâm thương mại hoặc ngõ nhỏ.  
- Bài toán 3 (VinFast - Lặp lại): Trợ lý ảo tra cứu cẩm nang sử dụng xe VinFast - khách hàng gặp thắc mắc về tính năng trên xe  
- Bài toán 4 (Vinmec - Tốn thời gian): Bác sĩ phải dành 15-20 phút sau mỗi ca khám để tóm tắt bệnh án thô thành hồ sơ xuất viện chuẩn hóa.  
Bài toán 5 (Vinpearl - AI-upgrade): Hệ thống tư vấn đặt phòng hiện tại chưa thể tự động gợi ý lịch trình vui chơi cá nhân hóa theo sở thích riêng của từng gia đình
---

# Phần 2: Thẻ đánh giá nhanh bài toán (Phase 2 — QUICK-ASSESS)

QUICK PROBLEM CARD #01: Xử lý khiếu nại Vinhomes
- Công ty: Vinhomes.  
- Đối tượng chịu ảnh hưởng (Actor): Nhân viên Ban quản lý tòa nhà.  
- Quy trình thủ công hiện tại:Tiếp nhận phản ánh từ cư dân qua App.  
- Nhân viên đọc và phân loại thủ công vào các nhóm (Kỹ thuật/Vệ sinh/An ninh).  
- Soạn nội dung phản hồi cá nhân hóa cho cư dân.  Gửi thông báo và theo dõi tiến độ xử lý.  
- Bước tốn thời gian nhất: Bước đọc hiểu phân loại và soạn phản hồi (15 phút/lượt). 
- AI hỗ trợ: LLM tự động phân loại và viết nháp phản hồi.  
- Chỉ số thành công: Giảm thời gian xử lý từ 15 phút xuống dưới 2 phút mỗi ticket.  
- Kiến trúc: LLM.  

QUICK PROBLEM CARD #02: Trợ lý ảo tra cứu cẩm nang sử dụng xe VinFast
- Công ty: VinFast.
- Đối tượng chịu ảnh hưởng (Actor): Khách hàng tài xế lái xe điện VinFast hoặc nhân viên tổng đài CSKH.
- Quy trình thủ công hiện tại: Khách hàng gặp thắc mắc về tính năng trên xe khi đang di chuyển 
(ví dụ: Cách bật chế độ cắm trại, cách xử lý khi màn hình bị treo, cách tối ưu hóa pin).
    - Khách hàng phải tự lật cuốn sách hướng dẫn sử dụng bằng giấy dày vài trăm trang lưu trong hộc xe hoặc mở file PDF trên điện thoại để tìm kiếm từ khóa.
    - Nếu không tìm ra, khách hàng phải bấm máy gọi lên tổng đài CSKH VinFast và mô tả tình trạng để đợi nhân viên kỹ thuật tra cứu hộ.
- Bước tốn thời gian/lỗi nhất: Bước lật sách tra cứu thủ công hoặc chờ đợi tổng đài viên tìm câu trả lời trong tài liệu kỹ thuật (10 phút/lượt).
- AI hỗ trợ: LLM đọc hiểu toàn bộ bộ tài liệu hướng dẫn sử dụng (User Manual) của xe, đóng vai trò trợ lý ảo trả lời ngay lập tức câu hỏi của tài xế qua giọng nói hoặc văn bản.
- Chỉ số thành công: Giảm thời gian tra cứu từ 10 phút xuống dưới 5 giây, giải quyết được 70% các câu hỏi kỹ thuật phổ biến mà không cần làm phiền tổng đài viên.
- Kiến trúc: LLM.

QUICK PROBLEM CARD #03: Tóm tắt bệnh án Vinmec
- Công ty: Vinmec.
- Đối tượng chịu ảnh hưởng (Actor): Bác sĩ và điều dưỡng.  
- Quy trình thủ công hiện tại:Tập hợp kết quả xét nghiệm và ghi chú lâm sàng thô.  
- Bác sĩ tổng hợp thông tin chính (triệu chứng, phác đồ, thuốc).  
- Gõ tay vào biểu mẫu hồ sơ xuất viện trên hệ thống.  
- Bước tốn thời gian nhất: Bước gõ tay và hệ thống hóa thuật ngữ y khoa (20 phút/lượt).  
- AI hỗ trợ: LLM trích xuất thực thể y tế và điền tự động vào form.  
- Chỉ số thành công: Giảm thời gian lập hồ sơ từ 20 phút xuống dưới 3 phút mỗi bệnh nhân.  
- Kiến trúc: LLM.  