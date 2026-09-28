# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: AI20K · K4
- Tên nhóm: Claude-Pro
- Repo Public: https://github.com/AGeneration/K4-DAY11-Claude-Pro
- Máy giữ hồ sơ chính / người quản lý: mỗi thành viên giữ hồ sơ của mình trên branch riêng
  (`vu-minh-duy-2a202602198`, `hoang-cong-tung-2a202602229`, `NguyenLeTheAnh-2A202602164`). Người giữ hồ sơ này:
  Vũ Minh Duy. Commit chia task và setup chung: `c2ae9e7` trên `main`.
- Slice chung lấy từ mode.json: nhóm không dùng slice chung. `mode --members anh duy tung` chia mỗi người một slice:
  anh → `B2-dense`, duy → `B4-center`, tung → `B2-mid`. Hồ sơ này là slice `B4-center`.
- Tên định danh vai A dùng cho --self: `duy` (hồ sơ này); hai bạn còn lại dùng `tung` và `anh`.
- Kênh trao đổi nội bộ: Discord
- Đại diện nộp (vai C): Vũ Minh Duy, 2A202602198 (cho hồ sơ này; Tùng và Thế Anh nộp branch của mình)
- Commit chốt bài: `ff9fa5b` (P3 peer QA B2-mid; `lab11.py check` exit 0)

## 2. Ba vai chính

Nhóm làm theo vòng quay trong [docs/03-roles-rotation-vi.md](docs/03-roles-rotation-vi.md): **mỗi người làm cả ba vai**.
Người đó gán nhãn slice của mình (A), soát mù bản khoá của người kế bên (B), rồi chẩn đoán và hoàn thiện slice của mình (C).
Vòng QA theo [team.json](submission/00_setup/team.json) là **anh → duy → tung → anh**, nghĩa là anh soát duy, duy soát tung, tung soát anh.

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Vũ Minh Duy | 2A202602198 | `duy` | Parking, C0 và slice B4-center; self-QC, lock, rework | Commit `3681d0b` (P0), `bf1a4d2` (C0, mã `A744-7D43`), `5c12a03` (B4-center khoá `34BC-63D5`), `f6ae329`/`79fdaac` (rework khoá `FA15-D3EC`) |
| A · Gán nhãn | Hoàng Công Tùng | 2A202602229 | `tung` | Parking, C0 và slice B2-mid; self-QC, lock, rework | Commit `c86eea2` trên branch của Tùng: C0 `ACE4-486E`, B2-mid khoá `24F8-C550`, 3 finding calib. Commit `3d42c40`: rework khoá `CF64-2680` (relock từ `6D7B-BC3A`), decision log D01–D04 |
| A · Gán nhãn | Nguyễn Lê Thế Anh | 2A202602164 | `anh` | Parking, C0 và slice B2-dense; self-QC, lock, rework | Commit `24e2cd6`, `fad2e60` và `0182dad` trên branch của Thế Anh: B2-dense khoá `E4B2-125A`, rework khoá `823C-842B` sau vòng import/export CVAT (`cvat_roundtrip.json`; các mã cũ `79DF-6639`, `00BC-F291` nằm trong history) |
| B · QA độc lập | Vũ Minh Duy → soát bài Tùng | 2A202602198 | `duy` | Soát bản khoá B2-mid trước reference, ghi finding QA | Cold review bản của mình ([qa_review.md](submission/r2_qa/qa_review.md), D3). Peer QA B2-mid đã xong: soát bản khoá `24F8-C550` trước reference, 7 nhận xét QA-TUNG-01…07 và đối chiếu rework `CF64-2680` trong [peer_B2-mid/qa_review.md](submission/r2_qa/peer_B2-mid/qa_review.md), kèm `source_tung/provenance.json`; 7 dòng `r2_qa,B2-mid` trong [findings.csv](submission/findings.csv) |
| B · QA độc lập | Nguyễn Lê Thế Anh → soát bài Duy | 2A202602164 | `anh` | Soát bản khoá B4-center trước reference, kiểm lại bản rework | Commit `bcdd5ac` trên branch của Thế Anh: `submission/r2_qa/qa_review.md` có 4 nhận xét QA-DUY-01…04 và đối chiếu rework `FA15-D3EC`, kèm `source_duy/provenance.json` |
| B · QA độc lập | Hoàng Công Tùng → soát bài Thế Anh | 2A202602229 | `tung` | Soát bản khoá B2-dense | Commit `3d42c40` trên branch của Tùng: `submission/r2_qa/qa_review.md` cho bản khoá `E4B2-125A`, 4 nhận xét (062370 L4 R04; 069450 L6, 117120 L3, 117120 L6 R01), 4 dòng `r2_qa,B2-dense` trong findings.csv |
| C · Chẩn đoán & điều phối | Vũ Minh Duy | 2A202602198 | `duy` | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp cho B4-center | Commit `c062c84` (P4: zone table, local quality, model), `8237106` (P6: error card, guideline patch, escalation, kế hoạch, exit ticket), [40_decision_log.csv](submission/40_decision_log.csv) D1–D12 |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI. Nhóm dùng đúng vòng đó:
mỗi người một slice và một hồ sơ, rồi QA chéo theo vòng.

## 3. Bàn giao theo pha

Các mốc dưới đây ghi theo hồ sơ B4-center của Duy. Mốc nào có trao đổi chéo thì ghi thêm luồng giữa các thành viên.

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | Duy → Tùng, Thế Anh | `c2ae9e7` trên `main`: `mode.json`, `team.json`, `doctor.txt` | Cả ba chạy `mode` với cùng danh sách `anh duy tung`. `assignments` và `qa_reviews` trong mode.json/team.json của ba branch trùng nhau | Xong |
| P2 · Khóa bản đầu | Duy → Thế Anh (QA) | `submission/r1_craft/` tại `5c12a03`, mã `34BC-63D5`, sha256 `34bc63d5…63f768b` | Thế Anh so sha256 và mã với `lock.txt`, lưu nguyên bản vào `source_duy/annotations.xml` (29 box, 12 polygon) | Xong. Thế Anh nhận file muộn (review lúc 21:44), sau khi Duy đã cold review (D3) |
| P2 · Khóa bản đầu (bài Tùng) | Tùng → Duy (QA) | Branch `hoang-cong-tung-2a202602229`, `c86eea2`, mã `24F8-C550` | Duy kiểm `git show …:r1_craft/annotations.xml` ra sha256 `24f8c550…621354`, khớp `lock.txt` | Xong |
| P3 · Chốt QA mù | Thế Anh → Duy | `bcdd5ac`: QA-DUY-01…04, ảnh `screenshots/duy-*.png` | Duy đối chiếu với cold review của mình: QA-DUY-04 trùng nhận xét 295948 L4 | Xong. Nhận xét được ghi trong hồ sơ của Thế Anh |
| P3 · Chốt QA mù (bài Tùng) | Duy → Tùng | [peer_B2-mid/](submission/r2_qa/peer_B2-mid/): QA-TUNG-01…07, ảnh `screenshots/tung-*.png`, mã khoá `24F8-C550` | Duy kiểm sha256 bản R1 khớp `lock.txt` trước khi soát; sau đó mới đối chiếu rework `CF64-2680`: QA-TUNG-02 đã xử lý, còn lại để Tùng phản hồi; rework phát sinh 2 box nằm trong ignore (R09) | Xong phía QA. Nhận xét đã giao Tùng |
| P3 · Chốt QA mù (bài Thế Anh) | Tùng → Thế Anh | `3d42c40` trên branch Tùng: `r2_qa/qa_review.md`, mã khoá `E4B2-125A` | Rework của Thế Anh sửa cùng các ca (062370 L4 đổi Car, REC-02; 069450 L6 bỏ box, REC-03; Car dưới 40 px ở 117120 loại khỏi bản sửa) | Xong |
| P4 · Quyết định sửa | Duy (vai C) → chính Duy (vai A) | `c062c84`, `findings.csv` round `r3_diag`, decision log D4–D8 | Mỗi khác biệt với reference đều có WHAT/WHY/owner. Hai ca reference sai được escalate (D6, D7) chứ không sửa nhãn theo reference | Xong |
| P5 · Kiểm bản sửa | Duy → Thế Anh → Duy | `rework/annotations-v2.xml`, `lock2.txt` mã `FA15-D3EC`, [delta.md](submission/rework/delta.md), commit `79fdaac` | Thế Anh đối chiếu bản rework với từng QA-DUY: 04 đã đổi (tách Pedestrian + Bike); 01–03 có bước xử lý tiếp theo ở mục 4 | Đang hoàn thiện, xem mục 4 |
| P6 · Chốt nộp | Duy (A, B) → Duy (C) | [manifest.json](submission/manifest.json), commit chốt | `lab11.py check` chạy lại sau khi bổ sung peer QA B2-mid: exit 0 ("Hồ sơ hình thức đầy đủ"), `failed_gates: []` | Xong |

## 4. Bất đồng và phối hợp

- **Một ca đã phân xử:** 295948 L4, R03. Người quấn khăn caro sát camera có phải rider (một `Bike`) không.
  Duy (cold review) và Thế Anh (QA-DUY-04) cùng nêu ca này, còn teaching reference gán một `Bike`. Duy soi crop thấy
  bàn chân chạm đất cạnh bánh xe và không thấy khung nối với xe ego. Vì vậy Duy quyết định tách thành `Pedestrian`
  truncated và `Bike`, rồi đưa vào rework `FA15-D3EC`
  ([decision log](submission/40_decision_log.csv) D4, D8; [delta.md](submission/rework/delta.md) E2). Luật chưa nói về
  người đang dừng xe và đứng dạng chân, nên Duy đề xuất bổ sung ở [20_guideline_patch.md](submission/20_guideline_patch.md).
  Thế Anh ghi nhận thay đổi và lưu ý vùng xe bị che, blur; ghi chú này được giữ lại để người duyệt guideline tham khảo.
- **Việc tiếp theo:**
  - QA-DUY-01 (270517 group 2, R05): box ghi `truncated=true` nhưng polygon cùng group ghi false.
    Người theo dõi: Duy. Phép kiểm tiếp theo: đồng bộ attribute polygon, relock rồi chạy `rework`.
  - QA-DUY-02 (271039 L1, R05): attribute `occluded=true` nhưng trường XML chuẩn `occluded=0`. Người theo dõi: Duy.
    Phép kiểm tiếp theo: import/export lại trên CVAT để đồng bộ hai trường.
  - QA-DUY-03 (271039 L12+L13, R02): hai người chồng box. Người theo dõi: Duy. Cần ghi rõ phần nhìn thấy của từng người.
  - Peer QA duy → tung cho B2-mid: xong. 7 nhận xét QA-TUNG-01…07 trên bản khoá `24F8-C550`
    ([peer_B2-mid/qa_review.md](submission/r2_qa/peer_B2-mid/qa_review.md)). Người theo dõi phản hồi: Tùng (các ca
    còn mở và 2 box vi phạm R09 trong rework `CF64-2680`).
  - QA tung → anh cho B2-dense: xong (`3d42c40`); rework `823C-842B` của Thế Anh đã xử lý các ca này.
  - Ticket 1 và 2 gửi người giữ reference (D6, D7, [30_escalation_ticket.md](submission/30_escalation_ticket.md)):
    đã escalate, đang chờ người giữ reference phản hồi.
- **Đóng góp của A/B/C vào kế hoạch và exit ticket:** mỗi thành viên tự viết error card, guideline patch, escalation,
  review/sampling/gold plan và exit ticket cho slice của mình. Duy làm các file này cho B4-center (`8237106`). Thế Anh
  làm cho B2-dense (`24e2cd6`). Tùng làm cho B2-mid (sampling/gold plan ở `c86eea2`; error card, guideline patch, escalation,
  review plan, exit ticket ở `3d42c40`). Mỗi slice có bộ kế hoạch riêng.
- **Thay đổi phân công nếu có:** không đổi người hay vai. Chỉ có thứ tự ở P3 thay đổi: Duy chờ quá 5 phút mà chưa nhận
  được file nên cold review bài mình trước (D3). Sau đó Duy làm peer QA cho Tùng theo đúng vòng team.json ([peer_B2-mid/](submission/r2_qa/peer_B2-mid/)). Thế Anh soát bài Duy muộn hơn, ở commit `bcdd5ac`, dựa trên các bản export
  Duy đã khoá tại `79fdaac`.

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Vũ Minh Duy. sha256 của `r1_craft/annotations.xml` và
  `rework/annotations-v2.xml` tại HEAD khớp `lock.txt` (`34BC-63D5`) và `lock2.txt` (`FA15-D3EC`). Thế Anh cũng đã
  kiểm lại độc lập hai mã này trong `provenance.json`.
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Nguyễn Lê Thế Anh (`bcdd5ac`,
  `reviewed_reference_or_model: false`, kiểm lại rework FA15-D3EC).
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Vũ Minh Duy. `check` chạy lại sau khi bổ sung
  peer QA B2-mid, exit 0.
- [x] manifest.json tại commit chốt có failed_gates rỗng (`failed_gates: []`).
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.

Chỉ đánh dấu việc đã kiểm thật. Nhóm nộp một hồ sơ chung; check không tự chấm đóng góp từng người. Giữ nguyên header/các cột enum của findings.csv; tên người được ghi trong tài liệu này hoặc phần note thích hợp.
