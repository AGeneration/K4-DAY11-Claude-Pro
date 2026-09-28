# Rework cuối — đã import và export lại qua CVAT

File nộp: [B2-dense-rework-cvat-export.zip](B2-dense-rework-cvat-export.zip). XML trích nguyên bytes: [annotations-v2.xml](annotations-v2.xml). Mã khóa hiện tại: **823C-842B**.

Đã thực hiện trên CVAT local 2.75.1: sao lưu nhãn job30 → xác minh bản cũ khớp export job30 gốc → import bản sửa vào task47 → chờ finished → đọc nhãn đã lưu trên server → export CVAT for images 1.1, không kèm ảnh → tải ZIP và kiểm toàn bộ hình/thuộc tính → relock. Thao tác qua API của CVAT bằng phiên server tạm, không mô tả là bấm Ctrl+S trên giao diện.

Ba ảnh: 062370 (8 box), 069450 (5 box), 117120 (8 box); mỗi ảnh có 3 polygon. Tổng 21 box, 9 polygon. Tất cả geometry/class/attributes/group khớp bản sửa có căn cứ trước import.

Thay đổi: đổi van thành Car, siết Bike, thêm Truck bị che ở 062370; bỏ Car dưới 40 px ở 069450; sửa Car vẽ thiếu và bỏ hai Car nhỏ ở 117120. Giữ ca Bus/ThreeWheeler đang escalation. Delta matched 15→19, missing 5→1, spurious 4→2.

Bằng chứng: [cvat_roundtrip.json](cvat_roundtrip.json), [provenance.json](provenance.json), [delta.md](delta.md), [overlay](rework_overlay.html). R1 E4B2-125A giữ nguyên. ZIP import 00BC-F291 và local_proposal_provenance.json là lịch sử trước export, không phải mã nộp hiện tại.

Không cần import lại gói này: CVAT job30 đã có nhãn sửa. Các escalation về chất lượng vẫn chờ người nhận phân xử; lock chứng minh tính toàn vẹn, không thay phê duyệt QA.

CVAT đổi metadata `source` thành `file` khi import nên lock mới ghi `prefill_kept=21`. Đây là dấu vết import, không chứng minh 21 box được giữ nguyên từ prefill đầu bài. So sánh đã kiểm geometry/class/attributes/group; lịch sử thao tác và bản trước import vẫn được giữ. Hash XML thay đổi theo export CVAT dù nội dung nhãn sửa tương đương.
