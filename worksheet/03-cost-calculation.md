# 03 · Cost Calculation — Tính chi phí từng Config × 2 Scenarios

> **Mục tiêu**: Tính cost theo từng cấu hình cho cả low season và high season, sau đó so sánh với baseline human $0.50/conversation.

---

## Giả định dùng để tính

```text
System prompt: 500 tokens
User message: 80 tokens
Assistant response: 180 tokens
1 prior turn history: 260 tokens
RAG top-5 chunks: 1,250 tokens
Web search results: 800 tokens
Web search API: $0.008 / query
```

**Scenario A — mùa thấp điểm**

```text
300 conversations / ngày
4 turns / conversation
Intent mix: Guide 50%, Visa 25%, Weather 10%, Booking 10%, Complaint 5%
```

**Scenario B — mùa cao điểm**

```text
1,200 conversations / ngày
7 turns / conversation
Intent mix: Guide 30%, Visa 15%, Weather 10%, Booking 35%, Complaint 10%
```

**Lưu ý tính toán**

```text
- Booking và Complaint được tính là handoff, gần như $0 LLM cost.
- Config dùng keyword classifier xem như không có cost classifier.
- Premium Concierge dùng Gemini 2.5 Flash-Lite làm LLM classifier, cost rất nhỏ nhưng vẫn cộng vào.
```

---

## Config 1 — Budget Bot

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---:|---:|
| Cost / conversation (avg) | $0.0123 | $0.0153 |
| Monthly cost | $110.80 | $552.11 |
| Human baseline | $4,500.00 | $18,000.00 |
| **Rẻ hơn human ___×** | 40.6× | 32.6× |
| **Savings %** | 97.54% | 96.93% |

**Sanity check**:

```text
Con số hợp lý. Cost thấp vì model rất rẻ, web chỉ bật cho Visa và Weather, còn Booking/Khiếu nại gần như không dùng LLM.
Scenario B chỉ tăng khoảng 5 lần thay vì 7 lần vì tỷ trọng handoff tăng mạnh lên 45%.
```

---

## Config 2 — Premium Concierge

| Item | Scenario A | Scenario B |
|---|---:|---:|
| Cost / conversation (avg) | $0.0673 | $0.0807 |
| Monthly cost | $605.39 | $2,904.46 |
| **Rẻ hơn human ___×** | 7.4× | 6.2× |
| **Savings %** | 86.55% | 83.86% |

**Sanity check**:

```text
Con số vẫn rẻ hơn human khá nhiều, nhưng đây là config có chi phí cao nhất vì cùng lúc dùng Sonnet 4.6, web broad và full history.
Mức cost này chỉ đáng deploy nếu doanh nghiệp thật sự cần chất lượng cao và có lợi ích kinh doanh rõ ràng từ trải nghiệm tốt hơn.
```

---

## Config 3 — Smart Mix

| Item | Scenario A | Scenario B |
|---|---:|---:|
| Cost / conversation (avg) | $0.0199 | $0.0244 |
| Monthly cost | $178.70 | $878.73 |
| **Rẻ hơn human ___×** | 25.2× | 20.5× |
| **Savings %** | 96.03% | 95.12% |

**Sanity check**:

```text
Con số nằm giữa Budget và Premium đúng như kỳ vọng.
Chi phí tăng chủ yếu ở intent Visa vì dùng DeepSeek V4 Pro, nhưng tổng monthly vẫn rất an toàn do chỉ áp dụng model mạnh cho phần traffic thật sự cần độ chính xác cao.
```

---

## Config 4 (optional)

| Item | Scenario A | Scenario B |
|---|---:|---:|
| Cost / conversation (avg) | N/A | N/A |
| Monthly cost | N/A | N/A |
| **Rẻ hơn human ___×** | N/A | N/A |
| **Savings %** | N/A | N/A |

---

## Quality + Speed estimate

| Config | Quality | Speed | Lý do |
|---|---|---|---|
| Budget Bot | Medium-Low | High | Model rẻ, web chỉ bật chọn lọc nên phản hồi nhanh nhưng dễ hụt chiều sâu ở câu hỏi phức tạp |
| Premium Concierge | High | Low | Model mạnh, web broad, full history nên chất lượng cao nhất nhưng độ trễ lớn hơn |
| Smart Mix | Medium-High | Medium | Dùng model mạnh đúng chỗ và chỉ bật web khi cần nên cân bằng tốt |
| Config 4 | N/A | N/A | Không dùng |

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Đã có cost/conv và monthly cho cả 3 configs
- [x] Đã so sánh với human baseline
- [x] Đã ước lượng quality và speed
- [x] Các con số đều nằm trong vùng hợp lý và nhất quán với giả định

Xong → mở `04-comparison-table.md`.
