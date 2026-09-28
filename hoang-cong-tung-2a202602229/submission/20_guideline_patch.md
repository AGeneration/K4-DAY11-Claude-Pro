# Guideline patch

- **Rule mới đề xuất:** Khi nhiều vật (người đi bộ, xe) đứng sát nhau đến mức mỗi box riêng phải vẽ rất hẹp (<25px chiều rộng) để tách biệt, annotator nên **thử vẽ box đủ khổ vật thật trước** (không giới hạn theo khoảng trống giữa các vật); chỉ chuyển sang `ignore_region reason=crowd_or_group` khi ranh giới giữa các vật không còn phân biệt được bằng mắt trên ảnh gốc (bị chồng lấn/che hoàn toàn vào nhau), không phải chỉ vì các box nằm gần nhau.
- **Áp dụng cho:** Class `Pedestrian`/`Bike`/`ThreeWheeler` khi ở cụm đông, và lựa chọn giữa box riêng lẻ với `ignore_region (reason=crowd_or_group)`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R06 chỉ định nghĩa `crowd_or_group` là "cụm vật không tách được từng cái", nhưng không nói rõ ngưỡng nào (khoảng cách, độ che phủ) để quyết định "không tách được". Ở slice B2-mid, tôi từng xóa nhầm 2 box người đi bộ thật (đã có sẵn trong prefill) và không mở rộng 1 box khác vì tưởng chúng quá mảnh/khó tách — trong khi thực tế cả 5 vật trong cụm đều tách biệt được khi nhìn kỹ trên ảnh gốc (xem `findings.csv` dòng `R5+M4`, `R6+M8`, `R7+M6`, `R9`, `R10+M5`, round `r3_diag`, frame `adasind_060000.jpg`).
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** Round `r3_diag`/`rework` trở đi (áp dụng ngay khi rework slice của mình); đề xuất áp dụng cho P2 của các lượt học sau.
