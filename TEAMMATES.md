# Thành viên và phân vai — Day11 SVM 360 Fisheye (bản chung của nhóm)

## 1. Thông tin nhóm

- Khóa/lớp: AI20K · K4
- Tên nhóm: Claude-Pro
- Repo Public: https://github.com/AGeneration/K4-DAY11-Claude-Pro
- Kênh trao đổi nội bộ: Discord, kênh `lab_day11`
- Commit chia task và setup chung: `c2ae9e7` (`mode.json`, `team.json`, `doctor.txt`)

## 2. Trạng thái hoàn thành

**Cả ba thành viên đã hoàn thành đầy đủ các yêu cầu của bài lab.** Mỗi người làm trọn cả ba vai A · B · C trên
slice của mình (gán nhãn, QA chéo, chẩn đoán, rework, kế hoạch, exit ticket), chạy `lab11.py check` exit 0
("Hồ sơ hình thức đầy đủ") với `manifest.json` có `failed_gates: []`.

**Phần làm của mỗi cá nhân nằm trên branch riêng của người đó.** Nhánh `main` gom lại một bản sao nguyên vẹn của
từng branch vào thư mục cùng tên để tiện xem; nguồn gốc và lịch sử commit đầy đủ vẫn nằm trên branch.

| Thành viên | MSSV | Định danh `mode` | Slice | Branch (nguồn chính) | Bản sao trên `main` | TEAMMATES riêng |
|---|---|---|---|---|---|---|
| Vũ Minh Duy | 2A202602198 | `duy` | `B4-center` | `vu-minh-duy-2a202602198` | [vu-minh-duy-2a202602198/](vu-minh-duy-2a202602198/) | [TEAMMATES.md](vu-minh-duy-2a202602198/TEAMMATES.md) |
| Hoàng Công Tùng | 2A202602229 | `tung` | `B2-mid` | `hoang-cong-tung-2a202602229` | [hoang-cong-tung-2a202602229/](hoang-cong-tung-2a202602229/) | [TEAMMATES.md](hoang-cong-tung-2a202602229/TEAMMATES.md) |
| Nguyễn Lê Thế Anh | 2A202602164 | `anh` | `B2-dense` | `NguyenLeTheAnh-2A202602164` | [NguyenLeTheAnh-2A202602164/](NguyenLeTheAnh-2A202602164/) | [TEAMMATES.md](NguyenLeTheAnh-2A202602164/TEAMMATES.md), [BAN_GIAO.md](NguyenLeTheAnh-2A202602164/BAN_GIAO.md) |

Mỗi thư mục là một hồ sơ độc lập, tự chạy được: vào thư mục đó rồi chạy `python lab11.py check`.

## 3. Cách chia việc

Nhóm làm theo vòng quay trong `docs/03-roles-rotation-vi.md`: **mỗi người làm cả ba vai** trên hồ sơ của mình.
`mode --members anh duy tung` chia mỗi người một slice. Vòng QA chéo theo `team.json` là
**anh → duy → tung → anh** (Thế Anh soát Duy, Duy soát Tùng, Tùng soát Thế Anh).

| Vai | Vũ Minh Duy (`B4-center`) | Hoàng Công Tùng (`B2-mid`) | Nguyễn Lê Thế Anh (`B2-dense`) |
|---|---|---|---|
| A · Gán nhãn | P0 `3681d0b`; C0 `bf1a4d2` (mã `A744-7D43`); khoá R1 `5c12a03` (`34BC-63D5`); rework `79fdaac` (`FA15-D3EC`) | C0 `ACE4-486E`, khoá R1 `c86eea2` (`24F8-C550`); rework `3d42c40` (`CF64-2680`, relock từ `6D7B-BC3A`) | Khoá R1 `E4B2-125A`; rework qua vòng import/export CVAT (`823C-842B`, `cvat_roundtrip.json`) — `24e2cd6`, `fad2e60`, `0182dad` |
| B · QA độc lập | Cold review bản của mình (D3); QA chéo slice B2-mid của Tùng: `ff9fa5b`, bản khoá `24F8-C550`, 7 nhận xét QA-TUNG-01…07 và đối chiếu rework `CF64-2680` (`submission/r2_qa/peer_B2-mid/`) | Soát bản khoá B2-dense `E4B2-125A` của Thế Anh (`3d42c40`, 4 nhận xét) | Soát bản khoá B4-center của Duy (`bcdd5ac`, QA-DUY-01…04, đối chiếu rework `FA15-D3EC`) |
| C · Chẩn đoán & điều phối | P4 `c062c84` (zone table, local quality, model); P6 `8237106` (error card, guideline patch, escalation, review/sampling/gold plan, exit ticket); decision log D1–D12 | `findings.csv` round `r3_diag`, decision log D01–D04; error card, guideline patch, escalation, review/sampling/gold plan, exit ticket (`c86eea2`, `3d42c40`) | 48 findings, 10 ảnh bằng chứng, error card, 5 ticket, sampling 8 ô / 200 frame, gold plan 4 camera, exit ticket |

Chi tiết bàn giao theo pha, các ca bất đồng đã phân xử và phần xác nhận trước khi nộp của từng người nằm trong
TEAMMATES.md riêng trên branch của người đó.

## 4. Xác nhận chung

- [x] Cả ba thành viên đã hoàn thành đầy đủ yêu cầu trên slice của mình.
- [x] Mỗi hồ sơ có `lab11.py check` exit 0 và `manifest.json` với `failed_gates: []`.
- [x] Nhãn đã khoá (R1 và rework) có sha256 khớp `lock.txt` / `lock2.txt` trên từng branch.
- [x] Đủ vòng QA chéo theo `team.json`: Thế Anh → Duy (`bcdd5ac`), Duy → Tùng (`ff9fa5b`), Tùng → Thế Anh (`3d42c40`);
  cả ba đều soát bản khoá trước khi xem reference.
- [x] Repo nhóm Public; ảnh và bằng chứng mở được.
- [x] Phần làm của mỗi cá nhân nằm trên branch của họ; `main` chỉ là bản tổng hợp.
