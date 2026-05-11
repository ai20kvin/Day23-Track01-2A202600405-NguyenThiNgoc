# 📄 Decision Memo – TrustLayerAI (RAG / Enterprise Search)

**Mục tiêu**: Đánh giá quyết định tiếp tục, chỉ số mạnh nhất, thay đổi dự kiến sau red‑team, và các yêu cầu chuẩn bị cho việc mở rộng quy mô.

## 1️⃣ Tiếp tục / Pivot / Kill?
- **Quyết định**: **Tiếp tục**. Sản phẩm đã đạt mục tiêu activation (30 % → 70 %), độ tin cậy (override <15 %), và giá trị kinh tế (cost saved $4k/tháng). Các chỉ số quan trọng đều đang tiến triển ổn định, không có rủi ro nghiêm trọng ngăn cản mở rộng.

## 2️⃣ Chỉ số mạnh nhất & lý do
- **Trust (tỷ lệ override <15 %)** – Người dùng tin tưởng kết quả AI, giảm nhu cầu kiểm tra lại thủ công. Đây là chỉ số phản ánh trực tiếp mức độ chấp nhận và an toàn của hệ thống.

## 3️⃣ Chỉ số sẽ được cải thiện sau red‑team & lý do
- **Precision @10** (độ chính xác của truy vấn) – Hiện tại 78 % → mục tiêu ≥ 85 %.
  - **Lý do**: Red‑team đã chỉ ra các trường hợp AI trả về kết quả không liên quan, gây mất thời gian cho người dùng. Chúng tôi sẽ fine‑tune mô hình với dữ liệu domain‑specific và cải thiện pipeline retrieval.

## 4️⃣ Yêu cầu trước khi scale (mở rộng quy mô)
1. **Pipeline CI/CD cho model**: Tự động hoá việc train, evaluate và deploy mô hình mới với kiểm tra regression.
2. **Giám sát latency**: Đảm bảo thời gian phản hồi < 1 s cho mọi query qua alert.
3. **Quản trị dữ liệu**: Thiết lập quy trình classification & masking để ngăn rò rỉ dữ liệu nhạy cảm khi ingest tài liệu mới.
4. **Governance & Auditing**: Ghi lại log toàn bộ truy vấn, quyết định và annotation để đáp ứng yêu cầu compliance.
5. **Hỗ trợ người dùng**: Tài liệu onboarding, video hướng dẫn và kênh hỗ trợ nội bộ để duy trì awareness và adoption.

---

*Prepared by: Nguyễn Thị Ngọc (2A202600405)*
