# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm cần hình dung khách quốc tế thật sự sẽ hỏi gì, hỏi theo cách nào, và một conversation thực tế sẽ diễn ra ra sao.

---

## Bước 1 — Mỗi người đóng vai 1 tourist

### Tourist #1 (Tên thành viên: Nguyễn Quốc Nam - 2A202600201)

```text
1. Hi, I am visiting Vietnam for 7 days in September. Which cities should I prioritize if my budget is around $1,200?
2. Do I need a visa for Vietnam if I hold an Australian passport?
3. I want a mix of food, culture, and nature. Can you suggest a simple itinerary?
4. Is Da Nang still a good destination in October, or will the weather be too rainy?
5. Can I travel from Hoi An to Hue by train or private car, and which option is better?
6. Is it safe to eat street food if I am traveling with my 10-year-old child?
```

### Tourist #2 (Tên thành viên: Đỗ Trọng Minh - 2A202600464)

```text
1. I will arrive in Ho Chi Minh City at night. Which area is best to stay for first-time visitors?
2. Can you recommend a romantic 5-day honeymoon trip in Vietnam?
3. Are there any public holidays or big events in late January that may affect hotel prices?
4. I only speak English. Will I have problems using transport in Hanoi or Da Nang?
5. Can you help me book a Ha Long Bay cruise for next Friday?
6. What is the average weather like in Sapa in December?
```

### Tourist #3 (Tên thành viên: Lê Hồng Quân- 2A202600097)

```text
1. My flight lands in Hanoi, but I also want to visit Ninh Binh. Is that realistic in 4 days?
2. Do I need cash everywhere, or can I mostly pay by card in Vietnam?
3. Which Vietnamese foods should I try if I cannot eat spicy food?
4. I paid a deposit for a tour last week but still did not receive confirmation. Can you check that for me?
5. Can you suggest a family-friendly beach destination with easy airport access?
6. Do I need any vaccines or special health preparation before coming to Vietnam?
```

---

## Bước 2 — Gom lại và phân loại

| # | Câu hỏi (1 dòng) | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
|---|---|---|---|---|
| 1 | Best 7-day Vietnam itinerary under $1,200 | Điểm đến/Guide | 4 lượt | Bot |
| 2 | Do I need a visa for Vietnam with an Australian passport? | Visa/Policy | 4 lượt | Bot |
| 3 | Is Da Nang good in October or too rainy? | Thời tiết/Sự kiện | 3 lượt | Bot |
| 4 | Can I combine Hoi An and Hue in one trip? | Điểm đến/Guide | 4 lượt | Bot |
| 5 | Is street food safe for a child? | Điểm đến/Guide | 3 lượt | Bot |
| 6 | Best area to stay in Ho Chi Minh City for first-time visitors | Điểm đến/Guide | 3 lượt | Bot |
| 7 | Are there any public holidays in late January? | Thời tiết/Sự kiện | 3 lượt | Bot |
| 8 | Can you help me book a Ha Long Bay cruise next Friday? | Tour/Booking | 1 lượt | Người |
| 9 | I paid a deposit but did not receive confirmation | Khiếu nại | 1 lượt | Người |
| 10 | Suggest a honeymoon trip in Vietnam | Điểm đến/Guide | 5 lượt | Bot |

---

## Bước 3 — Rút insight cho nhóm

**Tổng số câu hỏi nhóm gom được**:

```text
18 câu hỏi
```

**Phân bố intent thực tế của nhóm**:

```text
Guide: 44%
Visa: 22%
Weather: 11%
Booking: 17%
Khiếu nại: 6%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
Guide thường cần 3-5 lượt, Visa cần khoảng 4 lượt, Weather cần 2-3 lượt,
Booking và Khiếu nại thường chỉ 1 lượt rồi chuyển người.
```

**Đối chiếu với đề bài**:

```text
Phân bố của nhóm khá gần Scenario A ở phần Guide và Visa, nhưng tỷ lệ Booking cao hơn một chút.
Scenario B thực tế hơn ở giai đoạn cao điểm vì khách bắt đầu hỏi đặt tour nhiều hơn và bot chỉ nên làm bước sàng lọc ban đầu.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Tourist hiếm khi hỏi một intent hoàn toàn tách biệt; họ thường gộp budget, lịch trình và thời tiết trong cùng một conversation.
Những câu hỏi tưởng như đơn giản về visa hoặc thời tiết lại là nơi bot dễ trả lời sai nhất nếu không có thông tin cập nhật.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Mỗi người trong nhóm đã có 5-6 câu hỏi tourist
- [x] Đã gom và phân loại ít nhất 10 câu hỏi đại diện
- [x] Đã có phân bố intent % của nhóm
- [x] Có insight cụ thể về hành vi dùng chatbot của tourist

Xong → mở `01-base-flow.md`.
