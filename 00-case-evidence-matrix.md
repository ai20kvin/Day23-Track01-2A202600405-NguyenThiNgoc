# Mẫu 00 — Bảng So Sánh Case Thành Công / Thất Bại

Mục tiêu của bài này: đọc case thật để biết chỉ số nào chứng minh được giá trị (value), chỉ số nào chỉ tạo cảm giác tốt.

## Chọn Case

| Nhóm case | Gợi ý |
|---|---|
| Thành công / tín hiệu tốt | Morgan Stanley, DWP/GDS, Stripe, Nansen |
| Thất bại / cảnh báo | Klarna, IBM Watson / MD Anderson, KPMG dashboard, JPMorgan dashboard |

## Bảng Điền

| Trường | Case thành công | Case thất bại/cảnh báo |
|---|---|---|
| Case | Morgan Stanley: Trợ lý AI cho Tư vấn viên Tài chính | JPMorgan Chase: Dashboard Giám sát Nhân viên (WCOE) |
| AI được dùng trong quy trình nào? | Truy xuất và tóm tắt tri thức từ 100k+ báo cáo nghiên cứu nội bộ (RAG). | Giám sát hành vi và năng suất lao động của nhân viên. |
| Người dùng chính là ai? | Tư vấn viên tài chính (Financial Advisors - FA). | Quản lý ngân hàng và nhân viên. |
| Họ đo chỉ số gì? | Thời gian tiết kiệm được; Độ chính xác trích xuất nguồn (Retrieval Accuracy). | Thời gian có mặt tại văn phòng; Số lượng email/cuộc gọi/dòng code. |
| Chỉ số đó thuộc lớp nào? | Productivity / Quality | Activation / Engagement |
| Chỉ số đó chứng minh được gì? | Khả năng tìm kiếm tri thức cực nhanh, hỗ trợ FA ra quyết định nhanh hơn. | Sự hiện diện vật lý và khối lượng công việc thô được thực hiện. |
| Chỉ số đó chưa chứng minh được gì? | Hiệu suất thực tế của danh mục đầu tư khách hàng. | Hiệu suất thực tế, chất lượng công việc hay giá trị kinh tế thực sự. |
| Thiếu chỉ số nào? | Chất lượng tư vấn cuối cùng của con người sau khi có AI. | Chất lượng ý tưởng, sự sáng tạo và mức độ hài lòng của nhân viên. |
| Rủi ro lớn nhất | FA quá tin tưởng vào AI (Over-reliance) mà bỏ qua bước kiểm chứng. | Nhân viên đối phó (Gaming), mất niềm tin văn hóa và gây kiệt sức (Burnout). |
| Bài học cho dashboard nhóm | AI nên đóng vai trò "thủ thư" hỗ trợ, con người là trung tâm kiểm chứng. | Metric sai lệch dẫn đến hành vi sai lệch; đừng đo "nỗ lực ảo" thay vì "giá trị thật". |

## Câu Chốt Của Nhóm

```markdown
Case thành công dạy nhóm tôi rằng:
Công cụ tốt nhất là công cụ giúp con người làm việc thông minh hơn (Empowerment) bằng cách tối ưu hóa truy cập tri thức, nhưng cần duy trì quy trình kiểm chứng thủ công.

Case thất bại/cảnh báo dạy nhóm tôi rằng:
Việc tập trung vào các chỉ số giám sát bề nổi (Monitoring) sẽ phản tác dụng, dẫn đến việc nhân viên tìm cách "đối phó" hệ thống thay vì tập trung vào chất lượng.

Vì vậy dashboard nhóm tôi phải tránh:
Sử dụng các chỉ số thuần túy về số lượng (v.d: số prompt, thời gian sử dụng) làm thước đo duy nhất mà thiếu đi các lớp đo về Quality, Trust và Value.
```

## Tự kiểm tra

- [ ] Không chỉ kể chuyện case.
- [ ] Có nêu chỉ số cụ thể.
- [ ] Có nói chỉ số chứng minh được gì và không chứng minh được gì.
- [ ] Có ít nhất 1 bài học áp dụng vào dashboard nhóm.
