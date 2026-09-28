# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 13 | 4 | 3 | 6 | 7 | MISSING (3) |
| mid | 5 | 1 | 1 | 2 | 3 | WRONG_CLASS (1) |
| edge | 2 | 0 | 0 | 1 | 2 | — |

## Nhận xét

- **Phạm vi:** Đủ 062370, 069450 và 117120 từ ZIP job30; đã bỏ giảm frame3. Bảng trên do model tính, không sửa tay. Tất cả báo cáo lần này cùng dùng ba frame.
- **Nhãn L:** Center 4 missing/3 spurious trên 13 reference; mid 1/1 trên 5; edge 0/0 trên 2. Center có nhiều sai khác nhất theo số tuyệt đối, gồm geometry, vật bị che, một reference nghi trùng và hai nhãn có vật thật nhưng reference không có. Không suy khoảng cách tới xe hoặc mức an toàn từ zone.
- **Model M:** Center 6 missing/7 thừa; mid 2/3; edge 1/2. Ghép cùng class tạo LR_noM/M_only khi ThreeWheeler/Car bị M gọi Truck; các mã này không tự chứng minh có hai vật khác nhau. Sáu ca ThreeWheeler/Truck và ba ca tách rider hỗ trợ giả thuyết lệch taxonomy/miền, cần kiểm mapping và thêm dữ liệu.
- **Local-quality L/R:** TP=15, FP=4, FN=5; precision=0.789, recall=0.750, micro accuracy=0.652, mean IoU của TP=0.843. Truck có 0 TP, 1 FP và 1 FN; van L4/R4 ghép hình học IoU=0.967 nhưng sai class, tạo FP Truck/FN Car. Bus có một FP so với reference nhưng vật tại 117120 thực sự xuất hiện; class và reference đang escalation, không coi FP là đủ chứng cứ xóa.
- **Ca sát H=40:** Box Car XML2 trong 117120 cao 37.43 px bị loại khỏi matcher, nên R3/M5 xuất hiện RM_noL. Soát ảnh thấy vật cao khoảng 43 px, cần sửa box vẽ thiếu. XML3/XML6 nhỏ hơn ngưỡng thật thì bỏ. Hình học nhãn và phạm vi vật cần được kiểm cùng nhau.
- **IoU sweep:** Tổng L matched=16/15/13 tại 0.3/0.5/0.7; M=11/11/7. Siết ngưỡng làm geometry gần ranh mất match; không chữa được sai class hoặc policy rider bằng cách chỉ hạ IoU.
- **Attribute và giới hạn:** 069450 L1/R1 khác edge_zone nhưng vẫn là TP hình học; không suy ra occluded/ignore.reason sai. Ba frame không đại diện 48 ảnh hay bốn camera; teaching reference có thể sai và không phải gold. Các polygon và tracking không nằm trong phép đo rectangle này.
