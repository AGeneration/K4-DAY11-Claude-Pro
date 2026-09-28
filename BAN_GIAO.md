# Bàn giao Day11 — Nguyễn Lê Thế Anh

Đã hoàn tất vòng import/export rework trên CVAT local, job30/task47: **Day11 · ADASIND · B2-dense · raw_fisheye**. Đủ ba ảnh 062370, 069450, 117120.

- R1 nguyên export job30: **E4B2-125A**, giữ nguyên làm đối chứng.
- Rework export mới từ CVAT: **823C-842B**, [tải ZIP](submission/rework/B2-dense-rework-cvat-export.zip). Mã local 00BC-F291 đã được thay thế có ghi lý do relock.
- 48 findings, 10 ảnh bằng chứng, error card, năm ticket, sampling 8 ô tổng 200 frame, gold plan bốn camera, exit ticket.
- Peer QA: Anh review Duy B4-center tại commit 79fdaac, R1 34BC-63D5 và đối chiếu rework FA15-D3EC; [review](submission/r2_qa/qa_review.md).
- Baseline: TP15/FP4/FN5, precision 0.789, recall 0.750, mean IoU 0.843. Delta matched 15→19, missing 5→1, spurious 4→2.

## Kiểm chứng

CVAT import và export đều báo finished. ZIP trước sửa khớp job30 gốc. ZIP sau sửa được đối chiếu toàn bộ hình, geometry, class, attributes và group với bản rework: khớp đủ ba frame. Xem [bằng chứng CVAT](submission/rework/cvat_roundtrip.json) và [hướng dẫn bàn giao rework](submission/rework/README.md). Nhãn đã lưu trên CVAT, không cần bạn tự import/export lại.

`py -3.11 lab11.py triage` và `py -3.11 lab11.py check` kiểm hồ sơ; không thay phê duyệt chất lượng. Các ticket còn tranh luận giữ trạng thái escalation, chưa mạo nhận Duy/Coach đã duyệt. C0 giữ bản khóa cũ và finding đã ghi; B2 rework không sửa C0. K12/stretch đã ghi giảm, không giả lập polygon K12. Ba frame không đại diện hệ bốn camera; kế hoạch 200 frame là giả lập.

Review có trợ lý hỗ trợ. Thao tác CVAT thực hiện qua API server bằng quyền quản trị Docker local, phiên tạm đã đóng; không có mật khẩu/token trong hồ sơ. Tên task raw_fisheye đã được xác minh trực tiếp. Nhánh nộp: NguyenLeTheAnh-2A202602164; cache/profile và file tạm không đưa lên GitHub.
