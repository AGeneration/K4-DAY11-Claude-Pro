# Tự soát

- adasind_069450.jpg L6: chiều cao < H (xem lại phạm vi)
- adasind_117120.jpg L2: chiều cao < H (xem lại phạm vi)
- adasind_117120.jpg L3: chiều cao < H (xem lại phạm vi)
- adasind_117120.jpg L6: chiều cao < H (xem lại phạm vi)
- Tên task thiếu raw_fisheye

## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ
- [x] lens_border và ego_body
- [x] Class sáu nhãn
- [x] Rider và Bike
- [x] Geometry trên ảnh fisheye gốc
- [x] truncated và occluded
- [x] Vật thiếu hoặc box trùng
- [x] ignore_region có reason
- [x] Tên task raw_fisheye và export CVAT 1.1

## Ghi nhận job30

Đã soát đủ ba ảnh gốc và XML job30. [x] là đã kiểm và ghi kết quả; không có nghĩa mọi nhãn đã đúng. R1 E4B2-125A giữ nguyên bytes export làm đối chứng. Những lỗi dưới đây được giữ ở baseline và xử lý/đề xuất ở rework riêng.

1. H=40: 069450 XML6 cao 24.46 px; 117120 XML2/3/6 cao 37.43/21.15/32.77 px. XML2 vẽ thiếu phần trên của Car nên sửa biên theo ảnh; hai box nhỏ còn lại ngoài phạm vi thì bỏ.
2. Lens/ego: cả ba ảnh có hai lens_border và một ego_body; thân xe ở phía trái dưới thấy được. Đã đối chiếu silhouette; không dùng bóng đổ làm thân xe.
3. Class: 062370 van L4 đang là Truck, đề nghị Car theo R04. Bus ở 117120 có vật thật nhưng chi tiết nhỏ và nguồn khác class: giữ lại chờ phân xử.
4. Rider: Bike của người học ôm người+xe; không thêm Pedestrian theo output model khi đó là rider. C0 rider là ca riêng, không lẫn với B2.
5. Geometry: bám raw fisheye 1080×1920; 062370 Bike L3 rộng quá và 117120 Car XML2 bị ngắn trên. Soát xe bị che theo phần thấy, không tưởng tượng phần khuất.
6. Truncated/occluded: Bike sát x=1080 trong 062370 có truncated=true; Truck bổ sung bị rider che nên occluded=true. Không suy thuộc tính từ zone.
7. Thiếu/trùng: đề xuất thêm Truck thật bị che, không thêm box trùng để khớp R7. Reference/model chỉ dùng sau phần review ảnh; lịch sử review không được mô tả thành một lượt blind mới hoàn toàn.
8. Ignore: chín polygon có reason hợp lệ; selfqc không báo box nằm chủ yếu trong ignore. Không đánh đồng pixel blur với tự động phải ignore toàn bộ đối tượng.
9. Định dạng: CVAT XML 1.1, không có track; đủ ba tên ảnh đúng. Metadata dạng job thiếu tên task nên cảnh báo raw_fisheye chưa tự xác minh được; cần kiểm tên trên CVAT, không kết luận task tên Bus từ tên label đầu tiên.

K12: ZIP job30 không có bốn polygon/group_id đối chứng; giữ giảm stretch/k12 đã ghi, **không giảm frame3**. Không đưa polygon trợ lý tạo ở bản cũ vào nhãn người học.
Bằng chứng: screenshots/03-b2-van.png, 04-b2-scope.png, 07-job30-frame3.png và 00_setup/export_provenance.json. Review do trợ lý hỗ trợ; chưa có chứng nhận QA độc lập.
