# Mẫu 03 — Dashboard Mock (TrustLayerAI)

**Mô tả nhanh**: Mock dashboard 6 ô thể hiện trạng thái sức khỏe sản phẩm và các quy trình chính của TrustLayerAI (RAG / Enterprise Search).

## Quy Tắc
- Ô đầu tiên: tổng quan sức khỏe toàn sản phẩm.
- Các ô tiếp theo: tín hiệu theo từng workflow (Search, Summarize, Recommend, Knowledge Update) và một ô tổng hợp Trust / Quality.
- Mỗi ô hiển thị: metric, giá trị hiện tại, mục tiêu, trạng thái (GREEN/AMBER/RED), hành động khi màu đỏ.
- Không quá 6 ô.

## Khung 6 Ô (ASCII Mock)

```text
┌─────────────────────────────────────────────┐   ┌─────────────────────────────────────────────┐
│ TILE 1: PRODUCT HEALTH                      │   │ TILE 2: SEARCH WORKFLOW                     │
│ Metric: Activation Rate                     │   │ Metric: % Successful Queries               │
│ Current: 30%                               │   │ Current: 92%                               │
│ Target: 70%                                 │   │ Target: 98%                                 │
│ Status: AMBER                               │   │ Status: GREEN                               │
│ Action if RED: Tăng onboarding, videos      │   │ Action if RED: Tối ưu cache, fallback       │
└─────────────────────────────────────────────┘   └─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐   ┌─────────────────────────────────────────────┐
│ TILE 3: SUMMARIZE WORKFLOW                  │   │ TILE 4: RECOMMEND WORKFLOW                 │
│ Metric: Avg Summary Length (words)          │   │ Metric: Click‑Through Rate                  │
│ Current: 120                                │   │ Current: 12%                               │
│ Target: 150                                 │   │ Target: 20%                                 │
│ Status: AMBER                               │   │ Status: AMBER                               │
│ Action if RED: Tối ưu prompt, thêm guide    │   │ Action if RED: UI redesign, add trust overlay│
└─────────────────────────────────────────────┘   └─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐   ┌─────────────────────────────────────────────┐
│ TILE 5: KNOWLEDGE UPDATE WORKFLOW           │   │ TILE 6: TRUST / QUALITY                     │
│ Metric: Override Rate (human review)        │   │ Metric: Trust Score (CSAT)                  │
│ Current: 25%                                 │   │ Current: 3.8/5                              │
│ Target: <15%                                 │   │ Target: ≥4.5/5                              │
│ Status: RED                                  │   │ Status: AMBER                               │
│ Action if RED: Thêm confidence score, alert│   │ Action if RED: Add explainability overlay   │
└─────────────────────────────────────────────┘   └─────────────────────────────────────────────┘
```

*Ghi chú*: Các giá trị hiện tại và mục tiêu được lấy từ phần B của Product ROI Dashboard. Trạng thái được tính dựa trên khoảng cách giữa hiện tại và mục tiêu (GREEN ≤ 80% mục tiêu, AMBER 80‑95%, RED >95%).


Vẽ nhanh 4-6 ô để người đọc thấy dashboard sẽ dùng như thế nào. Không cần high-fidelity.

## Quy Tắc

- Ô đầu tiên: tình trạng toàn sản phẩm.
- Các ô tiếp theo: tín hiệu theo quy trình, trust/quality/value, hoặc quyết định.
- Mỗi ô có số hiện tại, mục tiêu, trạng thái, hành động nếu đỏ.
- Không vẽ quá 6 ô.

## Khung 6 Ô

```text
┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 1: PRODUCT HEALTH             │ │ TILE 2: WORKFLOW 1                 │
│ Metric: __________________________ │ │ Metric: __________________________ │
│ Current: ______ Target: _________  │ │ Current: ______ Target: _________  │
│ Status: GREEN / AMBER / RED        │ │ Status: GREEN / AMBER / RED        │
│ Action if red: ___________________ │ │ Action if red: ___________________ │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 3: WORKFLOW 2                 │ │ TILE 4: TRUST / QUALITY            │
│ Metric: __________________________ │ │ Metric: __________________________ │
│ Current: ______ Target: _________  │ │ Current: ______ Target: _________  │
│ Status: GREEN / AMBER / RED        │ │ Status: GREEN / AMBER / RED        │
│ Action if red: ___________________ │ │ Action if red: ___________________ │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 5: VALUE / COVERAGE           │ │ TILE 6: DECISION                   │
│ Metric: __________________________ │ │ Continue / Pivot / Kill: _________ │
│ Current: ______ Target: _________  │ │ Metric mạnh nhất: ________________ │
│ Status: GREEN / AMBER / RED        │ │ Before scale: ____________________ │
│ Action if red: ___________________ │ │ Người phụ trách: _________________ │
└────────────────────────────────────┘ └────────────────────────────────────┘
```

## Tự kiểm tra

- [ ] Có 4-6 ô.
- [ ] Ô đầu là toàn sản phẩm.
- [ ] Có ít nhất 1 ô Quality hoặc Trust.
- [ ] Có ô Decision.
- [ ] Mỗi ô có action nếu đỏ.
