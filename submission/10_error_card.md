# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | BOX_GEOMETRY | 2 |
| center | B2 | IGNORE_SCOPE | 1 |
| center | B2 | MISSING | 10 |
| center | B2 | SPURIOUS | 12 |
| center | C0 | SPURIOUS | 2 |
| edge | B2 | MISSING | 1 |
| edge | B2 | WRONG_CLASS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B2 | MISSING | 11 |
| mid | B2 | SPURIOUS | 10 |
| mid | B2 | WRONG_CLASS | 1 |
| unknown | B2 | BOX_GEOMETRY | 1 |

## Top defects
- SPURIOUS: 24 (ví dụ frame adasind_019560.jpg)
- MISSING: 22 (ví dụ frame adasind_060000.jpg)
- WRONG_CLASS: 3 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Phần lớn SPURIOUS/MISSING (khoảng 30/46 dòng) đến từ so sánh với **model** (`M_only`, `LR_noM`) — model YOLO26m tự sinh nhiều box không có thật (`E4_model_domain`) hoặc bỏ sót vật mà cả người gán nhãn và reference đều đồng thuận, không phải lỗi nhãn của tôi. Phần MISSING đáng kể còn lại (5 ca) tập trung ở một **cụm người đi bộ + xe sát nhau** tại rìa trái frame `adasind_060000.jpg` — tôi cho là `E2_guideline_gap` vì luật hiện tại không nói rõ khi nào nên tách nhiều box mảnh, khi nào nên gộp `ignore_region crowd_or_group`; ban đầu tôi xóa nhầm một số box thật trong cụm này vì nghi ngờ là bấm nhầm. 3 ca `WRONG_CLASS` gồm 1 lỗi thật của tôi ở vòng calib (xe ba bánh gán nhầm `Car`, đã rút kinh nghiệm cho slice chính) và 1 ca bất đồng có chủ đích với reference (frame `adasind_102750.jpg`, vật ở x≈88–169: tôi xác nhận trực tiếp trên ảnh gốc là `Truck`, dù reference và gợi ý K12 ghi `ThreeWheeler`).
- Cách sửa và ai nhận việc (`owner`): Các ca do model (`owner=ai_team`) không cần sửa nhãn, chỉ ghi nhận hạn chế. Cụm bị bỏ sót (`owner=guideline`, đề xuất bổ sung luật ở `20_guideline_patch.md`) đã được tôi tự sửa (`action=rework`) ở P5 — đã thêm đủ 5 box còn thiếu và khóa lại bản `rework`. Ca bất đồng Truck/ThreeWheeler giữ nguyên quyết định của tôi (`action=keep_with_reason`, `owner=annotator`) vì không có ai đối chứng ngay lúc này; đề xuất người soát độc lập xem lại nếu có dịp.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `findings.csv` các dòng round `r3_diag` và `rework` cho slice B2-mid; `submission/rework/delta.md` cho thấy số matched tăng từ 6→9 (center) và 5→8 (mid), missing về 0 ở cả hai zone sau khi sửa. Rule liên quan: R01 (ngưỡng 40px), R04 (ánh xạ Car/Truck/ThreeWheeler), R06 (lý do `ignore_region`).
