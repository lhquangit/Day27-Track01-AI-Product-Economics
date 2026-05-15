# 05 · Recommendation + Justification — Kết luận & Chuẩn bị Present

> **Mục tiêu**: Chọn cấu hình nên deploy, giải thích bằng số liệu, và chia phần trình bày rõ ràng để nhóm có thể present ngay.

---

## 4 câu hỏi nhóm phải trả lời

### Câu 1 — Recommend config nào?

```text
Nhóm recommend Smart Mix là cấu hình deploy mặc định cho bài toán chatbot du lịch này.
Lý do là Smart Mix giữ được monthly cost rất thấp so với human baseline, nhưng vẫn dành model mạnh hơn cho intent Visa là nơi rủi ro trả lời sai cao nhất.
Budget Bot phù hợp làm phương án fallback khi doanh nghiệp cần cắt chi phí tối đa, còn Premium Concierge chỉ nên dùng cho phân khúc VIP hoặc giai đoạn cần test trải nghiệm cao cấp.
```

### Câu 2 — So với human baseline $0.50/conv → tiết kiệm bao nhiêu? Có đắt hơn human ở chỗ nào không?

```text
Smart Mix tiết kiệm 96.03% ở Scenario A và 95.12% ở Scenario B, tương đương tiết kiệm khoảng $4,321.30/tháng ở mùa thấp điểm và $17,121.27/tháng ở mùa cao điểm.
Không có cấu hình nào trong bài đắt hơn human baseline, kể cả Premium Concierge.
Điểm cần lưu ý không phải là “AI có đắt hơn human không”, mà là “mình có đang trả thêm tiền cho chất lượng cao hơn có đáng hay không”.
```

### Câu 3 — Khi nào nên upgrade / downgrade config?

```text
Nên upgrade từ Smart Mix lên Premium Concierge khi complaint về chất lượng vượt 5%, tỷ lệ câu Visa phức tạp tăng rõ, hoặc khi doanh nghiệp bắt đầu phục vụ nhóm khách chi tiêu cao cần trải nghiệm tư vấn tự nhiên hơn.
Nên downgrade về Budget Bot khi đang low season, traffic chủ yếu là FAQ đơn giản, monthly conversation thấp và team cần tối ưu ngân sách hơn là tối ưu trải nghiệm.
Nếu conversion không cải thiện dù đã dùng Premium, doanh nghiệp nên quay lại Smart Mix vì chênh lệch cost là có thật nhưng lợi ích kinh doanh chưa chắc tương xứng.
```

### Câu 4 — Rủi ro lớn nhất của config được chọn là gì?

```text
Rủi ro lớn nhất của Smart Mix là logic routing sai intent, khiến bot vô tình dùng model chưa đủ mạnh cho câu Visa hoặc bật web search không đúng lúc.
Mitigation là đặt confidence threshold cho intent classification, câu nào mơ hồ thì chuyển human hoặc ép về nhánh an toàn hơn.
Ngoài ra cần monitor định kỳ cost theo intent và tỉ lệ escalation để chắc rằng cấu hình mix vẫn đang mang lại lợi thế kinh tế như thiết kế ban đầu.
```

---

## Final answer — Recommendation in 1 paragraph

```text
Nhóm recommend Smart Mix là cấu hình phù hợp nhất để triển khai chatbot du lịch cho khách quốc tế vì nó tạo cân bằng tốt nhất giữa chi phí, chất lượng và tốc độ. Ở Scenario A, Smart Mix chỉ tốn khoảng $178.70/tháng; ở Scenario B là $878.73/tháng, vẫn rẻ hơn human baseline lần lượt 25.2× và 20.5×. So với Budget Bot, cấu hình này tốn thêm chi phí nhưng giảm rủi ro trả lời sai ở intent Visa và giữ ngữ cảnh tốt hơn nhờ Last 5. So với Premium Concierge, Smart Mix giữ được phần lớn lợi ích chất lượng mà không phải gánh mức chi phí gần $2,900/tháng ở mùa cao điểm. Nhóm xem đây là cấu hình nên chạy mặc định quanh năm, còn Budget Bot là phương án tiết kiệm và Premium Concierge là phương án nâng cấp cho phân khúc cần trải nghiệm cao cấp hơn.
```

---

## Chia role task thành 3 phần

### Phần 1 — Nguyễn Quốc Nam

**Phụ trách**: mở bài, base flow, 3 knobs và chốt recommendation cuối.

**Nói gì**:

```text
Nhóm em xuất phát từ base flow gồm intent classification, routing, context assembly và response generation.
Từ đó nhóm chọn 3 knobs chính để so sánh là model tier, web search và history management.
Sau khi tính cost cho 3 cấu hình, nhóm recommend Smart Mix vì đây là điểm cân bằng tốt nhất giữa cost thấp và chất lượng đủ an toàn để deploy.
```

### Phần 2 — Đỗ Trọng Minh

**Phụ trách**: trình bày bảng cost comparison và key insight từ số liệu.

**Nói gì**:

```text
Trong 3 cấu hình, Budget Bot rẻ nhất với monthly cost mùa cao điểm là $552.11, còn Premium Concierge đắt nhất với $2,904.46.
Tuy vậy cả 3 cấu hình đều rẻ hơn human baseline rất xa; khác biệt chính nằm ở việc mình có sẵn sàng trả thêm để đổi lấy chất lượng hay không.
Một insight quan trọng là Scenario B không tăng chi phí gấp 7 lần vì tỷ lệ Booking và Complaint tăng lên 45%, nghĩa là nhiều conversation được handoff sớm.
```

### Phần 3 — __________

**Phụ trách**: nêu rủi ro, ngưỡng upgrade/downgrade và xử lý Q&A.

**Nói gì**:

```text
Rủi ro lớn nhất của Smart Mix là phân loại sai intent và dùng sai model cho câu hỏi nhạy cảm như Visa.
Nhóm đề xuất mitigation bằng confidence threshold, fallback sang human cho câu mơ hồ và theo dõi cost theo intent hằng tháng.
Nếu chất lượng chưa đủ hoặc nhóm khách VIP tăng lên, doanh nghiệp có thể nâng sang Premium Concierge; ngược lại low season có thể giảm về Budget Bot để tối ưu chi phí.
```

---

## Hardest question prep

**Nhóm dự đoán câu hỏi khó nhất sẽ bị hỏi là gì?**

```text
Tại sao không chọn Budget Bot luôn, khi nó rẻ nhất và vẫn rẻ hơn human rất nhiều?
```

**Câu trả lời sẵn**:

```text
Budget Bot đúng là rẻ nhất, nhưng nó đánh đổi khá mạnh ở chất lượng và khả năng giữ ngữ cảnh.
Với chatbot du lịch, phần Visa là nơi rủi ro sai thông tin cao nhất; Smart Mix chấp nhận tốn thêm một ít chi phí để giảm rủi ro này nhưng vẫn giữ unit economics rất khỏe.
```

---

## Q&A — 3 câu instructor thường hỏi

```text
1. Knob ảnh hưởng cost nhiều nhất là model tier; web search đứng thứ hai vì cộng thêm chi phí gần như theo từng turn.
2. Nếu provider tăng giá API gấp 2, Smart Mix vẫn sống được vì biên tiết kiệm hiện tại còn rất lớn so với human baseline; khi đó nhóm sẽ cắt web broad và siết routing trước khi đổi toàn bộ config.
3. Nếu nhóm khác chọn Premium, khác biệt chính là nhóm em ưu tiên cost-effectiveness quanh năm thay vì tối đa hóa trải nghiệm cho mọi traffic.
```

---

## Bảng kiểm cuối cùng

- [x] Đã trả lời đủ 4 câu PM
- [x] Đã có final paragraph 5-7 câu
- [x] Đã chia role task thành 3 phần
- [x] Đã chuẩn bị trước câu hỏi khó và câu trả lời

Xong → sẵn sàng present.
