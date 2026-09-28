# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| adasind_060000.jpg (slice B2-mid) | 5 MISSING (cụm người/xe sát nhau, đã rework) + 1 IGNORE_SCOPE | Nhiều ca nhất trong slice, gắn trực tiếp với khoảng trống luật (`E2_guideline_gap`) đang escalate — ảnh hưởng cách tính zone `center`/`mid` cho cả lớp nếu không làm rõ ngưỡng, không chỉ riêng bài này | `findings.csv` (round `r3_diag`/`rework`, frame này), `rework/delta.md`, `screenshots/01_060000_crowd_cluster.png` |
| adasind_102750.jpg (slice B2-mid) | 1 MISSING đã sửa (Truck bỏ sót) + 1 WRONG_CLASS đang bất đồng với reference (Truck vs ThreeWheeler) + 1 SPURIOUS người vẽ tin là thật (xích lô) | Có bất đồng trực tiếp với reference (`E0_reference_defect`) chưa có người thứ hai xác nhận độc lập — cần review trước khi coi là kết luận cuối cùng | `findings.csv` dòng `L1+R4` và `L2` (round `rework`/`r3_diag`), `screenshots/02_102750_truck_vs_threewheeler.png` |

Giới hạn của kết luận từ ba frame ADASIND: Slice B2-mid chỉ có 3 frame với khoảng 20 vật tham chiếu, thuộc **một** camera fisheye duy nhất (không rõ tương ứng camera nào trong bốn camera SVM front/rear/left/right thật). Không thể suy tỷ lệ lỗi tổng thể, ngưỡng H=40px hay quyết định gold set cho toàn hệ thống bốn camera chỉ từ slice này.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: Khi chọn 200 frame, cần rải theo thời gian/tình huống khác nhau (tránh lấy nhiều frame liên tiếp trong cùng một đoạn video/cùng một cảnh, vì chúng gần như giống hệt nhau và không phải là các ca độc lập về mặt thống kê — giống như 3 frame ADASIND trong slice này thực chất chỉ là 3 lát cắt riêng lẻ được chọn có chủ đích, không phải mẫu liên tục). 200 frame là mẫu **có chủ đích** (ưu tiên ca hard/normal theo `risk`), giúp tìm và ưu tiên ca cần xem kỹ, nhưng vì không phải mẫu ngẫu nhiên đại diện cho 50.000 frame nên không thể dùng để tính tỷ lệ lỗi tổng thể hay công bố chất lượng của toàn bộ tập dữ liệu.
