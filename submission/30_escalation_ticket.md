# Escalation ticket

Các ticket được ghi trong hồ sơ để bàn giao; chưa gửi trực tiếp cho Lab Coach/AI team và chưa nhận kết quả adjudication.

## Ticket 1 — Reference nghi trùng R5/R7

- **Frame:** adasind_062370.jpg, B2-dense; R5 và R7 trong teaching reference.
- **Ảnh chụp:** [screenshots/05-reference-duplicate.png](screenshots/05-reference-duplicate.png).
- **Expected impact:** R7 bị đếm là missing/FN dù L6 đã ôm chiếc xe ba bánh tương ứng R5. Nếu reference có duplicate, số thiếu center và recall bị ảnh hưởng. Bản rework vẫn còn một FN này; không tự sửa số hoặc gọi reference là gold.
- **Owner:** qa, phối hợp người quản lý teaching reference.
- **Recommendation:** Soi ảnh gốc và vùng blur, kiểm có một hay hai xe. R7=(163;814;254;874) nằm hoàn toàn trong R5=(161;750;258;874). Nếu xác nhận trùng, sửa reference có version mới và chạy lại báo cáo. Trước đó giữ R7 và số đo, không thêm box L. Findings R7 có E0_reference_defect/action=escalate; decision DIAG-01.

## Ticket 2 — Output model khác taxonomy và policy rider

- **Frame:** adasind_062370.jpg: M5/M8/M10 Truck, M3/M4 Pedestrian; adasind_069450.jpg: M5/M7 Truck; 117120: M7 Truck, M1 Truck trên SUV và M6 Pedestrian trên rider.
- **Ảnh chụp:** [screenshots/06-model-taxonomy.png](screenshots/06-model-taxonomy.png), [nhãn người học để đối chiếu](screenshots/03-b2-van.png); thêm r3_diag/model_compare.html.
- **Expected impact:** Sáu ThreeWheeler bị model gọi Truck, tạo các cặp LR_noM/M_only khi ghép cùng class; ba rider bị tách thành Pedestrian. Đếm các dòng này như các vật độc lập sẽ phóng đại số lỗi. Tín hiệu lặp trên ba frame gợi ý lệch taxonomy/miền mục tiêu, chưa chứng minh méo fisheye là nguyên nhân.
- **Owner:** ai_team.
- **Recommendation:** Kiểm tập class gốc, mapping sang sáu class và policy rider trước khi quy kết domain shift. Review thêm cảnh ở center/mid/edge và các điều kiện che khuất. Không đổi nhãn người học thành Truck/Pedestrian để giống model. Findings liên quan có E4_model_domain dưới dạng giả thuyết và action=escalate; decision DIAG-02.

## Ticket 3 — C0: tư thế người áo vàng bị blur che

- **Frame:** adasind_019560.jpg, L2/L8.
- **Ảnh chụp:** [screenshots/02-c0-rider.png](screenshots/02-c0-rider.png).
- **Expected impact:** Nếu là rider thì một Bike; nếu đang dắt xe thì Pedestrian và Bike riêng theo R03. Reference không khớp L8 không tự chứng minh việc giữ/xóa L2 đúng.
- **Owner:** qa.
- **Recommendation:** Phân xử trên ảnh có quyền dùng phù hợp hoặc frame lân cận nếu được cung cấp; không yêu cầu gỡ blur riêng tư. Khi vẫn không rõ, giữ E5_unresolved và mô tả giới hạn. L8 chỉ ôm một phần xe nên cần xem cùng L2 trước khi sửa. Findings C0 L8 action=escalate; decision CAL-01.

## Ticket 4 — 117120: vật thật thiếu trong reference và class chưa rõ

- **Frame:** adasind_117120.jpg; L3 Bus, L7 ThreeWheeler; M8 Car/M10 Truck cùng vị trí với L3.
- **Ảnh chụp:** [screenshots/07-job30-frame3.png](screenshots/07-job30-frame3.png); xem thêm r3_diag/model_compare.html. XML5 tương ứng L3; XML10 tương ứng L7.
- **Expected impact:** Hai nhãn bị tính spurious/FP so với reference nhưng ảnh có phương tiện thật. Xóa để tăng precision có thể bỏ vật hợp lệ. Model còn có hai box khác class gần trùng cho cùng phương tiện.
- **Owner:** qa; phối hợp ai_team cho M8/M10.
- **Recommendation:** Soát phương tiện nhỏ cao khoảng 49 px để phân xử Bus/Car/Truck, kiểm reference có thiếu không; soát box/occluded của ThreeWheeler bị ô tô phía trước che. Giữ nhãn người học khi chưa đủ căn cứ; E5 cho L3, nghi E0 cho L7. Không tự nhận reference là gold. Findings các dòng này action=escalate; quyết định JOB30-03.
