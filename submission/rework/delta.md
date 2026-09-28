# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 10 | 11 | 2 | 1 | 6 | 6 |
| mid | 5 | 5 | 0 | 0 | 0 | 0 |
| edge | 3 | 3 | 0 | 0 | 0 | 0 |

## Findings action=rework
- adasind_270517.jpg L8 SPURIOUS: đã sửa
- adasind_270517.jpg L8 IGNORE_SCOPE: đã sửa
- adasind_271039.jpg R10 MISSING: đã sửa
- adasind_271039.jpg R10 MISSING: đã sửa

## Nhận xét của mình

- **Chỉ sửa hai ca `action=rework` mức P1**, cả hai có căn cứ trên ảnh + luật: (1) 271039 thêm `Pedestrian` [263,825,288,908] (người áo vàng quần xám, bị người áo đen che một phần) — trước đó mình nhầm với mui xe ba bánh vàng phía sau (E1, R01); (2) 270517 bỏ box `ThreeWheeler` L8 [117,765,149,807] và vẽ `ignore_region` `reason=unreadable` cùng chỗ, vì class chỉ suy từ tỉ lệ khung của một vật mờ cao 42 px (E1, R06).
- **Thay đổi thật:** center matched 10 → 11, missing 2 → 1 (ca R10). L8 vốn đã là IGNORE_SCOPE (nằm trong ignore unreadable của reference) nên không đổi số matched/spurious — thay đổi này làm nhãn đúng luật hơn chứ không làm đẹp số.
- **Spurious center giữ 6 → 6** và là cố ý: 271039 L2 (xe máy), L8 (e-rickshaw), L13 (người, model cũng thấy) là vật nhìn thấy mà reference thiếu (E0, đã escalate); L14 là khoảng trống luật về polygon unreadable (E2); L1 chưa đủ bằng chứng (E5). Sửa các box này để khớp reference sẽ là "sửa âm thầm" nhãn đúng.
- **Missing còn 1** (R1 295948): reference gọi xe tải nhỏ thùng hở là `Car`, mình giữ `Truck` theo R04 (E0, escalate).
- **Giới hạn phép so:** ba frame, 20 box reference; ego_body hình chữ nhật của reference ở 295948 loại 4 box của mình khỏi phép so, nên delta ở frame đó không phản ánh chất lượng nhãn. Bản đã khoá trước (`r1_craft`, mã 34BC-63D5) giữ nguyên; bản sau sửa là `annotations-v2.xml`, mã 5AE6-554F.
