# Guideline patch

- **Rule mới đề xuất:** R12 — kiểm trường hợp reference trùng và giữ trạng thái chưa phân xử. Khi một box reference nằm trong box reference cùng class trên cùng vật, QA phải kiểm ảnh gốc, biên nhìn thấy, vùng blur và khả năng có hai vật thật. Không thêm box người học chỉ để xóa dòng MISSING. Ghi mã cả hai box, ảnh chụp, tọa độ và ticket; chỉ sửa reference sau lượt adjudication độc lập. Với rider bị blur che tư thế, giữ E5_unresolved và mô tả bằng chứng cần thêm.
- **Áp dụng cho:** Rectangle trong sáu class động của lab; đặc biệt ThreeWheeler bị blur và Bike/Pedestrian theo R03. Không mở rộng taxonomy sang vật tĩnh, không thay luật hình học R02 hoặc ngưỡng H=40.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R02/R03 quy định cách gán nhãn nhưng chưa chỉ rõ luồng phân xử khi chính reference có box lồng nhau hoặc blur che tư thế. Ở 062370, R7 nằm trong R5 trên cùng xe ba bánh; ở C0, L8/L2 liên quan người áo vàng có chân bị blur. Taxonomy cho phép E0/E5 nhưng cần thêm yêu cầu bằng chứng và người duyệt.
- **`rules_version` mới:** Đề xuất v1.0.0 → v1.1.0; mọi nhãn/findings hiện tại vẫn đánh giá theo v1.0.0.
- **Hiệu lực từ:** Vòng review kế tiếp sau khi Lab Coach/owner guideline duyệt. Đây là đề xuất chưa được phê duyệt, không áp dụng hồi tố để thay số của bài hiện tại.

Bằng chứng: [reference nghi trùng](screenshots/05-reference-duplicate.png), [C0 rider](screenshots/02-c0-rider.png). Giữ nguyên `docs/02-rules-vi.md` và teaching reference.
