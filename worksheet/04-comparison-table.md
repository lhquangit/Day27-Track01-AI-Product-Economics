# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp toàn bộ số liệu của 3 cấu hình vào một bảng duy nhất để dễ present và dễ chốt recommendation.

---

## Bảng chính

| | Config 1 | Config 2 | Config 3 | Config 4 |
|---|---|---|---|---|
| **Tên** | Budget Bot | Premium Concierge | Smart Mix | Không dùng |
| **① Model** | Gemini 2.5 Flash-Lite | Claude Sonnet 4.6 | Gemini 2.5 Flash cho Guide/Weather + DeepSeek V4 Pro cho Visa | N/A |
| **② Web search** | ON selective cho Visa, Weather | ON broad | ON selective cho Visa, Weather | N/A |
| **③ History** | Last 3 | Full history | Last 5 | N/A |
| **Intent classifier** | Keyword | LLM (Gemini 2.5 Flash-Lite) | Keyword | N/A |
| **Cost / conv (Scenario A — 4 turns)** | $0.0123 | $0.0673 | $0.0199 | N/A |
| **Cost / conv (Scenario B — 7 turns)** | $0.0153 | $0.0807 | $0.0244 | N/A |
| **Monthly A** (300 conv/day × 30) | $110.80 | $605.39 | $178.70 | N/A |
| **Monthly B** (1,200 conv/day × 30) | $552.11 | $2,904.46 | $878.73 | N/A |
| **vs human $4,500/mo (A)** | rẻ 40.6× | rẻ 7.4× | rẻ 25.2× | N/A |
| **vs human $18,000/mo (B)** | rẻ 32.6× | rẻ 6.2× | rẻ 20.5× | N/A |
| **Savings % (A)** | 97.54% | 86.55% | 96.03% | N/A |
| **Savings % (B)** | 96.93% | 83.86% | 95.12% | N/A |
| **Quality estimate** | Medium-Low | High | Medium-High | N/A |
| **Speed estimate** | High | Low | Medium | N/A |
| **Điểm yếu chính** | Dễ quên context và trả lời chưa đủ sâu | Chi phí cao nhất, dễ bị phình khi chat dài | Routing phức tạp hơn, cần kiểm soát logic intent | N/A |
| **Best for** | Low season, FAQ, ngân sách chặt | Khách VIP, thương hiệu premium, cần độ tự nhiên cao | Triển khai quanh năm, cân bằng cost và quality | N/A |

---

## Quan sát nhanh từ bảng

### Câu 1 — Config rẻ nhất là gì? Đắt nhất là gì?

```text
Rẻ nhất: Budget Bot — monthly B = $552.11
Đắt nhất: Premium Concierge — monthly B = $2,904.46
Chênh lệch: khoảng 5.26 lần
```

### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

```text
Knob ảnh hưởng mạnh nhất vẫn là model tier. Chỉ riêng việc đi từ model cheap sang model strong/premium đã kéo cost mỗi conversation tăng rất rõ, đặc biệt khi conversation dài.
Web search là nút tăng cost đứng thứ hai vì nó cộng thêm $0.008 cho gần như mỗi turn có tìm kiếm; nếu bật broad thì phần cộng dồn này rất lớn.
History ảnh hưởng thấy rõ nhất ở Scenario B, vì turn 5-7 làm full history phình input token nhanh hơn Last 3 hoặc Last 5.
```

### Câu 3 — Tại sao Scenario B không đắt ×7 lần Scenario A?

```text
Scenario B có volume gấp 4 và số turns dài hơn, nhưng tỷ lệ Booking + Complaint cũng tăng lên 45%, tức gần một nửa traffic chỉ handoff chứ không tiếp tục đốt LLM cost.
Vì vậy monthly cost thực tế chỉ tăng quanh mức 4.8-5.0 lần giữa A và B thay vì tăng thẳng theo volume × turns.
```

### Câu 4 — Có config nào AI đắt hơn human không?

```text
Không. Cả 3 cấu hình đều rẻ hơn human baseline rất xa trong cả hai scenarios.
Ngay cả Premium Concierge, vốn là cấu hình đắt nhất, vẫn rẻ hơn human khoảng 6.2× ở mùa cao điểm nên chưa có trường hợp AI bị âm unit economics trong bài này.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Bảng đã điền đủ số liệu cho 3 configs
- [x] Đã trả lời đủ 4 câu quan sát chính
- [x] Các con số khớp với file cost calculation

Xong → mở `05-recommendation.md`.
