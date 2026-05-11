# Day 23 — Bài 2: Bảng so sánh case thành công / thất bại

**Nhóm:** Track 1 (Nguyễn Thị Ngọc, Nguyễn Hữu Quang, Trần Vọng Triển, Nguyễn Thị Ngọc Thư)

Mục tiêu: đọc case thật để biết chỉ số nào chứng minh được giá trị (value), chỉ số nào chỉ tạo cảm giác tốt — rồi rút bài học cho dashboard TrustLayerAI.

---

## Chọn Case

| Nhóm case | Gợi ý |
|---|---|
| Thành công / tín hiệu tốt | Morgan Stanley, DWP/GDS, Stripe, Nansen |
| Thất bại / cảnh báo | Klarna, IBM Watson / MD Anderson, KPMG dashboard, JPMorgan dashboard |

---

## Bảng Điền

| Trường | Case thành công | Case thất bại/cảnh báo |
|---|---|---|
| **Case** | **Morgan Stanley: AI @ Morgan Stanley Assistant & Debrief** | **JPMorgan Chase: Hệ thống Giám sát Nhân viên WADU** |
| **AI được dùng trong quy trình nào?** | RAG (Retrieval-Augmented Generation) để truy xuất và tóm tắt tri thức từ 100.000+ tài liệu nghiên cứu nội bộ. Tool "Debrief" ghi chép cuộc họp, tóm tắt action items và đồng bộ CRM tự động. | AI + ML giám sát hành vi nhân lực toàn diện: tracking badge, Zoom calls, email, điện thoại, keystrokes, mouse clicks, lịch họp và dữ liệu từ điện thoại Blackberry. |
| **Người dùng chính là ai?** | ~16.000–20.000 Financial Advisors (FA) tại mảng Wealth Management. | Toàn bộ ~300.000 nhân viên JPMorgan Chase; quản lý là người xem dashboard. |
| **Chỉ số cụ thể họ đo** | • Tỷ lệ áp dụng (Adoption Rate): **98%** FA đang dùng hàng ngày *(nguồn: [OpenAI Case Study](https://openai.com/index/morgan-stanley/))* <br>• Document retrieval efficiency tăng từ **20% → 80%** *(nguồn: [CTO Magazine](https://ctomagazine.com/ai-in-morgan-stanley-shaping-the-future-of-financial-services/))* <br>• Tiết kiệm ~**30 phút/cuộc họp** nhờ Debrief; ~**15 giờ/tuần** nhờ tự động hoá tác vụ hành chính *(nguồn: [Klover.ai](https://www.klover.ai/morgan-stanley-ai-strategy-analysis-of-ai-dominance-in-financial-services/))* <br>• Net new assets Q3/2024: **$64 tỷ** — ban lãnh đạo quy một phần cho AI tools *(nguồn: [Klover.ai](https://www.klover.ai/morgan-stanley-ai-strategy-analysis-of-ai-dominance-in-financial-services/))* | • Thời gian có mặt qua badge swipe, desk reservation <br>• Số phút Zoom / email / cuộc gọi / keystrokes / mouse clicks <br>• Điểm "unique contributor" vs "regular worker" vs "dead weight" theo AI scoring *(nguồn: [WADU leak document](https://www.linkedin.com/pulse/j-p-morgans-wadu-employee-data-surveillance-system-medha-rashmi-h7uac/))* <br>• Biometric: mức độ tập trung (attention) và căng thẳng (stress) qua camera HD theo thời gian thực |
| **Chỉ số đó thuộc lớp nào?** | Productivity (Time saved) → Quality (Retrieval accuracy) → Business Outcome (Net new assets) | Activation / Engagement (volume-based) → Surveillance (behavior-based) |
| **Chỉ số đó chứng minh được gì?** | • Công cụ được dùng thực sự (98% adoption = không phải "shelf-ware") <br>• Tốc độ tìm thông tin tăng vượt bậc (20% → 80% retrieval efficiency) <br>• Thời gian hành chính được thu hồi → FA có thêm capacity phục vụ khách | • Sự hiện diện vật lý và khối lượng thao tác thô (số tin nhắn, số click) <br>• Nhân viên đang "trông có vẻ bận" |
| **Chỉ số đó chưa chứng minh được gì?** | • Chất lượng tư vấn cuối cùng của FA sau khi có AI <br>• Hiệu suất thực tế của danh mục đầu tư khách hàng <br>• Liệu AI có làm FA over-rely và bỏ qua kiểm chứng thủ công không | • Hiệu suất thực tế hay chất lượng tư duy của nhân viên <br>• Liệu output có tốt hơn không <br>• Sự sáng tạo, khả năng giải quyết vấn đề — những thứ "không thể đo bằng camera" |
| **Thiếu chỉ số nào?** | • Chỉ số về độ chính xác nội dung AI cung cấp (hallucination rate) <br>• Client satisfaction sau khi FA dùng AI <br>• Tỷ lệ FA kiểm chứng lại thông tin AI trả về | • Chất lượng ý tưởng và sự sáng tạo <br>• Employee Net Promoter Score (eNPS) / mức độ gắn kết thực sự <br>• Output quality thay vì output volume |
| **Rủi ro lớn nhất** | FA over-reliance: tin vào AI mà bỏ bước kiểm chứng, đặc biệt nguy hiểm với thông tin tài chính nhạy cảm | "Gaming the system": nhân viên dùng **mouse jiggler** để giả vờ đang làm việc; tập trung vào "trông có vẻ productive" thay vì làm việc thực sự *(nguồn: [eFinancialCareers](https://www.efinancialcareers.com/news/2022/05/jpmorgan-spying-on-employees))* |
| **Hậu quả thực tế đã xảy ra** | Chưa có báo cáo sự cố lớn. Morgan Stanley đạt 2024 Model Wealth Manager Award *(nguồn: [Celent](https://www.celent.com/en/insights/531525129))* | Nhân viên phản ứng dữ dội: **56% nhân viên bị giám sát báo cáo căng thẳng cao**, **59% cho rằng tracking làm giảm trust** *(nguồn: [ExpressVPN / Apploye](https://apploye.com/blog/employee-monitoring-statistics/))* <br>Nghiên cứu HBR: giám sát kiểm soát → **tăng hành vi phản tác dụng** *(nguồn: [HBR 2024](https://hbr.org/2024/02/surveilling-employees-erodes-trust-and-puts-managers-in-a-bind))* |
| **Bài học cho dashboard nhóm** | AI nên đóng vai trò **"thủ thư" hỗ trợ** (empowerment), không phải người quyết định. Con người là trung tâm kiểm chứng. Đo adoption rate & time saved chỉ là lớp đầu — cần tiến lên đo quality và business outcome. | **Metric sai lệch → hành vi sai lệch.** Khi đo "effort signals" (số prompt, thời gian online), người dùng sẽ tối ưu theo effort signals thay vì theo giá trị thật. Dashboard không được đo "nỗ lực ảo". |

---

## Câu Chốt Của Nhóm

```markdown
Case thành công dạy nhóm tôi rằng:
Công cụ AI tốt nhất là công cụ giúp con người làm việc thông minh hơn (Empowerment) 
bằng cách tối ưu hóa truy cập tri thức — chứng minh được bằng chỉ số cụ thể theo lớp:
Adoption Rate (98%) → Retrieval Efficiency (20%→80%) → Time Saved (30 min/meeting) → Business Outcome ($64B net new assets).
Nhưng cần luôn duy trì quy trình kiểm chứng thủ công để tránh over-reliance.

Case thất bại/cảnh báo dạy nhóm tôi rằng:
Tập trung vào chỉ số giám sát bề nổi (keystrokes, Zoom minutes, badge swipes) 
phản tác dụng và có bằng chứng khoa học: 56% nhân viên bị giám sát báo cáo stress cao,
nhân viên chuyển sang "gaming" (mouse jiggler) thay vì làm việc thật.
Đo volume thay vì value là sai ngay từ gốc.

Vì vậy dashboard nhóm tôi phải tránh:
Dùng chỉ số thuần số lượng (số prompt, thời gian sử dụng, số lần click) 
làm thước đo duy nhất mà thiếu các lớp đo về Quality, Trust và Value.

Dashboard nhóm tôi phải hướng đến:
Đo theo pyramid: Activation → Productivity → Quality → Business Outcome.
Không đo "người dùng có mặt không?" mà đo "người dùng có làm được việc tốt hơn không?"
```

---

## Nguồn Tham Khảo

| Case | Tài liệu | Link |
|---|---|---|
| Morgan Stanley | OpenAI Official Case Study | https://openai.com/index/morgan-stanley/ |
| Morgan Stanley | Morgan Stanley Press Release — Debrief Launch | https://www.morganstanley.com/press-releases/ai-at-morgan-stanley-debrief-launch |
| Morgan Stanley | Celent 2024 Model Wealth Manager Award | https://www.celent.com/en/insights/531525129 |
| Morgan Stanley | CTO Magazine — Retrieval Efficiency 20%→80% | https://ctomagazine.com/ai-in-morgan-stanley-shaping-the-future-of-financial-services/ |
| Morgan Stanley | Klover.ai — $64B net new assets Q3/2024 | https://www.klover.ai/morgan-stanley-ai-strategy-analysis-of-ai-dominance-in-financial-services/ |
| JPMorgan WADU | LinkedIn — WADU Surveillance Explainer | https://www.linkedin.com/pulse/j-p-morgans-wadu-employee-data-surveillance-system-medha-rashmi-h7uac/ |
| JPMorgan WADU | eFinancialCareers — Mouse Jiggler, Paranoia | https://www.efinancialcareers.com/news/2022/05/jpmorgan-spying-on-employees |
| Research chung | HBR 2024 — Surveillance Erodes Trust | https://hbr.org/2024/02/surveilling-employees-erodes-trust-and-puts-managers-in-a-bind |
| Research chung | Apploye — 56% stress, 59% giảm trust | https://apploye.com/blog/employee-monitoring-statistics/ |
| Research chung | SoftwareSeni — Gaming the System | https://www.softwareseni.com/how-employees-game-monitoring-systems-and-the-productivity-paradox-of-workplace-surveillance/ |

---

## Tự kiểm tra

- [x] Không chỉ kể chuyện case — có phân tích chỉ số theo lớp.
- [x] Có nêu chỉ số cụ thể: 98% adoption, 20%→80% retrieval, 30 min/meeting, $64B, 56% stress, 59% trust loss.
- [x] Có link tài liệu uy tín: OpenAI, Morgan Stanley chính thức, HBR, Celent.
- [x] Có nói chỉ số chứng minh được gì và không chứng minh được gì.
- [x] Có ít nhất 1 bài học áp dụng vào dashboard nhóm: đo theo pyramid Activation → Productivity → Quality → Business Outcome; tránh đo "effort signals".
