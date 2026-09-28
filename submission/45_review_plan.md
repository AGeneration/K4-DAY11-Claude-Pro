# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| **Cụm che khuất dày ở `center`** — `adasind_271039.jpg` (dãy xe ba bánh đỗ sau 5–6 người đi bộ) | 6 ca của L so với R: 1 MISSING thật của mình (R10, E1), 3 SPURIOUS do reference thiếu (L2, L8, L13, E0), 1 do polygon ignore phủ nửa người (L14, E2), 1 chưa phân xử (L1, E5); thêm 3 FP class của model (M9, M11, M12) | Đây là nơi cả người gán, reference và model cùng gãy, và 6/8 lỗi center của L nằm ở frame này; mỗi ca đổi trực tiếp TP/FP/FN của `Pedestrian`, `Bike`, `ThreeWheeler`. Một người soát thứ hai cần đếm từng người/xe trên crop ≥4x | Crop phóng to từng cụm (như `screenshots/02_271039_center_conflicts.png`), `object_ref` L/R/M, rule R01/R03/R09, frame kề của 271039 để xử ca L1 |
| **Phạm vi `ego_body` và người sát camera** — `adasind_295948.jpg`, `adasind_270517.jpg` (người lái ego áo caro ở góc trái dưới) | 1 lỗi phạm vi P0 của reference (ego_body chữ nhật che 4 vật: L1, L2, L3, L7), 1 ca luật chưa rõ (người khăn caro trên xe đạp sát camera, L4), 3 box model trên người ngồi trong xe ba bánh (M5, M10, M11) và 1 box model trên người lái ego (295948 Pedestrian [0,1200,232,1712]) | Lỗi phạm vi làm hỏng mọi phép so ở frame (R10 xếp P0) và có thể lặp ở 46/48 frame có thân ego; tín hiệu tổng hợp "ego_body 49" của report pre-label cho thấy vùng này đáng soát trước | Polygon `ego_body` của L và R chồng lên ảnh (`screenshots/01_295948_ref_ego_body_rectangle.png`), decision log D4/D6, rule R07/R10 |

Giới hạn của kết luận từ ba frame ADASIND: chỉ 3 frame (+1 frame C0), 20 box reference trong phạm vi (edge chỉ có 3),
đều từ **một** camera fisheye của một bộ dữ liệu Ấn Độ — nên không ước lượng được tỷ lệ lỗi theo zone hay theo class,
chỉ chỉ ra *loại* ca cần soi. Teaching reference có ít nhất hai lỗi đã escalate, nên chỉ số `local-quality`
(micro precision 0.750, recall 0.900) đo độ khớp với một bản nháp có lỗi, không đo độ đúng. Ngưỡng IoU cũng đổi số:
ở 0.7 thì L mid rớt từ 5 xuống 3 matched (`iou_sweep.md`).

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: (1) lấy mẫu theo **cảnh/clip** trước rồi mới theo frame —
tối đa 1–2 frame mỗi clip và cách nhau ≥ vài giây, để 10 frame liền nhau của cùng một ngã tư không bị đếm như 10 ca
độc lập; (2) mỗi ô `camera × normal/hard` có danh sách tiêu chí hard đã định trước (che khuất dày ở center như 271039,
vật bị vòng kính cắt, người/xe sát thân xe ego, seam với camera kề, xe ba bánh/xe hai bánh chở người, ngược sáng/đêm)
và đếm xem mỗi tiêu chí có ít nhất vài frame; (3) giữ thêm cột `clip_id`, `timestamp`, `camera_id` và phiên bản
calibration để kiểm trùng lặp và ghép seam sau này. Kế hoạch này chỉ giúp **tìm ca cần soi**: 200 frame chọn có chủ
đích (dồn vào hard) không phải mẫu ngẫu nhiên của 50.000 frame, nên không suy ra được tỷ lệ lỗi của toàn bộ tập; muốn
đo tỷ lệ cần thêm một mẫu ngẫu nhiên phân tầng riêng theo camera.
