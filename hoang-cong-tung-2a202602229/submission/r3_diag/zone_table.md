# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 9 | 3 | 2 | 5 | 8 | MISSING (3) |
| mid | 8 | 3 | 0 | 4 | 10 | MISSING (3) |
| edge | 3 | 0 | 0 | 2 | 0 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: Phía người gán nhãn (L), zone `center` và `mid` gãy bằng nhau (missing=3 mỗi zone), zone `edge` không thiếu vật nào (missing=0). Phía model, `mid` thừa nhiều nhất (10 box thừa) và `center` vừa thiếu nhiều nhất (5) vừa thừa nhiều (8); `edge` model chỉ thiếu 2, không thừa.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Khác với giả định thường gặp là vùng `edge` (rìa, méo nhiều) khó nhất, ở slice này toàn bộ 3 vật `L missing` đều nằm trong một cụm người/xe đứng sát nhau ở `center`/`mid` của frame 1 — nguyên nhân nhiều khả năng là mật độ vật cao và kích thước từng vật quá nhỏ để tách rõ ràng, không phải do méo ống kính ở rìa. Số box thừa cao của model ở `mid`/`center` phù hợp với cùng giả thuyết: vùng đông vật khiến model tách nhầm hoặc phát hiện nhầm chi tiết nền thành vật — đây là giả thuyết cần thêm bằng chứng từ nhiều slice khác mới kết luận chắc (E4_model_domain), không suy diễn chỉ từ 3 frame. Giới hạn rõ của slice: chỉ 20 vật tham chiếu trên 3 frame, quá ít để đại diện cho toàn bộ camera hay các slice khác của lớp; số liệu ở đây chỉ mô tả cục bộ theo quy tắc lab, không phải điểm rubric hay bằng chứng gold set.
