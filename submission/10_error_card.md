# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | BOX_GEOMETRY | 1 |
| center | B4 | IGNORE_SCOPE | 1 |
| center | B4 | MISSING | 5 |
| center | B4 | SPURIOUS | 16 |
| center | B4 | WRONG_CLASS | 2 |
| center | C0 | SPURIOUS | 1 |
| center | C0 | WRONG_CLASS | 1 |
| edge | B4 | MISSING | 1 |
| edge | B4 | SPURIOUS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B4 | IGNORE_SCOPE | 4 |
| mid | B4 | MISSING | 2 |
| mid | B4 | SPURIOUS | 5 |
| mid | B4 | WRONG_CLASS | 2 |
| unknown | B4 | MISSING | 1 |
| unknown | C0 | IGNORE_SCOPE | 1 |

## Top defects
- SPURIOUS: 23 (ví dụ frame adasind_019560.jpg)
- MISSING: 9 (ví dụ frame adasind_270517.jpg)
- WRONG_CLASS: 6 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

Lỗi nổi bật nhất theo bảng là **SPURIOUS (23)**, tập trung ở `center` của B4 (16). Mình tách nó theo *ai* thấy box
trước khi hỏi *vì sao*, vì con số gộp ba nguồn khác nhau:

- **Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy:**
  - *Phần lớn SPURIOUS thuộc model (M_only):* 270517 M5/M10/M11 là người lái và hành khách **ngồi trong** xe ba bánh
    (trái R03); 270517 M6/M7/M9 và 271039 M9/M11/M12 là xe ba bánh bị gọi `Car`/`Truck`, thành cặp FP (class sai) + FN
    (ThreeWheeler thiếu). Cùng mẫu đã thấy ở C0 (M7/M8 Truck, M1+M2 và M4+M5 tách rider). Model không sinh box
    `ThreeWheeler` nào trên 4 frame đã xem → giả thuyết `E4_model_domain` (lớp này và quy ước rider/người-trong-xe không
    có trong dữ liệu huấn luyện của model), có bằng chứng từ ≥9 box ở 3 frame chứ không từ một box lệch. Phép kiểm tiếp:
    đếm class M ghép với mọi `ThreeWheeler` của reference trên 48 frame.
  - *SPURIOUS của L ở 271039 (6 ca) phần lớn không phải lỗi người gán:* L2 xe máy, L8 e-rickshaw, L13 người là vật nhìn
    thấy mà teaching reference thiếu (`E0_reference_defect`; L13 được model thấy cùng); L14 là do polygon `unreadable`
    của reference chỉ phủ nửa người (`E2_guideline_gap`); L1 xe ba bánh bị che chưa đủ bằng chứng (`E5_unresolved`,
    cần frame kề).
  - *Lỗi thật của mình:* 271039 R10 (người áo vàng, `MISSING`) — nhầm áo vàng với mui xe ba bánh vàng phía sau khi
    vùng này có 5 người và 3 xe chồng nhau; và 270517 L8 đoán class cho một vật mờ cao 42 px thay vì dùng `unreadable`
    (`E1_annotator_error`). Cả hai là ca che khuất dày ở `center`, không phải méo rìa.
- **Cách sửa và ai nhận việc (`owner`):** `annotator` — đã rework hai ca E1 (center missing 2 → 1, xem `rework/delta.md`),
  và từ nay soát riêng từng người trong cụm che khuất bằng crop ≥4x trước khi khoá. `qa` — sửa teaching reference theo
  escalation Ticket 1 (ego_body chữ nhật 295948, P0) và Ticket 2 (vật thiếu 271039, Car→Truck 295948). `guideline` —
  R12 trong `20_guideline_patch.md` (ignore phải bao trọn vật; làm rõ người trên xe ego). `ai_team` — không dùng pre-label
  YOLO26m làm class `ThreeWheeler` hay cho người trong xe; lọc box `Pedestrian` nằm trong box xe trước khi prefill.
- **Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule):** `screenshots/02_271039_center_conflicts.png` (L2, L8,
  L13, L14, R10 — R01/R09), `screenshots/01_295948_ref_ego_body_rectangle.png` (R07/R10),
  `screenshots/03_295948_pickup_truck_vs_car.png` (R04, và M6 là gương xe tải); các dòng `r3_diag` của 270517 và
  271039 trong `findings.csv`; `r3_diag/model_compare.md`. Giới hạn: 3 frame + 1 frame C0, nên tỷ lệ theo zone chỉ là
  mô tả của slice này.
