# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 12 | 2 | 6 | 4 | 7 | SPURIOUS (5) |
| mid | 5 | 0 | 0 | 2 | 4 | — |
| edge | 3 | 0 | 0 | 1 | 1 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: **center** ở cả hai phía — L có 2 missing + 6 spurious trên 12 box reference, M có 4 missing + 7 thừa; mid và edge của L đều 0/0, M ở mid 2 missing + 4 thừa, edge 1 + 1. Nhưng "gãy" của L ở center không cùng một nguyên nhân: soi từng ca trên ảnh thì chỉ 1 missing là lỗi của mình (R10 người áo vàng 271039, E1); missing còn lại là R1 295948 do reference gọi xe tải nhỏ là Car (E0, R04). Trong 6 spurious: 3 ca reference thiếu vật nhìn thấy rõ (271039 L2 xe máy, L8 e-rickshaw, L13 người — L13 được model thấy cùng), 1 ca do polygon unreadable của reference chỉ phủ nửa người (L14, E2) và 1 ca chưa phân xử (L1 xe ba bánh bị che, E5); cả 6 đều ở 271039 — frame đông người đi bộ và xe đỗ chồng lên nhau.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: ở slice này lỗi **không** đến từ méo rìa — ca khó nằm ở center vì đó là chỗ vật bị che chồng (dãy xe ba bánh đỗ sau người đi bộ ở 271039). Lỗi của M có một mẫu lặp rõ: model không sinh box ThreeWheeler nào, gọi xe ba bánh là Car/Truck (270517 M6/M7/M9, 271039 M9/M11/M12, và C0 M7/M8), và box người ngồi trong xe ba bánh (270517 M5/M10/M11, trái R03) — giả thuyết là lệch taxonomy/miền dữ liệu (E4), cần kiểm trên 48 frame bằng cách đếm lớp M ghép với mọi R ThreeWheeler. Model còn box người lái ego ở 295948 (Pedestrian [0,1200,232,1712]), khớp tín hiệu tổng hợp "ego_body 49" của report pre-label. Giới hạn: chỉ 3 frame, 20 box reference (edge chỉ 3), nên bảng zone không đủ để kết luận zone nào khó hơn; ngưỡng H=40 và IoU 0.5 thay đổi số (iou_sweep: ở 0.7, L mid rớt từ 5 xuống 3 matched); teaching reference có ít nhất 1 lỗi phạm vi P0 (ego_body chữ nhật ở 295948 loại khỏi phép so 4 box của mình và 6 box của model), nên số đo ở 295948 không đáng tin.
