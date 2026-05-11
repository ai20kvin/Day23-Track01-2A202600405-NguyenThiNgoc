# Day 23 — Bài 1: Ghi chú thách thức + Case Evidence Matrix

**Học viên:** Nguyễn Thị Ngọc — **Mã:** 2A202600405  
**Nhóm:** Track 1
**Thành viên nhóm:** Nguyễn Thị Ngọc (2A202600405), Nguyễn Hữu Quang (2A202600167), Trần Vọng Triển (2A202600320), Nguyễn Thị Ngọc Thư (2A202600210)  
---

## 1. Ghi chú thách thức áp dụng AI (cá nhân, Bài 1A)

| Trường | Trả lời |
|---|---|
| **Tình huống** | Team thử dùng AI (vibe coding, Copilot/ChatGPT) để tăng tốc dev nhưng thiếu governance và “source of truth” cho PRD kiến trúc. |
| **Người dùng chính** | Developer, PO/BA trong dự án môn học / product nhỏ. |
| **Dấu hiệu bị kẹt** | Token tốn nhiều nhưng PR merge chậm; conflict code style; backlog phình do AI gợi ý refactor/idea ngoài scope; thiếu approval gate trước khi code. |
| **Giả thuyết ban đầu** | AI được gắn *bên ngoài* quy trình (không có rubric release, không đo productivity thật), nên adoption chỉ là “dùng tool” chứ chưa đổi cách làm việc. |

**Pattern nhóm gắn với lab:** “Metrics / governance không gắn quyết định” — tương tự case TrustLayerAI trong dashboard nhóm: có công cụ và số liệu nhưng thiếu gate và owner thì vẫn kẹt adoption.

---

## 2. Case Evidence Matrix (1 case — Morgan Stanley)

Mục tiêu: một case cụ thể, đọc chỉ số theo **tầng** (metric layer) và nói rõ chỉ số **chứng minh / không chứng minh** điều gì.

| Trường | Nội dung |
|---|---|
| **Case** | Morgan Stanley — *AI @ Morgan Stanley* (Assistant + Debrief), Wealth Management |
| **Metric shown** | Adoption ~**98%** FA dùng hàng ngày; retrieval efficiency **20% → 80%**; tiết kiệm thời gian họp/admin (ví dụ ~30 phút/cuộc họp trong tài liệu case); phía kinh doanh có narrative gắn net new assets (cần đọc kèm ngữ cảnh báo chí). |
| **Metric layer** | Activation / Engagement (dùng thường xuyên) → Productivity (time saved) → phía Value/Outcome (tài sản mới — **cần** tách attribution). |
| **What this proves** | Công cụ được **dùng thật** (không shelf-ware); truy xuất tri thức nội bộ nhanh hơn đo được; có tín hiệu productivity rõ. |
| **What this does NOT prove** | Chất lượng tư vấn cuối cùng cho khách; hiệu suất danh mục; mức **over-rely** vào AI (bỏ bước kiểm chứng). |
| **Missing metric** | Hallucination / factual error rate trên câu trả lời RAG; **client satisfaction** sau khi FA dùng AI; tỷ lệ **human verify** trước khi gửi khách. |
| **Biggest risk** | Over-reliance: FA tin output mà không verify — rủi ro tuân thủ / uy tín. |
| **Lesson for our dashboard** | Adoption % và time saved **chưa đủ**; dashboard nhóm phải có **Trust + Quality + outcome** (ví dụ validation rate, post-release quality, alignment dev–prod) để tránh lặp lỗi “đo dùng nhiều nhưng không đo đúng việc”. |

**Nguồn tham khảo nhanh:** OpenAI case study (Morgan Stanley); báo chí chuyên ngành về retrieval efficiency (đọc kỹ disclaimer attribution cho số liệu kinh doanh).
