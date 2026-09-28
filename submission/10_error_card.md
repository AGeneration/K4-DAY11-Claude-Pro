# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | BOX_GEOMETRY | 1 |
| center | B2 | MISSING | 11 |
| center | B2 | SPURIOUS | 12 |
| center | C0 | SPURIOUS | 2 |
| edge | B2 | SPURIOUS | 2 |
| mid | B2 | MISSING | 4 |
| mid | B2 | SPURIOUS | 4 |
| mid | B2 | WRONG_CLASS | 2 |
| unknown | B2 | STRUCTURE | 9 |
| unknown | C0 | IGNORE_SCOPE | 1 |

## Top defects
- SPURIOUS: 20 (ví dụ frame adasind_019560.jpg)
- MISSING: 15 (ví dụ frame adasind_062370.jpg)
- STRUCTURE: 9 (ví dụ frame adasind_069450.jpg)

## Phân tích của bạn

Hồ sơ job30 có 48 dòng findings qua các pha, không phải 48 vật hoặc 48 lỗi độc lập. Một vật có thể xuất hiện ở QA, compare và model; cặp LR_noM/M_only thường là cùng vật nhưng khác class. Bảng số trên do card tính lại từ findings mới. Các dòng STRUCTURE không có box in-scope nên có zone unknown; đó không phải camera hay zone thứ tư.

- **Nhãn người học:** 062370 L4 van đang là Truck (R04); L3 Bike rộng quá (R02); R8 Truck bị che chưa có nhãn (R01/R05). 069450 có box Car thứ 6 cao 24.46 px cần bỏ. 117120 có Car số 2 trong XML bị vẽ thiếu phần trên, khiến H=37.43 px dù vật thấy được khoảng 43 px; sửa geometry thay vì xóa. Hai Car nhỏ XML3/XML6 dưới 40 px được loại khỏi bản sửa.
- **Reference và ca mơ hồ:** 062370 R7 nằm trong R5 trên cùng ThreeWheeler, nghi duplicate. 117120 L3 Bus có vật thật nhưng class Bus/Car/Truck khác nhau giữa L và hai M; L7 ThreeWheeler là vật bị che mà R không có, cần soát cả reference và box còn rộng. Giữ hai nhãn này chờ QA, không xóa chỉ để tăng precision.
- **Model:** Sáu ThreeWheeler được M gọi Truck trên ba frame; ba rider bị tách Pedestrian; SUV 117120 cũng bị gọi Truck. Đây là tín hiệu lặp cho giả thuyết lệch taxonomy/miền mục tiêu, chưa chứng minh nguyên nhân là fisheye. Kiểm mapping, policy rider và output gần trùng M8/M10 tại 117120 trước kết luận.
- **Trước/sau:** Công cụ tính matched 15→19, missing 5→1, spurious 4→2. Missing còn lại là R7; hai spurious còn lại là Bus/ThreeWheeler 117120 đang escalation. Đây là độ khớp teaching reference chưa phê duyệt gold, không phải điểm rubric. Giữ số thật, không cố đạt 100%.
- **Owner và bằng chứng:** annotator nhận sửa nhãn có căn cứ; qa nhận R7, L3/L7 của 117120 và C0 L2/L8; ai_team kiểm taxonomy model. Xem screenshots/03-b2-van.png, 04-b2-scope.png, 05-reference-duplicate.png, 06-model-taxonomy.png, 07-job30-frame3.png và local_quality_conflicts.csv.
- **Nguồn và giới hạn:** R1 là nguyên XML export job30 đã khóa E4B2-125A, đủ ba ảnh. Rework 00BC-F291 là đề xuất chỉnh sửa tại máy, chưa có vòng import/export CVAT được xác minh. K12 đã ghi giảm, không giả lập số polygon. Review có trợ lý hỗ trợ và kế thừa lịch sử hai ảnh đầu; không mạo nhận là review độc lập mới của Duy.
