# 02 · Configuration Design — Đặt tên + Chốt knobs cho 3 Configs

> **Mục tiêu**: Biến các combo phác thảo thành 3 cấu hình cụ thể, mỗi cấu hình có tên, 3 knobs rõ ràng và lý do chọn.

---

## Config 1

**Tên config**:

```text
Budget Bot
```

### 3 Knobs

**① Model tier**:

```text
Response model: Gemini 2.5 Flash-Lite → giá $0.10 / $0.40 per 1M tokens
Classifier model: Keyword / regex → giá $0
```

**② Web search**:

```text
ON selective — bật cho intent Visa và Weather
```

**③ History management**:

```text
Last 3
```

### Lý do nhóm chọn config này

```text
Đây là cấu hình rẻ nhất và phù hợp nếu website chủ yếu xử lý câu hỏi FAQ, lịch trình cơ bản và nhu cầu sàng lọc khách ban đầu.
Việc chỉ bật web cho Visa và Weather giúp giữ thông tin cập nhật ở hai intent nhạy cảm mà vẫn tránh đốt tiền cho toàn bộ conversation.
History Last 3 đủ cho các đoạn chat ngắn trong low season, nơi khách thường hỏi nhanh rồi rời đi.
```

### Rủi ro lớn nhất của config này

```text
Bot có thể quên ngữ cảnh ở các conversation dài hơn 4 lượt và chất lượng trả lời phần Guide sẽ không đủ tốt với khách hỏi nhiều ràng buộc cùng lúc.
```

---

## Config 2

**Tên config**:

```text
Premium Concierge
```

### 3 Knobs

**① Model tier**:

```text
Response model: Claude Sonnet 4.6 → giá $3.00 / $15.00 per 1M tokens
Classifier model: Gemini 2.5 Flash-Lite → giá $0.10 / $0.40 per 1M tokens
```

**② Web search**:

```text
ON broad
```

**③ History management**:

```text
Full history
```

### Lý do nhóm chọn config này

```text
Đây là cấu hình ưu tiên trải nghiệm cao nhất, phù hợp nếu thương hiệu muốn chatbot trả lời tự nhiên, nhớ bối cảnh tốt và hạn chế tối đa câu trả lời mơ hồ.
Web broad giúp bot luôn có dữ liệu mới cho cả Guide, Visa và Weather, đặc biệt hữu ích nếu khách hỏi về dịp lễ, thời tiết, giờ mở cửa hoặc chính sách vừa thay đổi.
Full history phù hợp với khách có nhu cầu tư vấn hành trình dài, nhiều ràng buộc và kỳ vọng chatbot “nhớ” toàn bộ cuộc hội thoại.
```

### Rủi ro lớn nhất của config này

```text
Chi phí tăng mạnh khi volume cao hoặc conversation kéo dài, nên rất dễ làm biên lợi nhuận mỏng nếu chưa chứng minh được tác động lên conversion.
```

---

## Config 3

**Tên config**:

```text
Smart Mix
```

### 3 Knobs

**① Model tier**:

```text
Response model:
- Guide/Weather: Gemini 2.5 Flash → giá $0.30 / $2.50 per 1M tokens
- Visa/Policy: DeepSeek V4 Pro → giá $1.74 / $3.48 per 1M tokens
Classifier model: Keyword / regex → giá $0
```

**② Web search**:

```text
ON selective — bật cho intent Visa và Weather
```

**③ History management**:

```text
Last 5
```

### Lý do nhóm chọn config này

```text
Smart Mix cố tình dùng đúng mức “thông minh” cho đúng loại câu hỏi: Visa cần độ chính xác cao hơn nên dùng model mạnh hơn, còn Guide và Weather dùng model tầm trung để giữ chi phí thấp.
Web selective giúp nhóm bảo vệ chất lượng ở các intent có yếu tố real-time mà không phải trả phí tìm kiếm cho toàn bộ traffic.
Last 5 tạo cân bằng tốt giữa trải nghiệm và chi phí, phù hợp với phần lớn conversation thật có 4-7 lượt.
```

### Rủi ro lớn nhất của config này

```text
Logic routing phức tạp hơn, nên nếu phân loại sai intent thì bot có thể dùng sai model và làm giảm cả chất lượng lẫn hiệu quả chi phí.
```

---

## Config 4 (optional)

**Tên config**:

```text
Không dùng
```

### 3 Knobs

```text
Nhóm chủ động bỏ Config 4 để tập trung làm chắc 3 cấu hình chính và tính cost đầy đủ cho cả 2 scenarios.
```

### Lý do

```text
Ba cấu hình hiện tại đã thể hiện đủ 3 chiến lược: tối ưu chi phí, tối ưu chất lượng và cân bằng theo intent.
```

---

## Bảng kiểm trước khi tính cost

- [x] Đã có 3 configs đặt tên rõ ràng
- [x] Mỗi config đã chốt đủ 3 knobs
- [x] Mỗi config có lý do và rủi ro cụ thể
- [x] Ba config đủ khác biệt để so sánh trade-off

Xong → mở `03-cost-calculation.md`.
