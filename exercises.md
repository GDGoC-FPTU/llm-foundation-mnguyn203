# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature ở mức thấp (0.0 và 0.5), phản hồi rất nhất quán, cấu trúc rõ ràng và tập trung vào các sự thật phổ biến (như hình dáng chữ S hay xuất khẩu cà phê). Khi tăng lên 1.0, câu trả lời trở nên bay bổng và đa dạng hơn, nhưng ở mức 1.5, phản hồi có xu hướng mất mạch lạc, lặp ý hoặc sinh ra thông tin không chính xác (hallucination).

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature từ 0.0 đến 0.2. Đối với chatbot hỗ trợ khách hàng, tính chính xác, tính nhất quán và độ tin cậy của thông tin là quan trọng nhất; việc giảm temperature xuống tối đa giúp hạn chế sự sáng tạo sai lệch của mô hình.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Dựa trên bảng giá PRICING_1M_TOKENS:
> - GPT-4o: $5.00/1M input tokens, $20.00/1M output tokens.
> - GPT-4o-mini: $0.150/1M input tokens, $0.600/1M output tokens.
> - Cả giá đầu vào và đầu ra của GPT-4o đều đắt gấp exactly 33.33 lần so với GPT-4o-mini ($5.00 / $0.150 = 33.333... và $20.00 / $0.600 = 33.333...). Do đó, tổng chi phí sử dụng GPT-4o sẽ đắt hơn GPT-4o-mini đúng **33.33 lần** cho workload này.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> - **GPT-4o xứng đáng**: Khi cần giải quyết các bài toán logic phức tạp, lập trình code phức tạp, hoặc phân tích hợp đồng pháp lý yêu cầu sự chính xác cao về mặt ngữ nghĩa và lập luận.
> - **GPT-4o-mini tốt hơn**: Khi cần phân loại nhanh ý kiến khách hàng (sentiment analysis), phân loại ý định (intent routing) hoặc trích xuất thực thể (entity extraction) từ văn bản ngắn với quy mô lớn.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng chat tương tác trực tiếp (conversational AI, chatbot hỗ trợ) nơi người dùng cần phản hồi ngay lập tức để giảm bớt sự khó chịu khi chờ đợi (giảm thiểu Time to First Token - TTFT). Ngược lại, non-streaming phù hợp hơn cho các tác vụ chạy nền (background processing), phân tích văn bản tự động số lượng lớn, trích xuất dữ liệu có cấu trúc bằng JSON Mode hoặc khi cần gọi function calling ngầm trước khi đưa ra kết quả cuối cùng.


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
