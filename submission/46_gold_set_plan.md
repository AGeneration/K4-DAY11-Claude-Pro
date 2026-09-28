# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

*Bản P6 — bổ sung từ lỗi thật ở P1–P5 (C0 và slice B4-center). Tình huống bốn camera vẫn là giả lập; ADASIND chỉ có một
camera nên không thay được camera nào trong bảng.*

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Người đi bộ/xe hai bánh cắt ngang sát xe; cụm người + xe ba bánh che nhau ở giữa khung; vật bị vòng kính cắt; ngược sáng. **Normal** (20): đường thông thoáng, vật ở xa gần H=40 | Ranh giới "ngồi trên xe" và "dắt/đứng cạnh xe" (R03) dễ sai ở cả người lẫn model (C0: model tách đúng người áo đỏ dắt xe nhưng tách sai người áo vàng đang ngồi; reference gộp cả hai); xe ba bánh bị gọi Car/Truck; trong cụm che khuất người gán bỏ sót từng người (271039 R10) | Nhãn trên ảnh fisheye gốc front, vòng kính (cx, cy, r) và `lens_border` theo calibration front, rules v1.1.0 nếu R12 được duyệt | Hai người gán độc lập; người thứ ba phân xử từng khác biệt trên crop ≥4x, đếm từng người trong cụm; ghi rule và lý do vào decision log |
| rear | Trẻ em/vật thấp sát cản sau; ban đêm với đèn lùi; vật một phần nằm sau thân xe. **Normal** (20): lùi chậm, vật ở giữa khung | Polygon `ego_body` dễ phủ lấn vật thật; P4 thấy reference dùng `ego_body` chữ nhật che 4 vật (295948) | Polygon `ego_body` cố định theo calibration rear (vị trí gắn, góc), kiểm lại khi đổi xe/giá gắn; nhãn trên ảnh gốc | Soát riêng ranh giới `ego_body` trước khi soát box: không polygon ego nào chứa trọn một box; người soát ký xác nhận từng frame |
| left | Seam trước-trái/sau-trái; xe máy vượt sát; người trên xe hai bánh sát thân xe; vạch ô đỗ méo ở rìa. **Normal** (15): mặt đường, xe đỗ cạnh | Một vật có hai box ở hai camera; người sát camera bị vòng kính cắt dễ bị coi là ego (295948 L4) hoặc bị model bỏ sót | Timestamp đồng bộ, intrinsic + extrinsic left và cặp left–front, left–rear; vùng seam định nghĩa bằng calibration | Kiểm cùng timestamp trên camera kề trước khi quyết định trùng hay hợp lệ; ca seam chưa có policy giữ ở trạng thái "cần phân xử", không vào gold |
| right | Seam trước-phải/sau-phải; dãy xe đỗ + người trên vỉa hè che nhau; curb và vạch đỗ khi đỗ song song. **Normal** (15): lề đường thông thoáng | Occluded dày; polygon `unreadable` vẽ nửa vời làm cùng một người thành FP hoặc don't-care (271039 L14); curb dễ gán nhầm là vạch đỗ | Timestamp và extrinsic right, right–front, right–rear; luật `parking_line` (vai trò chia ô, không theo màu sơn) | Người soát xác nhận từng ca occluded/unreadable (polygon bao trọn vật) và từng vạch trên ảnh gốc |

**Cách chọn mẫu và người rà trước khi gọi là gold:**

- Chọn theo clip rồi mới theo frame (1–2 frame/clip, cách nhau theo thời gian) trong từng ô `camera × normal/hard` ở
  `45_sampling_plan.csv`; hard được chọn theo danh sách tiêu chí ở bảng trên, không chọn ngẫu nhiên.
- Mỗi frame: **hai người gán độc lập** trên CVAT, khoá export trước khi xem bản của nhau (như lock → reference của lab);
  người thứ ba (không gán frame đó) phân xử mọi khác biệt theo rule, ghi `rule_id` + lý do. Khác biệt do luật chưa đủ
  thì đưa về `guideline` (như R12) rồi gán lại, không phân xử bằng đa số.
- Chỉ gọi là gold khi: hết khác biệt chưa phân xử, `ego_body`/`lens_border` đã soát theo calibration của đúng camera,
  và một lượt kiểm tự động (không box ≥50% trong ignore, không ego chứa trọn box, class thuộc 6 lớp, `truncated` khớp
  vòng kính) sạch.

**Calibration / timestamp và một ca seam cần policy:** gold phải lưu kèm `camera_id`, timestamp đồng bộ, phiên bản
calibration (intrinsic + extrinsic, vòng kính) và phiên bản rules. Ca seam: một xe máy ở góc trước-phải thấy cùng
lúc trên camera front (zone `edge`, `truncated` bởi vòng kính) và camera right (zone `mid`). Hai box đều hợp lệ trên
ảnh gốc của từng camera; chỉ ghép thành một object (hoặc coi là `DUPLICATE`) khi có timestamp khớp, calibration để
chiếu về cùng không gian/BEV và policy output đích đã được duyệt.

- **Khi nào cần refresh gold set (đổi camera, calibration hoặc rule):** khi thay camera/lens hoặc vị trí gắn; khi
  calibration được làm lại (vòng kính, `ego_body` hoặc seam thay đổi); khi rules đổi phiên bản làm đổi định nghĩa class
  hoặc ignore (ví dụ duyệt R12 → phải soát lại mọi polygon `unreadable`/`crowd_or_group` đã có); khi dữ liệu mới có
  điều kiện chưa có trong gold (đêm, mưa, địa điểm/loại xe mới như xe ba bánh ở thị trường khác); và khi một lỗi
  reference được escalate và xác nhận (như Ticket 1–2) thì soát lại mọi frame cùng người rà hoặc cùng kiểu lỗi.
- **Giới hạn của reference hiện tại:** teaching reference ADASIND là bản nháp sửa tay của một người, không phải gold. Chỉ
  riêng slice B4-center đã thấy một lỗi phạm vi P0 (`ego_body` chữ nhật 295948), ba vật nhìn thấy bị thiếu (271039 L2,
  L8, L13), một sai class theo R04 (xe tải nhỏ → `Car`) và một polygon `unreadable` phủ nửa người. Vì vậy
  `local-quality` (micro precision 0.750, recall 0.900 trên 3 frame) chỉ đo độ khớp với bản nháp này.
- **Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera:**
  ADASIND chỉ có một camera, nên agreement ở đây không đo được lỗi seam, đồng bộ thời gian hay ghép track qua camera.
  Hai người cũng có thể đồng thuận cùng sai theo một luật chưa rõ (như polygon `unreadable` chỉ phủ một phần vật). Mỗi
  camera có `ego_body`, góc nhìn và loại hard case riêng, nên phải kiểm riêng từng camera và cả cặp camera kề nhau.
