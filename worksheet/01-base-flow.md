# 01 · Base Flow + Chốt 3 Knobs

> **Mục tiêu**: Hiểu luồng chatbot ở mức base và xác định 3 knobs nhóm sẽ tinh chỉnh để tạo ra các cấu hình khác nhau.

---

## Bước 1 — Base flow nhóm hiểu

```text
Khách gửi tin nhắn
    ↓
Phân loại intent
    ↓
┌───────────────┬──────────────┬──────────────┬──────────────┬──────────────┐
│ Visa/Policy   │ Guide        │ Weather      │ Booking      │ Complaint    │
└──────┬────────┴──────┬───────┴──────┬───────┴──────┬───────┴──────┬───────┘
       ↓               ↓              ↓              ↓              ↓
   RAG + web      RAG knowledge   Web search      Handoff sales   Escalate manager
       └───────────────┬──────────────┴──────────────┬──────────────┘
                       ↓
     Context assembly: system prompt + history + knowledge + user message
                       ↓
               Response generation
                       ↓
             Trả lời khách hoặc chuyển người
```

Nhóm thống nhất rằng Booking và Khiếu nại không nên cố xử lý bằng LLM quá sâu. Bot chỉ nên nhận diện nhanh, phản hồi lịch sự, rồi chuyển đúng người.

---

## Bước 2 — 3 knobs nhóm chọn để so sánh

### Knob 1 — Model tier

```text
Nhóm muốn so sánh rõ 3 mức:
- Rẻ nhất để tối ưu cost: Gemini 2.5 Flash-Lite
- Mạnh nhất để tối ưu chất lượng: Claude Sonnet 4.6
- Pha trộn theo intent để cân bằng: Gemini 2.5 Flash + DeepSeek V4 Pro cho Visa
```

### Knob 2 — Web search

```text
Nhóm không muốn bật web đại trà cho mọi trường hợp vì chi phí web search cộng dồn theo từng turn.
Hướng chính là chỉ bật cho Visa và Weather; riêng config premium sẽ thử web broad để xem chênh lệch cost và độ tin cậy.
```

### Knob 3 — History management

```text
Nhóm muốn test 3 mức nhớ ngữ cảnh:
- Last 3 để giữ chi phí thấp
- Last 5 để cân bằng
- Full history để ưu tiên trải nghiệm hội thoại dài
```

---

## Bước 3 — Combo nhóm dự định thử

**Combo 1 (định hướng cheap)**:

```text
Model: Gemini 2.5 Flash-Lite
Web: ON selective cho Visa, Weather
History: Last 3
Tên dự kiến: Budget Bot
```

**Combo 2 (định hướng premium)**:

```text
Model: Claude Sonnet 4.6
Web: ON broad
History: Full
Tên dự kiến: Premium Concierge
```

**Combo 3 (định hướng balanced / smart mix)**:

```text
Model: Gemini 2.5 Flash cho Guide/Weather, DeepSeek V4 Pro cho Visa
Web: ON selective cho Visa, Weather
History: Last 5
Tên dự kiến: Smart Mix
```

**Combo 4 (optional)**:

```text
Không dùng. Nhóm tập trung làm chắc 3 cấu hình chính để bảng so sánh đủ rõ trade-off.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Đã vẽ flow base đủ 4 bước: Intent → Route → Context → Response
- [x] Hiểu rõ Booking và Khiếu nại chủ yếu là handoff
- [x] Đã phác thảo 3 combo có khác biệt rõ ràng
- [x] Nhóm thống nhất hướng đi của từng combo

Xong → mở `02-config-design.md`.
