# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Người đi bộ/xe băng ngang gần ống kính, ánh sáng ngược | Méo fisheye ở rìa làm biến dạng hình dạng vật, dễ bỏ sót box nhỏ; ngược sáng làm mất viền vật thể | Giữ toạ độ pixel gốc (chưa dewarp), calibration lens không đổi giữa các lần chụp | Hai người gán độc lập, so IoU rồi đọc từng ca khó trên ảnh gốc trước khi chốt |
| rear | Vật cản thấp (trẻ em, cọc tiêu, xe đạp) khi lùi xe | Vật thấp dễ lọt ngoài box do góc nhìn từ trên xuống, dễ bị `ego_body` che | Giữ vị trí gắn camera và vùng `ego_body` nhất quán giữa các lần chụp | So với teaching reference, kiểm riêng nhóm vật cao <40px |
| left | Xe máy/xe đạp vượt trong điểm mù, vật ở vùng seam góc trước/sau-trái | Seam khiến một vật xuất hiện ở hai camera, dễ đếm trùng hoặc gán track sai nếu thiếu calibration ghép | Giữ toạ độ và timestamp đồng bộ giữa left và front/rear | Soát riêng các ca seam, chưa gán chung `track_id` nếu thiếu policy ghép |
| right | Người đi bộ sát lề, vật ở vùng seam góc trước/sau-phải | Tương tự left, thêm rủi ro nhầm hướng do ảnh bên phải hay bị soát ẩu hơn bên trái | Giữ toạ độ và timestamp đồng bộ giữa right và front/rear | Soát riêng các ca seam, đối chiếu cùng quy tắc như bên trái |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): Khi đổi vị trí/góc gắn camera, đổi calibration lens, đổi rule gán nhãn (ví dụ ngưỡng 40px hay định nghĩa ignore_region), hoặc khi review sau phát hiện nhiều lỗi hệ thống lặp lại trên cùng một camera.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: Cần timestamp đồng bộ giữa hai camera và calibration extrinsic (vị trí/góc tương đối giữa hai camera) xác nhận cùng một vật lý; nếu thiếu một trong hai, giữ hai box riêng biệt, không tự gán chung `track_id`.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: Mỗi camera có đặc thù méo ảnh, góc nhìn và điều kiện ánh sáng khác nhau (ví dụ rear thường gặp vật thấp, left/right gặp seam); đồng thuận tốt trên một camera không kiểm chứng được rule áp dụng đúng cho vùng đặc thù của ba camera còn lại.
