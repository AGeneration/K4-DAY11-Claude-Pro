# Tự soát


## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ
- [x] lens_border và ego_body
- [x] Class sáu nhãn
- [x] Rider và Bike
- [x] Geometry trên ảnh fisheye gốc
- [x] truncated và occluded
- [x] Vật thiếu hoặc box trùng
- [x] ignore_region có reason
- [x] Tên task raw_fisheye và export CVAT 1.1

## Fill ratio (K12)
- adasind_270517.jpg box 2 center: 0.780
- adasind_270517.jpg box 3 edge: 0.644
- adasind_271039.jpg box 6 edge: 0.739
- adasind_271039.jpg box 3 edge: 0.629
mean edge: 0.671 (n=3)
mean center: 0.780 (n=1)

## Cảnh báo tự động đã xử lý

Bản nháp đầu (`exports/r1-draft.zip`, export theo **job**) báo `Tên task thiếu raw_fisheye` dù task CVAT tên `Day11 · ADASIND · B4-center · raw_fisheye`: CVAT local 2.75.1 không ghi `<task><name>` vào export job. Đã xử lý bằng cách export bản cuối qua **Export task dataset** (task 72 chỉ có một job 72, cùng nội dung) để meta mang tên task; `selfqc` trên bản cuối/bản khoá không còn cảnh báo nào (danh sách cảnh báo phía trên rỗng).

## Ghi chú soát tay (theo thứ tự checklist, soát trên ảnh gốc phóng to)

1. **Phạm vi H=40.** Đã rà từng vùng đường/vỉa hè của ba frame bằng crop phóng 3–6×. Box thấp nhất: 270517 L8 ThreeWheeler [117,765,149,807] cao 42 px (xe ba bánh sau SUV, giữ vì ≥40). Không box: 270517 xe nhỏ tại x≈145–167 (cao ~25 px); 271039 bóng hồng sau quầy hàng mép phải (x≈1065–1080, phần thấy <40 px); 295948 xe sau đuôi xe tải x≈421–438 (cao ~25 px) và xe trắng x≈451–466 (~28 px). Ca nghi ngờ: 270517 dải tối sát mép trái x=0–12, y≈757–885 — không đọc được là người hay cột/thân cây, chỉ rộng ~12 px; **không box**, ghi vào decision log.
2. **lens_border và ego_body.** Hai polygon `lens_border` mỗi frame giữ nguyên bản import (đã phủ lên ảnh: viền bám vành kính ở trên, trái, phải và đáy; không thấy lệch đáng kể). `ego_body` tự vẽ ở 270517 (người lái áo caro/quần tối/dép ở góc trái dưới, x 0–152, y 1025–1720) và 295948 (người áo caro góc trái dưới, x 0–225, y 1200–1700). **Không** vẽ ego ở 271039 (R07).
3. **Class.** Xe ba bánh auto/e-rickshaw → `ThreeWheeler` (270517: 3; 271039: 5; 295948: 1). Van trắng 271039 [25,814,99,907] là van chở người → `Car` (R04). Pickup/xe tải nhỏ 295948 [460,890,655,1062] → `Truck` (R04).
4. **Rider.** Người lái trong xe ba bánh 270517 (x≈669–785) không box riêng (R03). 295948: người đi xe đạp chở thùng hàng bên trái → một `Bike` [0,894,138,1210]; người quấn khăn caro ngồi trên xe đạp bên phải (thấy bánh trước x≈639–699, y≈1420–1567 và bàn chân trên pedal) → một `Bike` [574,606,1080,1716], truncated. 271039: người áo sọc trắng [432,814,465,892] đứng cạnh xe máy đỗ [422,868,454,949] — không thấy rõ ngồi trên yên nên tách `Pedestrian` + `Bike`; ca này ghi là nghi ngờ.
5. **Geometry.** Box bám phần nhìn thấy trên ảnh fisheye gốc, không nắn thẳng. Đã sửa 3/4 box prefill frame 270517: ThreeWheeler [442,711,840,1030]→[450,713,816,1005] (prefill thừa bên phải và dưới vùng blur); Bike [995,948,1079,1180]→[1014,955,1080,1175]; Car [277,754,337,827]→[272,752,353,829] (prefill hụt phần đuôi xe sau người đi bộ). Giữ nguyên Car [43,765,119,837]. Không có box nào phủ cả dãy xe: dãy xe ba bánh đỗ ở 271039 được tách thành từng xe.
6. **truncated / occluded.** `truncated` chỉ khi khung/vòng kính cắt: 270517 Bike mép phải, 295948 Bike thùng hàng (mép trái khung) và Bike người khăn caro (khung phải + vòng kính đáy). `occluded` khi vật khác che: ví dụ 270517 Car L4 bị người đi bộ che; 271039 xe ba bánh sau van, hai xe ba bánh sau người đi bộ; 295948 xe ba bánh và người áo vàng bị thùng hàng che.
7. **Thiếu/trùng.** Tự động không báo cặp cùng class IoU>0.7. 271039 có hai Pedestrian chồng nhau [392,818,438,936] và [393,823,418,904] là hai người khác nhau (người trước áo đen, người sau áo trắng) — không phải trùng.
8. **ignore_region.** Chỉ dùng `lens_border` và `ego_body`; không dùng `crowd_or_group` vì mọi người/xe đếm được từng cái (card 6). Mỗi polygon có đúng một `reason`; không box nào nằm ≥50% trong ignore.
9. **Tên task và định dạng.** Task `Day11 · ADASIND · B4-center · raw_fisheye`; export **CVAT for images 1.1**, không kèm ảnh.

K12: 4 polygon viền thấy được (SAM 2 đề xuất từ box, soát lại bằng mắt) nhóm `group_id` với box cùng class. Polygon xe ba bánh 270517 đã sửa tay để bao cả phần thân xe nằm dưới ô làm mờ riêng tư (SAM cắt lõm quanh ô blur) — fill ratio center tăng 0.705 → 0.780. Với n=1 center và n=3 edge, chênh lệch fill ratio chỉ minh hoạ, không kết luận.
