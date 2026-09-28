# Guideline patch

Đây là **đề xuất** sửa `docs/02-rules-vi.md` (không sửa trực tiếp file đó). Áp dụng cho 6 class động của lab — tập
con của taxonomy ADASIND gốc.

- **Rule mới đề xuất:** **R12 — Hình học của `ignore_region` không phải thân xe/vành kính.** Polygon
  `reason=unreadable` hoặc `crowd_or_group` phải bao **trọn phần nhìn thấy** của vật (hoặc cả cụm) mà nó thay thế, không
  chỉ một phần thân. Nếu một phần vật vẫn đọc được class và cao ≥ H=40 px, vẽ box với `occluded=true` thay vì ignore.
  Không vẽ `unreadable` chồng một phần lên box của vật khác. Kèm theo, **làm rõ R03/R07:** người lái/người ngồi trên
  chính xe gắn camera thuộc `ego_body`; người trên một xe hai bánh khác sát bên theo R03. Người đang **ngồi trên yên**
  (kể cả khi dừng, một chân chống đất) là rider → một `Bike`; người **đứng** cạnh hoặc đứng dạng chân qua xe, cả hai
  bàn chân trên mặt đất và không ngồi trên yên → `Pedestrian` + `Bike`. Khi ảnh tĩnh không phân biệt được, ghi
  `E5_unresolved` và kiểm frame kề thay vì đoán.
- **Ví dụ:** `adasind_271039.jpg`, người áo sọc trắng [432,814,465,892] đứng sau xe máy đỗ. Teaching reference vẽ
  `unreadable` chỉ trên thân [436–462, 824–872]. Hệ quả: box của mình (33×78 px) nằm 48% trong ignore nên bị tính
  SPURIOUS, box của model (30×77 px) nằm 54% nên thành don't-care — cùng một người, kết quả đảo chiều chỉ vì 2–3 px
  bề rộng box (findings `r3_diag` L14, `why=E2_guideline_gap`). Ví dụ cho phần R03/R07: `adasind_295948.jpg` người quấn
  khăn caro sát camera [574,606,1080,1726] — `r1_craft` gán một `Bike`, bản rework tách `Pedestrian` + `Bike` vì bàn
  chân chạm đất, reference giữ một `Bike` (findings `rework` L1+R3, `E2_guideline_gap`; decision log D4, D8); và C0
  `adasind_019560.jpg` người áo đỏ dắt xe máy (L8 + L7) mà reference gộp thành một `Bike`.
- **Áp dụng cho:** `ignore_region` với `reason` `unreadable` và `crowd_or_group`; attribute `occluded`; mọi zone
  (`center/mid/edge`), đặc biệt vùng center đông người như 271039. Phần làm rõ R07 áp dụng cho `ego_body` và `Bike`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R06 chỉ liệt kê lý do hợp lệ, R09 chỉ nói ngưỡng 50%,
  nhưng không luật nào nói polygon ignore phải phủ tới đâu. Khi polygon chỉ phủ một phần vật, ngưỡng 50% của R09 biến
  một quyết định hình học rất nhỏ thành TP/FP/don't-care khác nhau, và L với M bị chấm khác nhau cho cùng một vật. R07
  nói "thân xe/gương/tay lái" nhưng ảnh ADASIND cho thấy người lái ego (270517, 295948) mới là phần chiếm khung nhiều
  nhất; luật chưa nói người ở sát camera là ego hay road user. R03 chỉ phân biệt "ngồi lên" và "dắt", chưa nói ca đứng
  dạng chân/đang dừng — chính ca này mà người gán, reference và model trả lời khác nhau ở C0 và 295948.
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** vòng `rework` kế tiếp và mọi lần sửa teaching reference sau khi escalation Ticket 2 được xử lý;
  không áp ngược lên bản `r1_craft` đã khoá (34BC-63D5).
