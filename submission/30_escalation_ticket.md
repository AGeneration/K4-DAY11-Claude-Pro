# Escalation ticket

Phạm vi: teaching reference của slice **B4-center** (ADASIND, một camera fisheye, 6 class động — tập con của taxonomy
ADASIND gốc). Cả hai ticket là lỗi nghi ngờ ở reference (`E0_reference_defect`), không phải lỗi của annotator, nên
mình không có thẩm quyền tự sửa reference. Mỗi ca có dòng `action=escalate` trong `findings.csv` và dòng
`status=escalated` trong `40_decision_log.csv` (D6, D7).

## Ticket 1 — `ego_body` của reference phủ nhầm người và xe tham gia giao thông (P0)

- **Frame:** `adasind_295948.jpg`
- **Ảnh chụp:** `submission/screenshots/01_295948_ref_ego_body_rectangle.png` (hình chữ nhật hồng là `ego_body` của
  reference; đường cyan là `ego_body` của mình chỉ bao người lái áo caro ở góc trái dưới)
- **Hiện tượng:** reference vẽ `ignore_region reason=ego_body` là một hình chữ nhật [x 0–229, y 915–1736]. Thân/người
  lái ego thực tế chỉ ở góc trái dưới (x 0–225, y ≈1200–1700). Chữ nhật này che thêm xe ba bánh [52,922,113,981],
  người áo vàng [110,920,141,992], người che ô [155,936,191,1021] và xe đạp chở thùng hàng [0,894,138,1210].
- **Expected impact:** theo R09 các box nằm ≥50% trong ignore thành don't-care, nên 4 box của mình (L1, L2, L3, L7) và
  6 box của model bị loại khỏi phép so ở frame này; compare báo 4 `IGNORE_SCOPE` thay vì matched/missing thật. Mọi
  thống kê zone `mid`/`center` và local-quality của 295948 vì thế không phản ánh chất lượng nhãn. Nếu reference này
  được dùng làm mẫu cho gold set, người gán sau sẽ học rằng có thể dùng `ego_body` để "xoá" vật khó ở rìa ảnh — đúng
  loại lỗi phạm vi P0 mà R10 cảnh báo.
- **Owner:** `qa` (người giữ teaching reference)
- **Recommendation:** sửa polygon `ego_body` của 295948 cho bám người lái ego ở góc trái dưới (có thể dùng polygon
  của export `r1_craft` làm điểm bắt đầu), rồi thêm vào reference: `Bike` truncated cho xe đạp chở thùng, `ThreeWheeler`
  occluded [52,922,113,981], `Pedestrian` [110,920,141,992] và [155,936,191,1021]. Thêm một bước kiểm tự động: cảnh báo
  mọi polygon `ego_body` chứa trọn một box đã có ở pre-label hoặc bản của annotator.

## Ticket 2 — reference thiếu vật nhìn thấy và sai class xe tải nhỏ (P1)

- **Frame:** `adasind_271039.jpg` và `adasind_295948.jpg`
- **Ảnh chụp:** `submission/screenshots/02_271039_center_conflicts.png`,
  `submission/screenshots/03_295948_pickup_truck_vs_car.png`
- **Hiện tượng:**
  - 271039: xe máy đỗ [422,868,454,949] cao 81 px (L2), người áo trắng [393,823,418,904] cao 81 px (L13, model cũng
    thấy — M8), e-rickshaw bị che [192,825,265,897] (L8) đều không có trong reference. Polygon `unreadable` của
    reference [436–462, 824–872] chỉ phủ thân trên người áo sọc, nên box người này ở L (48% trong ignore) thành
    SPURIOUS còn ở M (54%) bị bỏ qua.
  - 295948: xe tải nhỏ thùng hở [460,890,655,1062] bị reference gán `Car`; L và model đều gán `Truck`.
- **Expected impact:** center của B4-center có 6 spurious và 2 missing; sau khi soi ảnh thì chỉ 1 missing là lỗi của mình
  (đã rework). Nếu không sửa reference, precision của `Pedestrian`/`Bike`/`ThreeWheeler` và recall của `Car`/`Truck`
  trong `local_quality.md` bị kéo lệch, và ma trận nhầm lớp ghi một cặp Car→Truck không có thật.
- **Owner:** `qa` (sửa reference); phần polygon `unreadable` giao `guideline` (xem `20_guideline_patch.md`).
- **Recommendation:** bổ sung `Bike` occluded, `Pedestrian` occluded và `ThreeWheeler` occluded như trên vào reference
  271039; đổi class xe tải nhỏ 295948 thành `Truck` theo R04; vẽ lại polygon `unreadable` bao trọn người áo sọc (hoặc
  thay bằng box `Pedestrian` occluded nếu người soát đồng ý là đọc được). Sau khi sửa, chạy lại
  `python3 lab11.py compare r1_craft` và `local-quality` để có số mới.
