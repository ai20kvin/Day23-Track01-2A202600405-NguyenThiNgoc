# Day 23 — Reflect cá nhân (150–200 từ)

**Học viên:** Nguyễn Thị Ngọc — **Mã:** 2A202600405

---

## Prompt: “1 chỉ số hoặc 1 giả định tôi sẽ sửa + tại sao”

Chỉ số tôi chọn để thay là **“% khách kích hoạt bằng cách chạy evaluation ít nhất một lần trong tháng đầu”** (activation kiểu vanity). Nó dễ tạo ảo giác adopt vì chỉ chứng minh người ta “thử một phát”, không chứng minh TrustLayerAI đi vào **quyết định release** hay giảm rủi ro thật. Cơ chế cheat: team có thể chạy eval hình thức để đạt KPI mà không đổi workflow. Tôi sẽ thay bằng **“% release gate có báo cáo TrustLayerAI + kết quả 30 ngày sau release (issue rate)”** — gắn outcome và audit trail. Case **JPMorgan WADU** nhắc rằng khi thước đo là tín hiệu nỗ lực bề mặt, con người tối ưu “trông bận” chứ không tối ưu giá trị; case **Morgan Stanley** thì ngược lại: cần đi từ productivity sang **trust/quality** nếu không muốn over-rely. Sau vòng red-team, tôi càng tin cần thêm **điều kiện tiên quyết** (ví dụ % khách đồng ý rubric trong 4 tuần đầu và 3 retrospective dev–prod) trước khi coi gate release là “đã adopt”. Với nhóm, đổi chỉ số này giúp dashboard không thưởng cho hành vi “chạy eval cho có”.
