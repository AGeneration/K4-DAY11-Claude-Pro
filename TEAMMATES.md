# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: AI20K · K4
- Tên nhóm: Claude-Pro
- Repo Public: https://github.com/AGeneration/K4-DAY11-Claude-Pro
- Máy giữ hồ sơ chính / người quản lý: mỗi thành viên giữ hồ sơ của mình trên branch riêng
  (`vu-minh-duy-2a202602198`, `hoang-cong-tung-2a202602229`, `NguyenLeTheAnh-2A202602164`). Người giữ hồ sơ này:
  Nguyễn Lê Thế Anh. Commit chia task và setup chung: `c2ae9e7` trên `main`.
- Slice chung lấy từ mode.json: nhóm không dùng slice chung. `mode --members anh duy tung` chia mỗi người một slice:
  anh → `B2-dense`, duy → `B4-center`, tung → `B2-mid`. Hồ sơ này là slice `B2-dense`.
- Tên định danh vai A dùng cho --self: `anh` (hồ sơ này); hai bạn còn lại dùng `duy` và `tung`.
- Kênh trao đổi nội bộ: Discord
- Đại diện nộp (vai C): Nguyễn Lê Thế Anh, 2A202602164 (cho hồ sơ này; Duy và Tùng nộp branch của mình)
- Commit chốt bài: `0182dad` (rework qua vòng import/export CVAT, relock `823C-842B`; `lab11.py check` exit 0). Các commit
  sau đó chỉ cập nhật `TEAMMATES.md`.

## 2. Ba vai chính

Nhóm làm theo vòng quay trong [docs/03-roles-rotation-vi.md](docs/03-roles-rotation-vi.md): **mỗi người làm cả ba vai**.
Người đó gán nhãn slice của mình (A), soát mù bản khoá của người kế bên (B), rồi chẩn đoán và hoàn thiện slice của mình (C).
Vòng QA theo [team.json](submission/00_setup/team.json) là **anh → duy → tung → anh**, nghĩa là anh soát duy, duy soát tung, tung soát anh.

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Nguyễn Lê Thế Anh | 2A202602164 | `anh` | Parking, C0 và slice B2-dense; self-QC, lock, rework | Commit `24e2cd6`: C0 khoá `9A6E-6AB2`, B2-dense R1 khoá `E4B2-125A` từ export job30 (relock từ `820E-C320`). Commit `fad2e60`, `0182dad`: rework khoá `823C-842B` sau vòng import/export CVAT ([cvat_roundtrip.json](submission/rework/cvat_roundtrip.json); các mã cũ `79DF-6639`, `00BC-F291` nằm trong history của `lock2.txt`) |
| A · Gán nhãn | Vũ Minh Duy | 2A202602198 | `duy` | Parking, C0 và slice B4-center; self-QC, lock, rework | Trên branch của Duy: `5c12a03` (B4-center khoá `34BC-63D5`), `79fdaac` (rework khoá `FA15-D3EC`) |
| A · Gán nhãn | Hoàng Công Tùng | 2A202602229 | `tung` | Parking, C0 và slice B2-mid; self-QC, lock, rework | Trên branch của Tùng: `c86eea2` (B2-mid khoá `24F8-C550`), `3d42c40` (rework khoá `CF64-2680`) |
| B · QA độc lập | Nguyễn Lê Thế Anh → soát bài Duy | 2A202602164 | `anh` | Soát bản khoá B4-center trước reference, kiểm lại bản rework | Commit `bcdd5ac`: [r2_qa/qa_review.md](submission/r2_qa/qa_review.md) có 4 nhận xét QA-DUY-01…04 trên R1 `34BC-63D5` và đối chiếu rework `FA15-D3EC`, kèm [source_duy/provenance.json](submission/r2_qa/source_duy/provenance.json) (`reviewed_reference_or_model: false`); 4 dòng `r2_qa,B4-center` trong [findings.csv](submission/findings.csv) |
| B · QA độc lập | Hoàng Công Tùng → soát bài Thế Anh | 2A202602229 | `tung` | Soát bản khoá B2-dense | Commit `3d42c40` trên branch của Tùng: `r2_qa/qa_review.md` cho bản khoá `E4B2-125A`, 4 nhận xét (062370 L4 R04; 069450 L6, 117120 L3, 117120 L6 R01) |
| B · QA độc lập | Vũ Minh Duy → soát bài Tùng | 2A202602198 | `duy` | Soát bản khoá B2-mid trước reference | Commit `ff9fa5b` trên branch của Duy: `r2_qa/peer_B2-mid/qa_review.md`, 7 nhận xét QA-TUNG-01…07 |
| C · Chẩn đoán & điều phối | Nguyễn Lê Thế Anh | 2A202602164 | `anh` | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp cho B2-dense | Commit `24e2cd6` (r3_diag, 48 findings, error card, guideline patch, escalation, review/sampling/gold plan, exit ticket), [40_decision_log.csv](submission/40_decision_log.csv) (REC, JOB30, DIAG, PEER, CVAT…), [BAN_GIAO.md](BAN_GIAO.md) |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI. Nhóm dùng đúng vòng đó:
mỗi người một slice và một hồ sơ, rồi QA chéo theo vòng.

## 3. Bàn giao theo pha

Các mốc dưới đây ghi theo hồ sơ B2-dense của Thế Anh. Mốc nào có trao đổi chéo thì ghi thêm luồng giữa các thành viên.

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | (chung) Duy → Tùng, Thế Anh | `c2ae9e7` trên `main`: `mode.json`, `team.json`, `doctor.txt` | Cả ba chạy `mode` với cùng danh sách `anh duy tung`. `qa_reviews` trong team.json của ba branch trùng nhau | Xong |
| P1 · C0 calib | Thế Anh tự khoá | `24e2cd6`: `p1_calib/`, mã `9A6E-6AB2` | Selfqc báo thiếu `ego_body` và L9 dưới 40 px; ghi lỗi, giữ nguyên bản khoá (CAL-02). Ca rider C0 L8 escalate (CAL-01) | Xong, còn escalation |
| P2 · Khóa bản đầu (slice B2-dense) | Thế Anh tự khoá | `24e2cd6`: `r1_craft/`, mã `E4B2-125A` (relock từ `820E-C320` khi có export job30 đủ ba ảnh, JOB30-01) | Tự đối chiếu checklist self-QC ([selfqc.md](submission/r1_craft/selfqc.md)) | Xong |
| P2 · Khóa bản đầu (bài Thế Anh) → Tùng (QA) | Thế Anh → Tùng | Branch `NguyenLeTheAnh-2A202602164`, mã `E4B2-125A` | Tùng soát trên bản khoá `E4B2-125A` | Xong |
| P3 · Chốt QA mù (Thế Anh soát Duy) | Thế Anh → Duy | `bcdd5ac`: QA-DUY-01…04, ảnh `screenshots/duy-*.png`, R1 `34BC-63D5` tại commit `79fdaac` của Duy | Kiểm sha256 R1 `34BC-63D5` và rework `FA15-D3EC` khớp lock của Duy (PEER-02); ghi nhận xét R1 trước, đối chiếu rework sau | Xong. QA-DUY-02/03/04 escalate (PEER-03), QA-DUY-01 đề nghị Duy sửa (PEER-04) |
| P3 · Chốt QA mù (bài Thế Anh) | Tùng → Thế Anh | `3d42c40` trên branch Tùng: `r2_qa/qa_review.md`, mã khoá `E4B2-125A` | Thế Anh xử lý cả 4 nhận xét trong rework: 062370 L4 đổi Car (REC-02); 069450 L6, 117120 L3, L6 dưới H40 bị bỏ | Xong |
| P4 · Quyết định sửa | Thế Anh (vai C) → chính Thế Anh (vai A) | `24e2cd6`, `findings.csv` round `r3_diag`, decision log DIAG-01/02, JOB30-03 | Mỗi khác biệt với reference/model có WHAT/WHY/owner. Reference nghi trùng R5/R7 và lệch taxonomy của model được escalate chứ không ép nhãn theo reference | Xong |
| P5 · Kiểm bản sửa | Thế Anh tự rework, kiểm qua CVAT | `rework/annotations-v2.xml`, `lock2.txt` mã `823C-842B` (relock từ `00BC-F291`), [delta.md](submission/rework/delta.md), [cvat_roundtrip.json](submission/rework/cvat_roundtrip.json) | Import/export CVAT (job30/task47) đều finished; so sánh toàn bộ hình, class, thuộc tính, group khớp bản sửa. Matched 15→19, missing 5→1, spurious 4→2 | Xong (CVAT-01) |
| P6 · Chốt nộp | Thế Anh (A, C) | [manifest.json](submission/manifest.json), commit `0182dad` | `lab11.py check` exit 0 ("Hồ sơ hình thức đầy đủ"); `manifest.json` có `failed_gates: []` | Xong |

## 4. Bất đồng và phối hợp

- **Một ca đã phân xử:** `adasind_062370.jpg` L4, R04. Bản R1 gán `Truck` cho chiếc xe đỗ trước cửa hàng; Tùng (QA) nêu
  đây là van chở người. Thế Anh soi ảnh, xác nhận van chở người nên theo R04 phải là `Car`, và sửa trong rework `823C-842B`
  (REC-02; [screenshots/03-b2-van.png](submission/screenshots/03-b2-van.png)).
- **Việc tiếp theo:**
  - Ticket 1 (DIAG-01): reference nghi trùng R5/R7 ở 062370. Owner: qa và người giữ reference. Đang chờ phân xử.
  - Ticket 2 (DIAG-02): model gọi ThreeWheeler là Truck và tách rider thành Pedestrian. Owner: ai_team. Đang chờ phản hồi.
  - JOB30-03: 117120 L3/L7 bị báo spurious nhưng có vật thật, giữ nhãn và chờ QA phân xử class/reference.
  - C0: CAL-01 (rider hay người dắt xe ở L8) đang escalate; CAL-02 (thiếu `ego_body`, L9 dưới ngưỡng) đã ghi, giữ bản khoá.
  - QA cho Duy: QA-DUY-02/03/04 đang escalate (PEER-03); QA-DUY-01 chờ Duy đồng bộ `truncated` của polygon (PEER-04).
    Người theo dõi: Duy.
- **Đóng góp của A/B/C vào kế hoạch và exit ticket:** mỗi thành viên tự viết error card, guideline patch, escalation,
  review/sampling/gold plan và exit ticket cho slice của mình. Thế Anh làm cho B2-dense (`24e2cd6`: sampling 8 ô tổng
  200 frame, gold plan bốn camera, 5 ticket). Duy làm cho B4-center (`8237106`). Tùng làm cho B2-mid (`c86eea2`, `3d42c40`).
- **Thay đổi phân công nếu có:** không đổi người hay vai. Ở P3, Thế Anh chưa nhận được bản khoá của Duy sau hơn 5 phút
  nên cold review bài mình trước (QA-01, lưu ở `r2_qa/previous_self_review.md`). Khi Duy push commit `79fdaac`, Thế Anh
  thay bằng peer QA bài Duy đúng theo team.json (PEER-01, PEER-02).

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Nguyễn Lê Thế Anh. sha256 của `r1_craft/annotations.xml` và
  `rework/annotations-v2.xml` tại HEAD khớp `lock.txt` (`E4B2-125A`) và `lock2.txt` (`823C-842B`); C0 khớp `9A6E-6AB2`.
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Hoàng Công Tùng soát bản khoá `E4B2-125A`
  (`3d42c40`); rework `823C-842B` đã xử lý cả 4 nhận xét.
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Nguyễn Lê Thế Anh. `lab11.py check` →
  "Hồ sơ hình thức đầy đủ" (exit 0).
- [x] manifest.json tại commit chốt có failed_gates rỗng (`failed_gates: []`).
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
