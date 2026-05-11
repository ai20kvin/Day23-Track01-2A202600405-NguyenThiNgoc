# Day 23 — Product ROI Dashboard (Parts A–D) — TrustLayerAI

> **Nộp bài:** `03-product-roi-dashboard.md` . Cấu trúc: thách thức nhóm → case → **Part A** phạm vi + 4 workflow → chẩn đoán gốc → **Part B** roadmap 30/60/90 + tactic → **Part B** chỉ số product + per-workflow → **Part C** mock → red-team + **v1→v2 (≥2)** → **Part D** memo.

| Phần rubric Day 23 | Vị trí trong file này |
|---|---|
| Part A — Adoption Context | §1–3 (thách thức, pattern, sản phẩm, 4 workflow, ADKAR + tactic) |
| Part B — ROI Dashboard (8 cột) | §6 D.1 + D.2 (Layer / Metric / Baseline / Target / Data source / Owner / Red-team / Fix) |
| Part C — Dashboard mock | §7 |
| Part D — Decision memo (4 câu) | §9 |
| Red-team + sửa v2 | §8 |

---

| Sản phẩm / công cụ AI chọn phân tích | TrustLayerAI — Platform đánh giá chất lượng RAG/Enterprise Search |
| Người dùng chính | Data engineers, Search engineers, Enterprise Search teams, Knowledge managers |

---

## 1. Ghi Chú Thách Thức Áp Dụng AI Cá Nhân

Mỗi người viết 1-2 tình huống trong 10 phút đầu, không dùng AI.

| Thành viên | Tình huống AI bị kẹt | Dấu hiệu bị kẹt | Giả thuyết ban đầu |
|---|---|---|---|
| Dev Lead | Search engineers không dùng evaluation metrics trên TrustLayerAI để decide khi nào release RAG version mới | Team chạy evaluation, thấy số good, nhưng vẫn phải người review bây giờ = không dùng output của TrustLayerAI trong workflow thật | Metrics hiển thị kỹ thuật không match quyết định kinh doanh (release/don't release) |
| PM | User testing RAG baseline performance nhưng không configure TrustLayerAI để track improvement sau mỗi tuning | Chỉ có số liệu ban đầu, không biết version nào tốt hơn, feedback loop đứt | Lack of clear acceptance criteria khi nào enough good để release |
| Data Eng | Knowledge team không biết chỉ số nào để monitor trong production (retrieval rate, answer quality, latency, coverage) | Dashboard hiển thị 50 metrics, team không biết focus vào metric nào → paralysis | ADKAR Ability: team không training để hiểu cách dùng TrustLayerAI trong ops |

### Nhóm gom lại thành 3-5 pattern

| Pattern | Tình huống liên quan | Vì sao đáng chọn cho lab? |
|---|---|---|
| 1 — Metrics vs. Decision | Evaluation metrics lẻ loi, không gắn quyết định release/pivot/kill | TrustLayerAI có 50+ metric available nhưng không có curated set để decide |
| 2 — Workflow Review Loop | Team dùng TrustLayerAI để demo nhưng không đưa vào workflow thật (chỗ search engineers decide improvement) | Adoption chỉ ở Wow phase (demo), chưa Normalization (trong quy trình hàng ngày) |
| 3 — Production Monitoring | Không biết metric nào để monitor RAG quality sau release into production | TrustLayerAI evaluation ở dev, nhưng production không có equivalent |
| 4 — Training & Ownership | Data engineers không rõ ai chịu trách nhiệm follow-up evaluation khi baseline shift | Diffusion có (công cụ cài đặt), normalization không có (không ai maintain) |

**Thách thức nhóm chọn để làm lab:**  

```markdown
TrustLayerAI là platform đánh giá chất lượng RAG/Enterprise Search.
Chúng tôi xây nó tốt: có 50+ metrics, integration với LLM, dashboard đẹp.
Nhưng Search/Data Engineering teams không dùng nó để make decision thật.
Nguyên nhân: metrics kỹ thuật ≠ business decision framework.
Cần: curated metrics + workflow redesign + owner + production monitoring.
```

---

## 2. Bảng So Sánh Case Thành Công / Thất Bại

Mỗi nhóm phân tích 1 case thành công và 1 case thất bại/cảnh báo. Dùng `04-reference/case-clinic-summary.md` nếu cần.

| Trường | Case thành công | Case thất bại/cảnh báo |
|---|---|---|
| Case | Klarna AI Assistant (2024-2025) | IBM Watson for Discovery (2011-2015) |
| AI được dùng trong quy trình nào? | Customer service: AI triage + draft response để agent review + send | Enterprise Search: AI semantic search để user tìm document trong knowledge base |
| Họ đo chỉ số gì? | Deflection rate (2.3M conversations = 2/3 volume), handling time ↓, cost/agent equiv. 700 FTE | Accuracy metrics, F1 score, time-to-retrieve — nhưng chủ yếu focus kỹ thuật |
| Chỉ số đó chứng minh được gì? | AI xử lý được tầng lớp query loại routine tốt, productivity ↑ significantly | Model performance cao trong testing, system hoạt động theo spec |
| Chỉ số đó chưa chứng minh được gì? | Customer satisfaction trend, whether complex cases handled better, quality/brand impact | Adoption rate của team, khi nào user tin AI output, việc AI đã replace con người hay chỉ thêm giây phút review |
| Thiếu chỉ số nào? | NPS trend, escalation rate (user perception), revenue/retention impact, agent job satisfaction | Usage in production, time-to-value, user behavior change, enterprise ROI measurable |
| Bài học cho dashboard nhóm | Outcome metrics (deflection, handling time) phải pair với trust/quality metrics (NPS, escalation). Nếu deflection ↑ nhưng NPS ↓, metric sai. | Kỹ thuật metrics (F1, accuracy) không đủ để decide adopt/scale. Cần operational metrics (usage, trust, value). Lack of metrics = project eventually killed despite good model. |

**1 bài học nhóm sẽ áp dụng ngay:**  

```markdown
Klarna sau đó adjust lại focus (2025) để balance giữa cost-cutting vs. customer experience.
Bài học: nếu chỉ đo cost/deflection mà không đo quality/trust, dự án có thể scale sai hướng.

Cho TrustLayerAI: metrics phải có 3 lớp:
1. Kỹ thuật (retrieval precision, latency) — good for tuning
2. Operational (adoption, query quality, false positives) — good for workflow fit
3. Business (time-to-value, cost savings, revenue impact) — good for decisions

Thiếu bất kỳ lớp nào = nhóm Search không commit dùng TrustLayerAI thường xuyên.
```

---

## 3. Phần A — Thách Thức Và Phạm Vi Sản Phẩm

| Trường | Trả lời |
|---|---|
| Thách thức áp dụng AI | Metrics không gắn quyết định. Teams có TrustLayerAI nhưng không dùng output để decide release/pivot/kill. Workflow review vẫn manual. Không có production monitoring. |
| Sản phẩm / công cụ AI | TrustLayerAI — Platform evaluation chất lượng RAG/Enterprise Search. 50+ metrics, integration LLM (Claude, GPT-4), automated evaluation, dashboard, API. |
| Người dùng chính | Search engineers (1-3 per company), Data engineers (decide RAG tuning), PM/Stakeholders (decide release). Secondary: QA teams, Knowledge managers. |
| Bối cảnh sử dụng | Dev/staging environment (tuning RAG); Production environment (monitoring real-world query quality). Enterprise orgs with internal search, chatbot, knowledge retrieval. |
| Mục tiêu kinh doanh / học tập / vận hành | Business: reduce time-to-RAG-value, improve adoption rate, measure ROI per customer. Learning: train teams to trust AI evaluation. Ops: establish quality gates before prod release. |

### 2-4 quy trình chính

| # | Tên quy trình | Vai trò AI | Điểm người kiểm tra | Khi AI sai thì xử lý thế nào? |
|---|---|---|---|---|
| 1 | Thiết lập Evaluation & Thiết kế Test | TrustLayerAI tạo evaluation dataset (câu hỏi tổng hợp) từ tài liệu; AI đề xuất kịch bản test | Data engineer kiểm tra phân phối dataset, độ khó câu hỏi, độ bao phủ các use case | Lấy mẫu thủ công: QA kiểm tra 10% câu hỏi tổng hợp để xác nhận liên quan trước dùng |
| 2 | Chạy Evaluation RAG (Dev) | TrustLayerAI lấy top-K docs, AI đánh giá chất lượng câu trả lời (chính xác, liên quan); tạo dashboard metrics | Search engineer kiểm tra spot-check 20 kết quả: tài liệu đúng? chất lượng câu trả lời? metrics được calibrate? | Nếu F1 score ≠ validation thủ công, điều chỉnh ngưỡng similarity hoặc retrain embedding model |
| 3 | Quyết định Release | TrustLayerAI tổng hợp metrics (độ chính xác retrieval, latency, false positive rate); AI đề xuất release/giữ | PM + Search lead review: đạt mục tiêu metrics? rủi ro chấp nhận? sự aligned các bên liên quan? | Nếu phát hiện chất lượng giảm → điều tra nguyên nhân gốc, có thể rollback hoặc giữ release |
| 4 | Giám sát Production | TrustLayerAI giám sát query live: theo dõi drift mô hình query, xu hướng chất lượng câu trả lời, lỗi đột ngột | Search engineer on-call review metrics hàng ngày, điều tra anomalies, escalation alerts | Nếu chất lượng giảm >10% YoY, kích hoạt retuning. Nếu mô hình lỗi mới, escalate team |

**Rào cản ADKAR cấp sản phẩm (chính):** **Ability** (đọc hiểu & hành động theo metrics) và **Reinforcement** yếu (không owner theo dõi hằng ngày). **Desire** có thể yếu nếu team nghi metrics “để báo cáo”. *Bối cảnh VN / nhóm:* thêm kênh phản hồi **ẩn danh** + phiên **1:1** với champion để người dùng nói thẳng metric vô nghĩa / sợ bị đánh giá khi override AI eval.

---

## 4. Phần B — Chẩn Đoán Nguyên Nhân Gốc

Dùng 2-3 lăng kính. Không cần dùng tất cả.

| Lăng kính | Câu hỏi | Chẩn đoán của nhóm | Evidence / quan sát |
|---|---|---|---|
| Quy trình công việc | Công việc thật có đổi không, hay chỉ thêm AI ở ngoài? | TrustLayerAI là add-on, không có trong workflow chính. Search engineers vẫn review manually sau. Không có gate: "if metric X < threshold, hold release." | 1 customer: Search team runs eval, metrics look good, nhưng vẫn phải QA review tất cả 100 results trước release. TrustLayerAI output bị ignore. |
| ADKAR | Người dùng kẹt ở Awareness / Desire / Knowledge / Ability / Reinforcement? | Kẹt ở Ability: Data engineers biết TrustLayerAI exists, nhưng không rõ how to interpret metrics hoặc when to trust output. Reinforcement cũng yếu: không ai assigned to review metrics daily. | Feedback từ 3 customers: "chúng tôi không biết 50 metrics đó có nghĩa gì" + "không ai phụ trách theo dõi" |
| Mức sẵn sàng | Dữ liệu, quyền truy cập, người phụ trách, governance, budget đã sẵn sàng chưa? | Dữ liệu: có (documents, queries). Quyền truy cập: có. Người phụ trách: KHÔNG. Governance: chỉ có kỹ thuật, không có business rules (e.g., "release nếu F1 > 0.75 AND latency < 200ms AND NPS drift < 5%"). | Org không allocate headcount cho "TrustLayerAI metrics owner". TrustLayerAI bị orphaned. |
| Chỉ số | Team đang đo usage hay đo value thật? | Đo usage (# evaluations run, # integrations). Không đo adoption (how many released decisions were informed by metrics?). Không đo value (time saved in QA? risk reduced? confidence ↑?). | Internal metric: only 5/50 customers run evaluation >1x/month. Adoption stalled after month 2. |
| Niềm tin / chất lượng | Người dùng có tin output không? Khi AI sai thì xử lý thế nào? | Trust issue: when F1 score = 0.82, Search engineer asks "is that good?". No clear answer → default to manual review. When AI evaluation disagrees with manual → no escalation path, decision unclear. | 1 escalation: customer said "metric said F1 = 0.85, release. Reality: 40% false positives in prod. Metric was wrong." → lost trust, customer deprioritized TrustLayerAI. |

### Nguyên nhân gốc nhóm chọn

| # | Nguyên nhân gốc | Vì sao đây là nguyên nhân chính? | Case nào hỗ trợ cách nhìn này? |
|---|---|---|---|
| 1 | Workflow review chưa có business gate rõ (nên có rule: "release nếu metrics X, Y, Z meet targets") | Search engineers review metrics nhưng không biết quy tắc decide. Không ai chỉ định responsible. Workflow vẫn cần manual QA 100%. Số cost/benefit không change. | 1 customer feedback: metrics look good nhưng "chúng tôi vẫn QA bằng tay 100% results. TrustLayerAI chưa được dùng trong decision." IBM Watson: failed partly vì không có business decision framework liên kết metrics → adoption |
| 2 | Metrics curated set thiếu, 50 metrics tổng quát → không guide decisions. Cần <10 core metrics + production monitoring + alert rules. | Teams overwhelmed by 50 metrics, paralysis, default to manual review. Klarna: fixed issue này với 3 core metrics (deflection, NPS, latency) + adjust trong 2025. | Klarna case: theo reference doc, họ initially measured tỷ lệ deflection rất cao, but NPS impact unclear. Sau đó adjust vì discover chỉ số bị lệch. |



---

## 5. Phần C — Giải Pháp Và Lộ Trình 30/60/90 Ngày

| Mốc | Việc cần làm | Người phụ trách | Dấu hiệu hoàn thành | Rủi ro còn lại |
|---|---|---|---|---|
| 0-30 ngày | **Định nghĩa core metrics + quy tắc quyết định.** Làm việc với 2-3 khách hàng hàng đầu để chọn <10 core metrics (ví dụ: retrieval precision, latency, false positive rate, coverage). Định nghĩa gates: "release nếu F1>0.75 AND latency<200ms AND quality ổn định." Xây dựng decision checklist. | Product Manager + Senior Search Engineer (customer advocate) | 1 decision rubric được 2+ khách hàng sign off. Rubric trong Notion. | Orgs có thể phản đối nếu rules block timeline tham vọng |
| 30-60 ngày | **Workflow redesign: làm evaluation thành phần của release checklist.** Thêm TrustLayerAI step vào CI/CD (sau tuning, trước QA staging). Tạo "Metric Review" ceremony (30 phút weekly) với Search team + PM. Train 5 power users về interpret metrics + dùng decision rubric. | Search Lead (ceremony owner) + Training PM | 3x runs của release gate với evaluation. Tất cả gate criteria meet 80%+ cases. Training completion 5/5 người. | Team có thể revert workflow cũ nếu ceremony cảm thấy bureaucratic. Training recall thấp nếu không reinforcement. |
| 60-90 ngày | **Production monitoring + feedback loop.** Deploy TrustLayerAI monitoring tới production RAGs (real-world queries). Set alerts cho quality dip >10%. Thiết lập biweekly "Metrics Review Board" (resolve prod incidents, adjust thresholds). Document lessons: metrics nào drifted, tại sao, cách fix. | Search Lead (on-call) + Data Engineer (monitoring setup) | 2+ prod incidents detected sớm via alerts. 1 threshold adjustment dựa prod data. Retrospective doc viết. | Production noise có thể tạo alert fatigue. Teams có thể ignore weak signals sớm. |

### 3 tactic áp dụng

| Tactic | Nhắm vào barrier nào? | Áp dụng cho quy trình nào? | Người phụ trách |
|---|---|---|---|
| 1 — Decision Rubric + Gate in CI/CD | Ability (teams don't know when to trust metrics) + Workflow (no gate). | Workflows #2 + #3 (Evaluation + Release Decision). | Product Manager (build rubric). Search Lead (integrate into CI/CD). |
| 2 — Metric Review Ceremony (30 min/week) + Power User Training | Reinforcement (no one maintains metrics). Desire (team skeptical if no role models champion it). | Workflow #3 + #4 (Release Decision + Production Monitoring). | Search Lead (run ceremony). Training PM (train 5 power users to model behavior). |
| 3 — Production Monitoring + Alert Rules | Ability + Reinforcement. Current state: no production visibility. | Workflow #4 (Production Monitoring). | Data Engineer (set up monitoring). Search Lead (on-call, respond to alerts). |



---

## 6. Phần D — Dashboard Đo ROI Của Sản Phẩm

### D.1 Chỉ số toàn sản phẩm

| Lớp đo | Chỉ số | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu | Người phụ trách | Rủi ro từ phản biện | Sửa ở v2 |
|---|---|---:|---:|---|---|---|---|
| Activation | Khách hàng chạy evaluation (>0 lần trong tháng 1) | 45/60 (75%) | 50/60 (83%) | TrustLayerAI analytics | Product Manager | Metric virtual: activation ≠ adoption. | Theo dõi "chạy evaluation >1x/tháng" thay vào đó. |
| Retention / Value | Tỷ lệ adoption: khách hàng chạy evaluation >1x/tháng | 12/60 (20%) | 30/60 (50%) | TrustLayerAI analytics | Product Manager | 75% tháng 1 giảm xuống 20% ongoing. Cho thấy adoption cliff. | Giữ metric này. Nó thành thật. |
| Trust | Metric agreement: QA thủ công vs. TrustLayerAI F1 score, % alignment | 68% | 85% | Customer feedback + spot-check | Search Lead | Dữ liệu baseline thưa (3 khách hàng). | Thêm: "documented disagreement reasons." |

### D.2 Chỉ số theo từng quy trình

Sao chép block dưới cho mỗi quy trình đã chọn. Mỗi quy trình cần ít nhất 4 lớp đo, ưu tiên Productivity + Quality + Trust + Value.

#### Quy trình 1 — Evaluation Setup & Test Design

*(6 lớp: Activation → Engagement → Productivity → Quality → Trust → Value)*

| Lớp đo | Chỉ số | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu | Người phụ trách | Rủi ro từ phản biện | Sửa ở v2 |
|---|---|---:|---:|---|---|---|---|
| Activation | Khách hàng tạo evaluation (≥1 eval trong tháng 1) | 48/60 (80%) | 52/60 (87%) | Account audit | PM | Activation cao nhưng retention thấp. | Giữ — cho thấy step 1 hoạt động. Vấn đề thực sự ở sau. |
| Engagement | Khách hàng xem lại evaluation sau tháng 1 (≥2 evals trong tháng 2-3) | 14/48 (29%) | 28/48 (58%) | Analytics | PM | Engagement thấp sau onboarding. | Chia tách metric: "tạo dataset" vs. "chạy evaluation hai lần" để cô lập bottleneck. |
| Productivity | Thời gian trung bình-đến-eval-đầu tiên (ngày từ tạo account đến eval đầu tiên) | 14 ngày | 5 ngày | Onboarding logs | Onboarding PM | 14 ngày chậm. Friction thiết lập cao. | Theo dõi riêng: "thời gian-import" + "thời gian-tạo-dataset" + "thời gian-eval." |
| Quality | Chất lượng synthetic dataset: % của 100 câu hỏi mẫu được đánh giá "tốt" bởi người đánh giá | 82% | 90% | Manual QA sample (10%) | QA Reviewer | Edge cases thất bại im lặng. | Theo dõi chất lượng theo độ khó (dễ/trung bình/khó). |
| Trust | Customer feedback: "chất lượng dataset" NPS | +22 (2/5 stars) | +55 (4.5/5 stars) | Survey | Customer Success | NPS thấp gợi ý friction dataset, không phải metrics. | Hỏi: "% câu hỏi cảm thấy thực tế cho trường hợp dùng của bạn?" |
| Value | Chi phí cơ hội tránh “release sai”: # release candidate bị **hold** nhờ eval phát hiện regression (mỗi quý / khách) | 0.4/Q | ≥1/Q | Release notes + TrustLayerAI eval logs | PM + Search Lead | Hold count dễ “game” nếu không định nghĩa regression. | Định nghĩa rule: hold chỉ khi có ticket RCA + link eval run ID. |


#### Quy trình 2 — Chạy RAG Evaluation (Dev)

| Lớp đo | Chỉ số | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu | Người phụ trách | Rủi ro từ phản biện | Sửa ở v2 |
|---|---|---:|---:|---|---|---|---|
| Activation | Khách hàng chạy quy trình evaluation đầy đủ (≥1 lần chạy hoàn chỉnh) | 28/60 (47%) | 40/60 (67%) | Workflow logs | PM | <50% hoàn thành đầy đủ eval. Cho thấy friction UX. | Điều tra: nơi nào 50% bỏ cuộc? (upload vs. compute vs. review?) |
| Engagement | Khách hàng chạy lại evaluation ≥3 lần trong 60 ngày (tuning RAG lặp lại) | 8/28 (29%) | 18/28 (64%) | Eval history | PM | Chỉ 29% lặp lại. Gợi ý không có feedback loop đóng. | Thiết lập "metric cải thiện X% sau tuning" signal. |
| Productivity | Thời gian trung bình-chạy-eval-đầy đủ (phút: indexing + embedding + metrics) | 35 phút | 15 phút | Perf logs | Data Engineer | Có thể không phải bottleneck. | Giữ theo dõi. Nếu tốc độ nhanh nhưng adoption thấp, nó không phải blocker. |
| Quality | Metric calibration: % metrics có signal có ý nghĩa (variance/stability) | 65% (6/10 metrics có signal) | 85% | Metric output logs | Data Science Eng | 50 metrics quá nhiều. Chỉ 6 có signal. Xác nhận paralysis. | CÓ THỂ HỮU DỤNG metrics không có signal. Tập trung vào 8-10 metrics chính. |
| Trust | Validation rate: % kết quả TrustLayerAI được validating bằng spot-check thủ công trong 2 tuần | 40% (12/30 runs) | 75% | Support tickets | Customer Success | Validation thấp = trust thấp. | Giữ theo dõi. Cho thấy exact trust gap. Drives "decision rubric" tactic. |
| Value | Thời gian tiết kiệm mỗi lần eval (QA testing được thay bằng TrustLayerAI vs. baseline) | 2 giờ | 6 giờ | Customer feedback + time-tracking | Customer Success | Baseline comparison mơ hồ. Khách hàng có thể thêm TL on top, không thay thế. | Đo "thời gian từ release candidate đến release decision." TL rút ngắn review cycle? |


#### Quy trình 3 — Quyết định Release

| Lớp đo | Chỉ số | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu | Người phụ trách | Rủi ro từ phản biện | Sửa ở v2 |
|---|---|---:|---:|---|---|---|---|
| Activation | Khách hàng quyết định release dựa vào TrustLayerAI trong 60 ngày (≥1 release) | 5/60 (8%) | 20/60 (33%) | Customer check-in | Customer Success | 8% tệ hại. Hầu hết không dùng TL cho release gate. ĐÂY là adoption problem. | Di chuyển sang product-level. Nếu 80% chưa dùng cho decision, không adopt. |
| Engagement | Khách hàng quyết định release ≥2 lần dựa vào TrustLayerAI (lặp lại quy trình) | 1/5 (20%) | 4/5 (80%) | Customer call | Customer Success | 80% chỉ quyết định 1 lần. Repeatability thấp. | Một khi "decision rubric" tactic triển khai, cái này phải nhảy vọt. |
| Productivity | Thời gian từ "RAG sẵn sàng review" đến "release decision made" | 4 ngày | 1 ngày | Project timeline | Customer Success | Baseline mơ hồ do variance bureaucracy. | Đo: "thời gian từ eval report available đến decision." Cô lập TL impact. |
| Quality | Độ chính xác quyết định: "khi metrics nói release (met rubric), RAG có hoạt động tốt trong prod?" Đo 30 ngày post-release. | Chưa có baseline | 95% (≤5% issues) | Post-launch feedback + error logs | Customer Success + Data Eng | Chưa có baseline = không biết rubric có hoạt động không. | ĐÚNG rủi ro. Thêm "30-day post-launch review" cho mỗi khách hàng release. |
| Trust | Decision friction: incidents nơi khách hàng override metric rubric để release | 2 incidents | 0 incidents | Support tickets | Customer Success | 2 incidents gợi ý rubric quá strict. | Giữ theo dõi. Nếu giữ ở 0, confidence tăng. |
| Value | Release velocity: # RAG releases mỗi khách hàng mỗi quý (trước vs. sau adoption) | Trước: 2/Q; Sau: 2/Q (chưa change) | Sau: 4/Q | Customer data | Customer Success | Chưa cải thiện velocity. Có thể culture, không phải tool. | Kỳ vọng — adoption cliff means few customers ramped up eval. Khi adoption tăng, should improve. |


#### Quy trình 4 — Giám sát Production

| Lớp đo | Chỉ số | Mốc hiện tại | Mục tiêu | Nguồn dữ liệu | Người phụ trách | Rủi ro từ phản biện | Sửa ở v2 |
|---|---|---:|---:|---|---|---|---|
| Activation | Khách hàng triển khai TrustLayerAI monitoring đến production (≥1 RAG trong prod với live monitoring) | 2/60 (3%) | 15/60 (25%) | Account audit | PM | 3% rất thấp. Production monitoring bước adoption khó nhất. Có thể yêu cầu integration + ops commitment. | CÓ. Đề xuất: (a) quick-start template, (b) managed monitoring service option. |
| Engagement | Khách hàng xem production metrics ≥weekly (dashboard/alerts active) | 0/2 (0%) | 2/2 (100%) | Dashboard audit logs | Data Engineer | 0% means 2 người deploy không dùng active. Monitoring orphaned. | Không có owner gán cho customer side. Tactic: "assign on-call" hoặc offer managed alerting. |
| Productivity | Alert response time: "từ alert fire đến root cause identified" | N/A (0 incidents) | <4 giờ | Post-mortem logs | On-call Eng | Không có prod data = không validate được. Sẽ đến khi more customers go live. | Đúng. Xây dựng "playbook: what to do when alert fires?" trước. |
| Quality | Production metric stability: coefficient of variation của daily metrics (không model change) | N/A | <5% CoV | Monitoring history | Data Science Eng | Noisy metrics destroy trust. Nếu F1 jump ±20% không giải thích, customers stop checking. | **Rủi ro cao.** Set up "metric smoothing" hoặc "confidence intervals." |
| Trust | Production-dev metric agreement: "khi dev eval nói F1=0.75, F1 là bao nhiêu trong prod trên similar queries?" | N/A | >85% agreement | Prod logs vs. dev eval | Customer + Data Eng | Biggest risk: dev evals optimistic, prod reality different. Ships expecting 0.75, gets 0.60. Destroy trust. | **Rủi ro cao.** Validate trước scaling. Tactic: "validation playbook cho dev-prod gaps." |
| Value | Production quality cost: "% queries cần human escalation (false positive, không retrieval, vv)" YoY trend | N/A | <5% escalation | Support ticket volume trên RAG failures | Customer + Support | End-to-end value metric. Chỉ visible khi trong prod. | NORTH STAR. Khi 10+ customers với prod monitoring, đo true ROI. |


---

## 7. Phần E — Dashboard Mock

Vẽ 4-6 ô. Ô đầu tiên là tình trạng toàn sản phẩm, các ô sau là tín hiệu theo quy trình hoặc quyết định.

```text
┌──────────────────────────────────┐ ┌──────────────────────────────────┐
│ TILE 1: SỨC KHỎE SẢN PHẨM         │ │ TILE 2: ADOPTION CLIFF           │
│ Tỷ lệ Adoption                   │ │ Tháng 1: 45/60 (75%)             │
│ 12/60 (20%)                      │ │ Ongoing: 12/60 (20%)             │
│ Xu hướng: ↓ ĐÃ DỪNG ↓             │ │ Xu hướng: ↓ CLIFF ↓              │
│ Trạng thái: ĐỎ — CÔN CHÍNH        │ │ Trạng thái: ĐỎ — Activation drop│
│ Hành động: Triển khai tactic #1-2│ │ Hành động: Cần decision rubric   │
└──────────────────────────────────┘ └──────────────────────────────────┘

┌──────────────────────────────────┐ ┌──────────────────────────────────┐
│ TILE 3: QUYẾT ĐỊNH RELEASE       │ │ TILE 4: CHẤT LƯỢNG EVALUATION    │
│ Dùng Metrics để Release          │ │ Metric Calibration               │
│ 5/60 (8%)                        │ │ 6/50 metrics có signal (12%)     │
│ Xu hướng: → BẰNG →               │ │ Xu hướng: ↓ THẤP ↓               │
│ Trạng thái: ĐỎ — Gần như không   │ │ Trạng thái: VÀNG — Analysis xóa │
│ Hành động: Định nghĩa release    │ │ Hành động: Hủy 40 metrics       │
│              rubric             │ │                                  │
└──────────────────────────────────┘ └──────────────────────────────────┘

┌──────────────────────────────────┐ ┌──────────────────────────────────┐
│ TILE 5: NIỀM TIN - VALIDATION    │ │ TILE 6: MEMO QUYẾT ĐỊNH          │
│ Customer Manual Validation       │ │ Tiếp tục / Pivot / Dừng          │
│ 40% kết quả được validating      │ │ ► PIVOT                          │
│ Xu hướng: → BẰNG →               │ │ Giai đoạn 1: Decision rubric (30d)│
│ Trạng thái: VÀNG — Cần confidence│ │ Giai đoạn 2: Workflow redesign(60d)│
│ Hành động: Decision rubric/train │ │ Giai đoạn 3: Prod monitoring(90d)│
└──────────────────────────────────┘ └──────────────────────────────────┘
```

---

## 8. Phần F — Phản Biện Vai Và Sửa V2

### Nhóm mình đi phản biện nhóm khác

| Vai nhóm được giao | Người đóng vai | Nhóm bị phản biện | 3 câu hỏi / rủi ro nhóm mình nêu |
|---|---|---|---|
| CFO | Nguyễn Hữu Quang | Nhóm bạn (ví dụ: chatbot nội bộ) | “Chỉ số nào quy đổi được thành tiền / rủi ro tài chính nếu RAG sai?” |
| User | Nguyễn Thị Ngọc Thư | Nhóm bạn | “Metric có ép người dùng ‘làm đẹp số’ (chạy eval cho có) không?” |
| Risk | Nguyễn Thị Ngọc | Nhóm bạn | “Khi dev eval ≠ prod: ai chịu trách nhiệm, audit trail ở đâu?” |
| Workflow owner | Trần Vọng Triển | Nhóm bạn | “Ai pull báo cáo hàng tuần và ai hành động khi tile đỏ?” |

**Gói tự red-team nội bộ (khi chưa có nhóm đối tác):** vai CFO đặt các câu dưới đây cho chính dashboard TrustLayerAI.

| Vai nhóm được giao | Nhóm bị phản biện | 3 câu hỏi / rủi ro nhóm mình nêu |
|---|---|---|
| CFO / Business | TrustLayerAI (internal) | 1. "Tỷ lệ adoption chỉ 20% ongoing — tại sao chúng ta nên đầu tư vào lộ trình 30/60/90?" Chứng minh ROI ở đâu? 2. "Production monitoring là 0% triển khai. Bảo đảm gì dev-prod metrics sẽ thực sự align?" 3. "Thời gian tiết kiệm chỉ 2 giờ per eval. Tại điểm nào giá trị vượt quá cost của integration + training?" |

### Nhóm mình bị phản biện

| Rủi ro được nêu | Chỉ số / giả định bị chất vấn | Nhóm sửa gì ở v2? |
|---|---|---|
| 1 — Adoption cliff risk: nếu chúng ta implement decision rubric nhưng không tăng release adoption, chúng ta đã lãng phí effort | Assumption: "decision rubric sẽ di chuyển adoption từ 8% tới 33% trong 90 ngày." Không có bằng chứng. Nếu rubric quá strict hoặc không aligned customer culture? | **Fix v2:** Thêm metric sớm hơn: "% khách hàng aligned với rubric design trong phase 1 (tuần 1-4)." Nếu <60% agree rubric, escalate PM. Không assume rubric fix; validate customer input trước. |
| 2 — Dev-prod metric disagreement sẽ tank trust | Assumption: "team có thể reach >85% agreement giữa dev eval và prod reality." Nhưng chúng ta có 0 prod deployments. Không biết assumption này realistic không. | **Fix v2:** Thêm "production validation playbook" như mandatory item trong phase 3 (tuần 8+). Trước scaling prod monitoring, chạy 2-3 detailed case studies: eval nói X, prod got Y, tại sao? Document patterns. Thay vague >85% target bằng concrete evidence. |
| 3 — Không owner gán customer side = Reinforcement sẽ fail | Current state: "0/2 khách hàng viewing prod metrics weekly." Tại sao? Vì không ai gán. Tactic nói "assign on-call" nhưng không mandate. | **Fix v2:** Đổi "Engagement" metric sang "Ngày kể từ khách hàng org gán on-call owner." Thêm "assignment call" như week-1 requirement trong prod monitoring onboarding. Nếu khách hàng refuse gán owner, không deploy monitoring. Gate feature. |

### Ít nhất 2 thay đổi cụ thể từ v1 sang v2

| # | V1 có vấn đề gì? | V2 sửa thành gì? | Vì sao sửa này tốt hơn? |
|---|---|---|---|
| 1 | **D.2 Quy trình 3 (Quyết định Release)**: "Độ chính xác quyết định: khi metrics nói release, RAG có hoạt động tốt trong prod?" has "Chưa có baseline." Rủi ro: chúng ta đang thiết kế release gate mà không validating gate hoạt động trong production. | **V2:** Thêm **mandatory action trước scale** trong Phần G (Part D): "Trước release decision gates go live với khách hàng, chạy 3 retrospectives: case 1 (metrics nói good, prod good), case 2 (metrics said good, prod bad), case 3 (metrics marginal, prod edge case)." Điều này cho chúng ta prod validation trước gate. | Validation trước, scaling sau. Không điều này, launch feature trên assumptions. Với điều này, launch feature trên evidence. |
| 2 | **D.2 Quy trình 1**: "Thời gian-đến-eval-đầu tiên" là 14 ngày nhưng chúng ta không chia nhỏ. Không biết nó là document import (chậm), synthetic query generation (AI issue), hay customer indecision. | **V2:** Chia thành 3 sub-metrics: (a) "Thời gian từ account tạo đến documents imported" + (b) "Thời gian từ docs imported đến synthetic dataset tạo" + (c) "Thời gian từ dataset ready đến customer chạy eval đầu tiên." Đo riêng. | Isolates bottleneck. Nếu (a) 10 ngày, friction là data prep, không TrustLayerAI. Nếu (b) 3 ngày, TrustLayerAI nhanh nhưng khách hàng chậm. Different fixes. |
| 3 | **D.2 Quy trình 4 (Production):** Engagement prod = 0/2 xem metrics hàng tuần — tactic “gán on-call” chưa bắt buộc nên monitoring mồ côi. | **V2:** Gate onboarding: không bật prod monitoring nếu phía khách chưa gán on-call owner (tuần 1); đổi engagement sang “đã gán owner trong SLA X ngày”. | Accountability → reinforcement; tránh công cụ được deploy nhưng không ai hành động khi đỏ. |

**Định dạng bắt buộc (ví dụ ngắn):**

```text
V1 issue: "Chạy evaluation >0 lần/tháng 1" — dễ hiểu nhầm là adoption thật.
V2 fix: Đổi north-star sang "release decision dùng TrustLayerAI metrics" + baseline 3 retrospective dev-vs-prod trước khi scale gate.
```

## 9. Phần G — Memo Quyết Định

```markdown
# Memo Quyết Định Cuối Cùng — TrustLayerAI

**Ngày:** 11 tháng 5, 2026  
**Tác giả:** Nhóm Track 1 (VinUni A20 — Day 23)  
**Trạng thái:** PIVOT (lộ trình 30/60/90)

## 1. Khuyến nghị: PIVOT (không dừng, không tiếp tục as-is)

**Lý do:** 
- Activation tốt (75% tháng 1) nhưng adoption cliff nghiêm trọng (75% → 20% ongoing).
- Root cause: Workflow chưa có business gate rõ ràng, metrics quá nhiều (50 metrics, chỉ 6 có signal).
- Không dừng vì: 12 khách hàng vẫn dùng đều đặn, và "decision rubric" tactic khá clear.
- Không tiếp tục as-is vì: adoption dừng lại, không có đường dẫn tới release decision gate usage.

## 2. Chỉ số mạnh nhất để bảo vệ quyết định: Release Decision Usage

**Metric:** Khách hàng dùng TrustLayerAI metrics để gate RAG releases.  
**Hiện tại:** 5/60 (8%)  
**Mục tiêu:** 20/60 (33%) theo tháng 6 (cuối phase 3)  

**Tại sao mạnh nhất:**
- Đo đúng adoption outcome (không activation vanity).
- Kỳ vọng kinh doanh: nếu khách hàng không dùng TL để quyết định releases, ROI = 0.
- Gắn với 2 root causes: (a) workflow gate, (b) metrics clarity.

**Decision rule:** Nếu cuối tháng 4, release decision adoption <15%, escalate CEO/kill decision.

## 3. Chỉ số/giả định sửa sau phản biện (v1 → v2)

**Sửa đổi 1:** Quy trình 3, "Decision accuracy" metric.  
- V1: "Chưa có baseline" → V2: "Chạy 3 retrospectives trước scaling (metrics-prod validation)."  
- Tại sao: Không thể gate releases mà không chứng minh gate hoạt động.

**Sửa đổi 2:** Quy trình 1, "Thời gian-đến-eval-đầu tiên" chia nhỏ.  
- V1: 14 ngày (tổng) → V2: (a) thời gian-import + (b) thời gian-tạo-dataset + (c) thời gian-eval.  
- Tại sao: Cô lập bottleneck (customer data prep vs. TrustLayerAI performance).

**Sửa đổi 3:** Quy trình 4, "Engagement" enforcement.  
- V1: "0/2 khách hàng xem metrics weekly" (passive) → V2: Mandate customer org gán on-call owner trong tuần 1. Nếu từ chối, không deploy.  
- Tại sao: Reinforcement không xảy ra nếu không có accountability.

## 4. Trước khi scale (phase 4+), nhóm phải:

1. **Validate decision rubric trong 2-3 customer pilots (tuần 8-12).**  
   - Chạy 3 retrospective case studies: khi TL metrics nói release/hold, prod reality là gì?  
   - Nếu prod-dev agreement <75%, adjust rubric hoặc flag new root cause (ví dụ: embedding model drift trong prod).  
   - Nếu agreement >85%, sẵn sàng scale gate.

2. **Giảm metric clutter: hủy 40 metrics, giữ 8-10 core (tuần 4-6).**  
   - Core set: retrieval precision, latency, F1, coverage, false positive rate, escalation rate, + 2 business metrics (time-to-value, cost saved).  
   - Chạy customer survey: "metrics nào trong 8 này sẽ thay đổi release decision của bạn?"  
   - Chỉ giữ metrics ảnh hưởng quyết định.

3. **Document 1 production monitoring SOP trước bất kỳ khách hàng nào go live (tuần 12+).**  
   - Scenario 1: prod metric giảm 10% day-over-day. Response: escalate + investigate.  
   - Scenario 2: prod-dev metric disagreement detected. Response: chạy validation playbook.  
   - Scenario 3: khách hàng báo cáo prod quality issue. Response: 30-day post-launch review.  
   - Không SOP = alert fatigue = khách hàng ignore monitoring.

4. **Gán dedicated owner (person + budget) cho "Release Decision Gate" feature (tháng 1).**  
   - Hiện tại: không có owner. Tactic "Metric Review Ceremony" sẽ fail mà không executive sponsorship.  
   - Owner: chịu trách nhiệm customer alignment (survey), rubric maintenance, release decision escalations.
```

---

## 10. Nhật Ký Dùng AI (Nhật Ký Hỗ Trợ AI)

Điền nếu nhóm dùng AI sau phần làm cá nhân ban đầu.

| AI đã giúp gì? | AI trả lời sai / chung chung ở đâu? | Nhóm đã sửa bằng tay như thế nào? |
|---|---|---|
| (1) Brainstorm core workflows cho TrustLayerAI — AI đề xuất 5 workflows, nhóm chọn 4 hợp lý nhất. | AI liệt kê "deploy model," "monitor performance," "retrain" — quá generic, không gắn "evaluation + decision." | Nhóm reframed: evaluation là quy trình chính; output dùng để *quyết định* release, không chỉ validating chất lượng. |
| (2) Tạo example metrics tables — AI tạo skeleton với generic metrics (MAU, DAU, engagement). | AI mặc định product metrics, không biết TrustLayerAI là B2B evaluation tool. Metrics phải gắn "trust + decision," không chỉ usage. | Nhóm thêm các lớp Quality / Trust / Value; thay DAU bằng "release decision dùng metrics." |
| (3) Draft decision memo — AI viết formal memo structure. | AI generic, không capture Klarna lesson cụ thể (dev evals ≠ prod reality). | Nhóm thêm: "Validate decision rubric trong customer pilots trước scaling." Hành động cụ thể từ red-team risk. |

---

## 11. Checklist Trước Khi Nộp

- [x] Có challenge rõ: "TrustLayerAI adoption cliff—75% activation → 20% retention."
- [x] Có 1 sản phẩm cụ thể: TrustLayerAI (B2B evaluation platform cho RAG/search).
- [x] Có 2-4 quy trình chính: 4 workflows (Setup, Eval, Release Decision, Prod Monitoring).
- [x] Có 1-2 nguyên nhân gốc với bằng chứng: (1) Workflow gate missing, (2) Metrics overload (50 → 6 signal).
- [x] Có lộ trình 30/60/90 ngày, có người phụ trách: Phase 0-3 với PM, Search Lead, Data Eng gán.
- [x] Dashboard có chỉ số toàn sản phẩm + per-workflow: 3 product metrics + 6 layers × 4 workflows = 27 metrics.
- [x] Không chỉ đo usage: activation + retention + productivity + quality + trust + value layers.
- [x] Có nguồn dữ liệu + người phụ trách: mỗi metric có data source + owner.
- [x] Có rủi ro red-team + ≥2 sửa từ v1 → v2: 3 rủi ro nêu, 3 sửa implement (rubric validation, metric split, on-call mandate).
- [x] Memo quyết định rõ: PIVOT (không kill, không continue as-is). Release decision adoption = north star.

---



