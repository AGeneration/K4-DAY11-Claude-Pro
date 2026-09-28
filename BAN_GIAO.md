# Bàn giao job30 — Nguyễn Lê Thế Anh

Hồ sơ dùng **đủ ba ảnh B2-dense** từ ZIP job30: 062370, 069450, 117120. Đã bỏ giảm frame3; chỉ giữ giảm stretch/k12 vì export không có polygon K12. Bản hai ảnh cũ đã được thay thế.

- R1 **E4B2-125A**: nguyên annotations.xml của ZIP người học, kiểm hash trong submission/00_setup/export_provenance.json.
- 48 dòng findings qua các pha, QA review, compare/local-quality/model/IoU, error card, năm ticket, sampling đủ 200, gold plan và exit ticket; mười ảnh chụp overlay làm bằng chứng.
- Baseline L/R: **TP=15, FP=4, FN=5**, precision 0.789, recall 0.750, mean IoU 0.843. Đây là độ khớp teaching reference, không phải điểm rubric.
- Rework **00BC-F291**: bản sửa đề xuất tại máy. Delta matched **15→19**, missing **5→1**, spurious **4→2**. Giữ các ca nghi reference thiếu/trùng hoặc chưa rõ class, không sửa để đạt 100%.

## Phần cần xác nhận trước khi coi là hoàn tất thao tác CVAT

Import `submission/rework/annotations-v2.xml` vào đúng task ba ảnh, kiểm các thay đổi trên ảnh, Save và export lại CVAT for images 1.1. Bản rework hiện **chưa có vòng export CVAT mới được xác minh**; provenance.json khai báo rõ. Sau khi có ZIP mới phải ghi quyết định, relock rework, cập nhật mã/provenance và chạy lại delta/check.

Tên task raw_fisheye chưa xác minh từ metadata job. Peer QA đã cập nhật đúng Anh review Duy, B4-center, commit 79fdaac: R1 34BC-63D5 và đối chiếu rework FA15-D3EC. Review có trợ lý hỗ trợ, chưa có phản hồi phê duyệt của Duy; lịch sử tự review B2 được giữ riêng. Escalation là ticket trong hồ sơ, chưa được người nhận phê duyệt. C0 giữ bản khóa cũ và các lỗi đã ghi, không nhận là được sửa trong rework B2.

## Kiểm hồ sơ

```powershell
$env:PYTHONUTF8='1'
py -3.11 lab11.py triage
py -3.11 lab11.py check
```

Check chỉ xác nhận hình thức/độ đầy đủ, không thay review chất lượng hay các bước CVAT ở trên. Ba frame một camera không đại diện hệ bốn camera; kế hoạch 200 frame là giả lập.

Nhánh đích: `NguyenLeTheAnh-2A202602164` trong `AGeneration/K4-DAY11-Claude-Pro`. Chỉ bàn giao hồ sơ và bằng chứng cần thiết; profile trình duyệt, cache, bản sao local, ZIP trung gian và lịch sử bài hai ảnh không đưa lên Git.

Chi tiết review Duy: [submission/r2_qa/qa_review.md](submission/r2_qa/qa_review.md). Bốn finding QA của Duy thay bốn dòng tự review B2 cũ; tổng vẫn 48 dòng. R1/rework của Anh và số đo B2 giữ nguyên. Lấy dữ liệu GitHub không thay cho vòng import/export CVAT còn thiếu của bản rework Anh.
