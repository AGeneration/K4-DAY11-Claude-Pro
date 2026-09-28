# Kế hoạch review từ lỗi quan sát được

Báo cáo hiện dùng đủ ba frame của B2-dense từ job30. Chọn hai lát cắt ADASIND cần ưu tiên dưới đây; không dùng zone thay camera_id.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| 062370 — center/mid: van, Bike và Truck bị che | 4 dòng compare: BOX_GEOMETRY L3+R9, WRONG_CLASS L4+R4, MISSING R7/R8. R7 nghi trùng reference, chỉ ba ca nhãn được sửa. | Ban đầu TP=5 FP=2 FN=4; tách lỗi class/geometry thật khỏi reference defect trước rework. | XML/lock; compare.html; conflict CSV; screenshots/03-b2-van.png và 05-reference-duplicate.png. |
| 117120 — phương tiện nhỏ sát H=40 và vật bị che | 3 dòng compare: SPURIOUS L3/L7, MISSING R3; thêm ba box XML dưới H=40 cần soát scope. | TP=5 FP=2 FN=1; một box vẽ thiếu không đồng nghĩa vật dưới ngưỡng. Hai spurious có vật thật nhưng class/reference chưa phân xử. | XML raw index so với L in-scope; screenshots/07-job30-frame3.png; R3/M5 và M8/M10 trên model overlay; ticket 4. |

069450 là đối chứng: 5 TP, 0 FP, 0 FN cho box in-scope nhưng có một Car XML dưới H=40 và hai ThreeWheeler model gọi Truck. Một số 100% không thay soát phạm vi và taxonomy.

Giới hạn: Ba ảnh cùng miền/chuyến không phải mẫu độc lập đại diện 50.000 frame hoặc bốn camera. 48 dòng findings gồm lặp cùng sự kiện qua các pha; không dùng số dòng làm tỷ lệ lỗi hay đếm vật độc lập.

## Chuyển sang kế hoạch bốn camera giả lập

Tám ô front/rear/left/right × normal/hard: front 60, rear 50, left 45, right 45; tổng 200 (normal 95, hard 105). Trải theo chuyến/thời điểm/ánh sáng, lấy ngẫu nhiên trong từng tầng, bỏ near-duplicate, tách chuyến train/eval. Một thời điểm lấy bốn camera tính bốn quan sát ảnh.

QA kiểm riêng seam trước-trái, trước-phải, sau-trái, sau-phải và điều kiện khó của từng camera. Giữ timestamp/calibration/policy trước khi ghép identity hoặc BEV. Tỷ trọng hard là lựa chọn review, không phải tần suất lỗi toàn bộ dữ liệu; cần mẫu số và trọng số tầng phù hợp trước khi suy rộng.
