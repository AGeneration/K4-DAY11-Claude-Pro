# Escalation ticket

## Ticket 1

- **Frame:** adasind_060000.jpg
- **Ảnh chụp:** submission/screenshots/01_060000_crowd_cluster.png
- **Expected impact:** Nếu không làm rõ ngưỡng, học viên khác gặp cụm vật đông đúc tương tự (người đi bộ/xe sát nhau ở center/mid) nhiều khả năng sẽ xóa nhầm hoặc bỏ sót các vật thật giống tôi ở slice B2-mid — làm lệch số liệu zone `center`/`mid` một cách hệ thống, không chỉ riêng slice này (xem `findings.csv` round `r3_diag`, 5 dòng `R5+M4`/`R6+M8`/`R7+M6`/`R9`/`R10+M5`).
- **Owner:** guideline
- **Recommendation:** Bổ sung vào `docs/02-rules-vi.md` một tiêu chí cụ thể (ví dụ: dựa trên việc ranh giới từng vật còn phân biệt được bằng mắt trên ảnh gốc hay không, không dựa trên khoảng cách/kích thước box) để phân biệt "cụm nên tách nhiều box riêng" với "cụm nên gộp `ignore_region reason=crowd_or_group`" — chi tiết đề xuất ở `submission/20_guideline_patch.md`.
