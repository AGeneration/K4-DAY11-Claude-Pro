# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 10 | 11 | 2 | 1 | 6 | 7 |
| mid | 5 | 4 | 0 | 1 | 0 | 1 |
| edge | 3 | 3 | 0 | 0 | 0 | 1 |

## Findings action=rework
- adasind_271039.jpg R10 MISSING: đã sửa
- adasind_271039.jpg R10 MISSING: đã sửa

## Nhận xét của mình

Bản sau sửa `annotations-v2.xml` là bản hiện tại trong CVAT local (task 72, mã `FA15-D3EC`). Bản trước là `r1_craft`,
khoá trước khi mở reference (`34BC-63D5`). Mọi thay đổi có dòng trong `findings.csv` (`round=rework`) và decision log
D8. Chỉ số L của bản rework theo thứ tự XML của bản này, khác với `r1_craft`.

**Thay đổi thật, theo zone:**

- **center: matched 10 → 11, missing 2 → 1.** Thêm `Pedestrian` áo vàng quần xám ở 271039 [263,825,288,908] (khớp R10),
  là lỗi bỏ sót của mình (E1, R01). **Spurious 6 → 7** vì bản rework thêm `ThreeWheeler` L9 [424,916,440,965] sau đuôi
  xe tải 295948. Reference không có vật này, còn model có (M6 `Car`); ca này vẫn chưa chắc (E5).
- **mid: matched 5 → 4, missing 0 → 1, spurious 0 → 1.** Người quấn khăn caro ở 295948 đổi từ một `Bike` thành
  `Pedestrian` (truncated) vì bàn chân chạm đất cạnh bánh xe đạp. Reference vẫn coi là rider (R3 `Bike`), nên một cặp
  WRONG_CLASS bị đếm thành 1 missing + 1 spurious. Đây là bất đồng về R03 với người đang dừng xe, không phải sửa theo
  reference (E2).
- **edge: spurious 0 → 1.** Là `Bike` L3 [639,1415,1013,1581] cho xe đạp dưới người khăn caro, hệ quả của cách tách ở trên.

**Thay đổi không làm đổi số:**

- 295948: người áo xanh ngọc được tách khỏi xe đạp chở thùng (`Pedestrian` + `Bike`), nhưng cả hai vẫn nằm trong
  `ego_body` chữ nhật của reference (Ticket 1).
- 270517: box xe tay ga mở rộng lên trên, IoU với R7 tăng 0.67 → 0.88 nhưng vẫn là matched. Box `ThreeWheeler`
  [117,765,149,807] nằm trong ignore `unreadable` của reference nên là don't-care.

**Vì sao không "cải thiện" thêm số:** ngoài R10, mọi spurious còn lại ở center là vật reference thiếu (271039: xe máy,
e-rickshaw, người áo trắng; E0, đã escalate), polygon `unreadable` phủ nửa người (E2) hoặc ca chưa phân xử (E5). Sửa
các box này cho khớp reference sẽ là sửa âm thầm nhãn mà mình tin đúng.

**Giới hạn của phép so:** chỉ ba frame và 20 box reference. Ở 295948, `ego_body` chữ nhật của reference loại 5 box
của mình khỏi phép so. Bản rework được làm sau khi đã xem reference.
