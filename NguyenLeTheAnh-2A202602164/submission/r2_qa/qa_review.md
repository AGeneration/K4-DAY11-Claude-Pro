# QA review · Anh review Duy · B4-center

Nguồn: [nhánh Duy tại commit 79fdaac](https://github.com/AGeneration/K4-DAY11-Claude-Pro/tree/79fdaacdf8a056a2c1858fd67ab57a6b20150514). Đây là commit mới lấy theo thông báo của người học. R1 không thay đổi so với 82371069; rework đã cập nhật.

- Người thực hiện hồ sơ: Nguyễn Lê Thế Anh, có trợ lý hỗ trợ soát ảnh và XML; người được review: Vũ Minh Duy. Không ghi Duy là người review bài Anh.
- R1: **34BC-63D5**, SHA256 `34bc63d57a96f592abe7c1091da7c700bdd63c7f56317727ad46796d863f768b`; nguyên bản giữ tại [source_duy/annotations.xml](source_duy/annotations.xml), 29 box và 12 polygon, đủ 270517/271039/295948.
- Đã soát ảnh gốc, nhãn R1 và rules v1.0.0 trước khi đọc rework. Không mở reference, model, compare hoặc findings của Duy để lấy đáp án QA. Sau đó mới đối chiếu XML rework ở mục riêng bên dưới.
- L1…Ln là mã box trong overlay **R1**, không dùng số thứ tự rework thay thế. Các dòng r2_qa có cell=L_only và why trống. Ghi chú tự review B2-dense trước đây nằm trong previous_self_review.md/previous_self_findings.json, không còn tính là peer QA.

## Nhận xét trên bản R1

1. **QA-DUY-01 — 270517, L3/group 2, R05, P2:** xe máy mép phải bị cắt tại biên x=1080. Box ghi truncated=true đúng với ảnh, nhưng polygon Bike cùng group ghi false. Đề nghị đồng bộ polygon; không cần thêm Pedestrian. Bằng chứng: [ảnh 270517](../screenshots/duy-270517.png) và XML group 2.
2. **QA-DUY-02 — 271039, L1, R05, P2:** ThreeWheeler phía sau người đi bộ bị che. Attribute occluded=true phù hợp ảnh, nhưng trường XML chuẩn occluded=0. Đây là bất nhất biểu diễn cần xác minh khi import/export, không phải kết luận thuộc tính tùy chỉnh sai. Parser lab đọc attribute nên số đo hiện tại không thể chứng minh công cụ khác hiểu đúng. Bằng chứng: [ảnh 271039](../screenshots/duy-271039.png), box (263;824;326;908).
3. **QA-DUY-03 — 271039, L12+L13, R02, P1 chờ phân xử:** hai người chồng nhau cạnh xe máy; box nhỏ nằm trong box lớn. Yêu cầu chỉ rõ đầu/thân/chân nhìn thấy của từng người, kiểm lại cạnh box; không xóa nhãn chỉ do overlap. Bằng chứng: cùng ảnh 271039, L12=(392;818;438;936), L13=(393;823;418;904).
4. **QA-DUY-04 — 295948, L4, R03, P1 chờ phân xử:** Bike đang ôm người sát camera nhưng phần xe/chân có che và blur. Cần xác nhận người đang ngồi trên xe hay dắt xe trước quyết định một Bike hay Pedestrian+Bike. Không suy class chỉ từ tư thế một phần. Bằng chứng: [ảnh 295948](../screenshots/duy-295948.png), L4=(574;606;1080;1716).

## Những điểm giữ với căn cứ ảnh

270517: giữ ThreeWheeler lớn, không box riêng người ngồi bên trong (R03/R04); giữ Bike sát biên với truncated=true. 271039: không thấy ego_body nên giữ không thêm polygon ego (R07); hai lens_border vẫn có. 295948: xe nhỏ ở (460;890;655;1062) có thùng hàng, giữ Truck theo R04; ego_body được vẽ ở góc trái dưới. Các nhận xét này không tương đương phê duyệt mọi đỉnh polygon hoặc mọi đối tượng nhỏ trong ảnh.

## Đối chiếu bổ sung với rework mới nhất

Rework **FA15-D3EC**, SHA256 `fa15d3ec04e86ec04651ba580dc5d3887dd16d204f332abda5cfd2511c26a1f9`, nguyên bản tại source_duy/annotations-v2.xml. Không thay thế bản R1 đã review và không mở reference/model.

- QA-DUY-01: box số 5 tại 270517 vẫn truncated=true, polygon group 2 vẫn false; chưa khép được nhận xét.
- QA-DUY-02: box số 5 tại 271039 vẫn có hai trường occluded khác nhau; cần kiểm serialization trên CVAT và công cụ tiêu thụ.
- QA-DUY-03: hình học giữ nguyên, nay là box số 9 và 10 tại 271039; vẫn cần xác nhận từng người.
- QA-DUY-04: 295948 đổi Bike lớn thành Pedestrian số 1 (574;606;1080;1726.5), thêm Bike số 3 (639.21;1415.05;1012.76;1581.40). Ghi nhận đã thay đổi, nhưng ảnh vùng xe bị che/blur nên chưa đủ căn cứ tự phê duyệt việc tách; đề nghị Duy chỉ rõ phần xe và trạng thái dắt/ngồi.

Các đề nghị đã ghi trong hồ sơ, chưa gửi bình luận hoặc thông báo cho Duy. Không sửa hay push vào nhánh Duy. Đây là QA có trợ lý hỗ trợ, không mạo nhận Duy/Coach đã xác nhận các ca còn mở.
