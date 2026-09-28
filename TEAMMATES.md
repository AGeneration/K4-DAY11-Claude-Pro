# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: AI20K · K4
- Tên nhóm: Claude-Pro
- Repo Public: https://github.com/AGeneration/K4-DAY11-Claude-Pro
- Máy giữ hồ sơ chính / người quản lý: mỗi thành viên giữ hồ sơ của mình trên branch riêng
  (`vu-minh-duy-2a202602198`, `hoang-cong-tung-2a202602229`, `NguyenLeTheAnh-2A202602164`). Người giữ hồ sơ này:
  Hoàng Công Tùng. Commit chia task và setup chung: `c2ae9e7` trên `main`.
- Slice chung lấy từ mode.json: nhóm không dùng slice chung. `mode --members anh duy tung` chia mỗi người một slice:
  anh → `B2-dense`, duy → `B4-center`, tung → `B2-mid`. Hồ sơ này là slice `B2-mid`.
- Tên định danh vai A dùng cho --self: `tung` (hồ sơ này); hai bạn còn lại dùng `duy` và `anh`.
- Kênh trao đổi nội bộ: Discord, kênh `lab_day11`
- Đại diện nộp (vai C): Hoàng Công Tùng, 2A202602229 (cho hồ sơ này; Duy và Thế Anh nộp branch của mình)
- Commit chốt bài: `3d42c40` (hoàn thành P3–P6, `python3 lab11.py check` exit 0 — "Hồ sơ hình thức đầy đủ"); HEAD
  hiện tại `7731d43` gồm thêm các commit cập nhật `TEAMMATES.md`, không ảnh hưởng kết quả `check`

## 2. Ba vai chính

Nhóm làm theo vòng quay trong [docs/03-roles-rotation-vi.md](docs/03-roles-rotation-vi.md): **mỗi người làm cả ba vai**.
Người đó gán nhãn slice của mình (A), soát mù bản khoá của người kế bên (B), rồi chẩn đoán và hoàn thiện slice của mình (C).
Vòng QA theo [team.json](submission/00_setup/team.json) là **anh → duy → tung → anh**, nghĩa là anh soát duy, duy soát tung, tung soát anh.

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Vũ Minh Duy | 2A202602198 | `duy` | Parking, C0 và slice B4-center; self-QC, lock, rework | Commit `3681d0b` (P0), `bf1a4d2` (C0, mã `A744-7D43`), `5c12a03` (B4-center khoá `34BC-63D5`), `f6ae329`/`79fdaac` (rework khoá `FA15-D3EC`) |
| A · Gán nhãn | Hoàng Công Tùng | 2A202602229 | `tung` | Parking, C0 và slice B2-mid; self-QC, lock, rework | Commit `c86eea2` trên branch của Tùng: C0 `ACE4-486E`, B2-mid khoá `24F8-C550`, 3 finding calib. Commit `3d42c40`: rework khoá `CF64-2680` (relock từ `6D7B-BC3A`), decision log D01–D04 |
| A · Gán nhãn | Nguyễn Lê Thế Anh | 2A202602164 | `anh` | Parking, C0 và slice B2-dense; self-QC, lock, rework | Commit `24e2cd6`, `fad2e60` và `0182dad` trên branch của Thế Anh: B2-dense khoá `E4B2-125A`, rework khoá `823C-842B` sau vòng import/export CVAT (`cvat_roundtrip.json`; các mã cũ `79DF-6639`, `00BC-F291` nằm trong history) |
| B · QA độc lập | Vũ Minh Duy → soát bài Tùng | 2A202602198 | `duy` | Soát bản khoá B2-mid trước reference, ghi finding QA | Cold review bản của mình ([qa_review.md](submission/r2_qa/qa_review.md), D3). Peer QA B2-mid đang thực hiện: soát bản khoá `24F8-C550`, ghi vào `submission/r2_qa/peer_B2-mid/` và các dòng `r2_qa,B2-mid` trong [findings.csv](submission/findings.csv) |
| B · QA độc lập | Nguyễn Lê Thế Anh → soát bài Duy | 2A202602164 | `anh` | Soát bản khoá B4-center trước reference, kiểm lại bản rework | Commit `bcdd5ac` trên branch của Thế Anh: `submission/r2_qa/qa_review.md` có 4 nhận xét QA-DUY-01…04 và đối chiếu rework `FA15-D3EC`, kèm `source_duy/provenance.json` |
| B · QA độc lập | Hoàng Công Tùng → soát bài Thế Anh | 2A202602229 | `tung` | Soát bản khoá B2-dense | Commit `3d42c40` trên branch của Tùng: `submission/r2_qa/qa_review.md` cho bản khoá `E4B2-125A`, 4 nhận xét (062370 L4 R04; 069450 L6, 117120 L3, 117120 L6 R01), 4 dòng `r2_qa,B2-dense` trong findings.csv |
| C · Chẩn đoán & điều phối | Vũ Minh Duy | 2A202602198 | `duy` | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp cho B4-center | Commit `c062c84` (P4: zone table, local quality, model), `8237106` (P6: error card, guideline patch, escalation, kế hoạch, exit ticket), [40_decision_log.csv](submission/40_decision_log.csv) D1–D12 |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI. Nhóm dùng đúng vòng đó:
mỗi người một slice và một hồ sơ, rồi QA chéo theo vòng.

## 3. Bàn giao theo pha

Các mốc dưới đây ghi theo hồ sơ B2-mid của Tùng. Mốc nào có trao đổi chéo thì ghi thêm luồng giữa các thành viên.

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | (chung) Duy → Tùng, Thế Anh | `c2ae9e7` trên `main`: `mode.json`, `team.json`, `doctor.txt` | Cả ba chạy `mode` với cùng danh sách `anh duy tung`. `assignments` và `qa_reviews` trong mode.json/team.json của ba branch trùng nhau | Xong |
| P2 · Khóa bản đầu (slice B2-mid) | Tùng tự khoá | `c86eea2`: `submission/r1_craft/`, mã `24F8-C550` | Tự đối chiếu đủ 9 mục checklist self-QC trước khi khoá ([selfqc.md](submission/r1_craft/selfqc.md)) | Xong |
| P2 · Khóa bản đầu (bài Tùng) → Duy (QA) | Tùng → Duy | Branch `hoang-cong-tung-2a202602229`, `c86eea2`, mã `24F8-C550` | Duy kiểm `git show …:r1_craft/annotations.xml` ra sha256 `24f8c550…621354`, khớp `lock.txt` | Xong (Duy tự xác nhận phía hồ sơ của Duy) |
| P3 · Chốt QA mù (Tùng soát Thế Anh) | Tùng → Thế Anh | `3d42c40`: `r2_qa/qa_review.md`, mã khoá đã soát `E4B2-125A` | 4 nhận xét theo rule (062370 L4 R04; 069450 L6, 117120 L3, 117120 L6 R01). Thế Anh đã rework đúng cả 4 điểm, khoá `823C-842B` | Xong |
| P3 · Chốt QA mù (bài Tùng) | Duy → Tùng | `submission/r2_qa/peer_B2-mid/` | Chưa có trên branch Duy tính đến lúc kiểm tra gần nhất | **Đang chờ Duy thực hiện** |
| P4 · Quyết định sửa | Tùng (vai C) → chính Tùng (vai A) | `3d42c40`, `findings.csv` round `r3_diag`, 46 dòng điền đủ why/severity/owner/action | Mỗi khác biệt với reference/model đều có WHAT/WHY/owner. 1 cụm bỏ sót được escalate vì luật chưa rõ (D02); 1 ca reference sai giữ nguyên nhãn của mình, không sửa theo reference (D04) | Xong |
| P5 · Kiểm bản sửa | Tùng tự rework, tự đối chiếu delta | `rework/annotations-v2.xml`, `lock2.txt` mã `CF64-2680` (relock từ `6D7B-BC3A`), [delta.md](submission/rework/delta.md) | Missing giảm từ 6 ca về 1 ca (zone center 3→0, mid 3→0); bản đầu tiên (`6D7B-BC3A`) chỉ sửa đúng 2/6 và làm lệch 1 class, đã ghi lý do relock ở D01 | Xong |
| P6 · Chốt nộp | Tùng (A, B, C) | [manifest.json](submission/manifest.json), commit `3d42c40` | `lab11.py check` exit 0 ("Hồ sơ hình thức đầy đủ"); `manifest.json` có `failed_gates: []` | Xong |

## 4. Bất đồng và phối hợp

- **Một ca đã phân xử:** `adasind_102750.jpg`, vật ở vị trí reference gọi là `R4` (`ThreeWheeler`; gợi ý K12 của
  công cụ cũng ghi cùng toạ độ (133,918)). Sau khi zoom kỹ trên ảnh gốc trong CVAT, Tùng xác nhận đây là một chiếc
  `Truck` (có thùng chở hàng, không phải xe ba bánh) và giữ nguyên nhãn của mình thay vì đổi theo reference/gợi ý
  K12 — ghi `why=E0_reference_defect`, `action=keep_with_reason` vào `findings.csv` (`round=rework`,
  `object_ref=L1+R4`), kèm [decision log](submission/40_decision_log.csv) D04 và ảnh chụp màn hình
  `screenshots/02_102750_truck_vs_threewheeler.png`. Luật R04 hiện chỉ mô tả chung, chưa có tiêu chí phân biệt xe
  ba bánh với xe tải nhỏ khi nhìn xa trên ảnh fisheye.
- **Việc tiếp theo:**
  - Peer QA Duy → Tùng cho slice B2-mid: soát bản khoá `24F8-C550` (trước reference), ghi vào
    `submission/r2_qa/peer_B2-mid/` và các dòng `r2_qa,B2-mid` trong findings.csv. Người theo dõi: Duy. Tùng sẽ
    phản hồi sau khi nhận được.
  - Ticket 1 gửi guideline team (D02, [30_escalation_ticket.md](submission/30_escalation_ticket.md)): cụm 5
    vật sát nhau ở `adasind_060000.jpg` — luật chưa nói rõ khi nào tách box riêng, khi nào gộp
    `ignore_region crowd_or_group`. Đã escalate, đang chờ phản hồi.
  - 2 box giữ bất đồng với reference chưa có người soát thứ hai xác nhận (D03): `adasind_086220.jpg` L6 (xe máy)
    và `adasind_102750.jpg` L2 (xích lô) — cả hai không có model/reference đồng thuận, chỉ dựa trên quan sát của
    Tùng.
  - QA Tùng → Anh cho B2-dense: xong (`3d42c40`); rework `823C-842B` của Thế Anh đã xử lý đúng cả 4 điểm nêu ra.
- **Đóng góp của A/B/C vào kế hoạch và exit ticket:** mỗi thành viên tự viết error card, guideline patch,
  escalation, review/sampling/gold plan và exit ticket cho slice của mình. Tùng làm các file này cho B2-mid
  (sampling/gold plan ở `c86eea2`; error card, guideline patch, escalation ticket, review plan, exit ticket ở
  `3d42c40`). Duy làm cho B4-center (`8237106`). Thế Anh làm cho B2-dense (`24e2cd6`). Mỗi slice có bộ kế hoạch
  riêng.
- **Thay đổi phân công nếu có:** không đổi người hay vai. Ở P5, bản rework đầu tiên của Tùng (mã `6D7B-BC3A`)
  chỉ sửa đúng 2/6 ca và vô tình đổi nhầm 1 box `ThreeWheeler` thành `Car`. Tùng ghi rõ lý do vào decision log
  (D01) rồi khoá lại đúng (`--relock`, mã `CF64-2680`) thay vì âm thầm sửa hay bỏ qua sai sót.

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Hoàng Công Tùng. sha256 của `r1_craft/annotations.xml` và
  `rework/annotations-v2.xml` tại HEAD khớp `lock.txt` (`24F8-C550`) và `lock2.txt` (`CF64-2680`).
- [ ] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: chưa có — Duy (người được phân công soát bài
  Tùng theo `team.json`) chưa thực hiện peer QA cho slice B2-mid (xem mục 3, mốc P3 "bài Tùng").
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Hoàng Công Tùng. `python3 lab11.py check`
  chạy tại commit `3d42c40` → "Hồ sơ hình thức đầy đủ" (exit 0).
- [x] manifest.json tại commit chốt có failed_gates rỗng. `submission/manifest.json` trên nhánh này có
  `failed_gates: []`.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được. Đã xác nhận qua GitHub API (`"private": false`) và mở thử
  các ảnh/screenshot trong repo, đều xem được.
- [ ] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố. "Đã push" thì đúng (nhiều commit đã lên
  GitHub, nhánh `hoang-cong-tung-2a202602229`), nhưng việc gửi link qua Discord (`lab_day11`) là hành động ngoài
  repo — Tùng tự tích khi đã thực sự gửi.

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
