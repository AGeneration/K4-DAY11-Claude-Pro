# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

*Bản nháp P0 — sẽ bổ sung lý do từ lỗi thật sau P4.*

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Người đi bộ/xe hai bánh cắt ngang sát xe; vật bị vòng kính cắt ở rìa; ngược sáng | Vật ở rìa fisheye bị méo và truncated; rider và xe hai bánh dễ tách nhầm thành hai box | Nhãn trên ảnh fisheye gốc, ghi phiên bản calibration front và rules v1.0.0 | Hai người gán độc lập, người thứ ba phân xử các ca khác nhau theo luật và ghi lý do |
| rear | Vật thấp/trẻ em sát cản sau; ban đêm với đèn lùi | Thân xe ego che một phần, dễ nhầm vật với `ignore_region` | Giữ polygon `ego_body` cố định theo calibration rear; nhãn trên ảnh gốc | Soát riêng ranh giới ego_body và vật sát xe trên ảnh gốc trước khi khoá |
| left | Vùng seam trước-trái/sau-trái; xe máy vượt sát; vạch đỗ méo ở rìa | Một vật có thể hiện ở hai camera với hai box và hai zone khác nhau | Timestamp đồng bộ và extrinsic giữa left–front/left–rear | Kiểm cùng timestamp trên camera kề trước khi quyết định trùng hay hợp lệ |
| right | Người trên vỉa hè bị che; curb và vạch đỗ khi đỗ song song; seam trước-phải | Occluded/truncated nhiều, curb dễ bị gán nhầm là vạch đỗ | Timestamp đồng bộ và extrinsic giữa right–front/right–rear; luật parking_line | Người soát xác nhận từng ca occluded và từng vạch trên ảnh gốc |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): khi thay camera/lens hoặc vị trí gắn, khi
  calibration được làm lại (vòng kính, ego_body hoặc seam thay đổi), khi rules đổi phiên bản làm đổi định nghĩa class
  hoặc ignore, và khi dữ liệu mới có điều kiện chưa có trong gold (đêm, mưa, địa điểm mới).
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: một xe máy ở góc trước-phải thấy cả trên
  camera front (ở zone `edge`) và camera right (ở zone `mid`) cùng timestamp. Cần calibration để chiếu hai box về cùng
  không gian và policy đích (giữ cả hai box theo từng camera hay ghép một object trên BEV) trước khi gọi là
  `DUPLICATE`.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera:
  ADASIND chỉ có một camera, nên agreement ở đây không đo được lỗi seam, đồng bộ thời gian hay ghép track qua camera.
  Hai người cũng có thể đồng thuận cùng sai theo một luật chưa rõ. Mỗi camera có ego_body, góc nhìn và loại hard case
  riêng, nên phải kiểm riêng từng camera và cả cặp camera kề nhau.
