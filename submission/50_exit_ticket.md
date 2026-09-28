# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao?

   **Cần một quy tắc riêng, mặc định không phải `DUPLICATE`.** `DUPLICATE` trong lab nghĩa là hai box cho một vật **trên
   cùng một ảnh**. Ở seam, mỗi camera là một ảnh fisheye gốc khác nhau, và R02 yêu cầu box bám phần nhìn thấy trên
   *ảnh gốc của camera đó*, nên một xe máy ở góc trước-phải có một box ở camera front (có thể ở zone `edge`,
   `truncated` bởi vòng kính) và một box ở camera right (zone `mid`) là **hai nhãn hợp lệ**. Chỉ gọi là trùng khi có
   policy output đích nói rõ (ví dụ "một object trên BEV") **và** chứng minh được đó là cùng vật: timestamp đồng bộ
   giữa hai camera, calibration (intrinsic + extrinsic) để chiếu hai box về cùng không gian, và ngưỡng chồng lấn đã
   thống nhất. Thiếu một trong ba thứ đó thì giữ cả hai box, ghi ca vào danh sách seam cần người soát — không xoá box
   nào. Lỗi `DUPLICATE` thật vẫn là hai box cùng class cho một vật trong **cùng một camera** (như check IoU > 0.7 của
   self-QC).

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.

   **Giữ cùng track ID** khi vẫn là cùng một vật và nó còn quan sát được liên tục, kể cả khi bị che một phần
   (`occluded`) hay đổi zone từ `center` sang `edge`. **Thêm keyframe** khi hình học đổi đủ lớn để nội suy sai — trên
   fisheye điều này xảy ra nhanh ở rìa: một xe tới gần vành kính bị méo cong và bị vòng kính cắt (`truncated`), nên cần
   keyframe dày hơn ở `edge` so với `center`; cũng thêm keyframe khi attribute đổi (bắt đầu bị che, bắt đầu bị cắt).
   **Đặt Outside** khi vật rời trường nhìn hữu ích (ra ngoài vòng kính, đi vào vùng `lens_border`/`ego_body`, hoặc bị
   che hoàn toàn) theo guideline của task; khi vật xuất hiện lại mà không chắc là cùng vật thì mở track mới thay vì
   đoán. **Trước khi nối track qua hai camera** cần: timestamp đồng bộ của hai luồng, calibration để chiếu vị trí về
   cùng hệ toạ độ (BEV hoặc toạ độ xe), vùng seam đã định nghĩa, policy output (track riêng theo camera hay một track
   toàn cục) và ít nhất vài ca đã được người soát xác nhận cùng vật — ảnh tĩnh một camera như ADASIND không cung cấp
   bằng chứng nào trong số này.

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?

   Ở `adasind_295948.jpg`, mình gán xe tải nhỏ thùng hở `L6` [460,890,655,1062] là `Truck`, còn teaching reference gán
   `Car` (`R1`) — compare báo `WRONG_CLASS` và local-quality tính một cặp Car→Truck. Mình không đổi nhãn cho khớp: soi
   lại trên ảnh thấy cabin nhỏ và thùng hàng hở phía sau, R04 xếp xe bán tải nhỏ vào `Truck`, và model đóng băng cũng
   gán `Truck` (M2). Mình ghi `why=E0_reference_defect`, `action=escalate` trong `findings.csv`, `status=escalated`
   trong decision log (D7), kèm `screenshots/03_295948_pickup_truck_vs_car.png` và Ticket 2. Nếu làm lại, điều mình đổi
   là cách soát **cụm che khuất dày** chứ không phải ca này: ở `adasind_271039.jpg` mình bỏ sót người áo vàng (`R10`)
   vì nhìn cả cụm ở độ phóng 3x và coi áo vàng là mui xe ba bánh. Lần sau mình sẽ đếm từng người trong cụm ở crop ≥6x
   và đối chiếu số đầu/số cặp chân trước khi khoá, và dùng `unreadable` ngay khi class chỉ đoán được từ hình dạng mờ
   (như `L8` ở 270517) thay vì chọn một class.
