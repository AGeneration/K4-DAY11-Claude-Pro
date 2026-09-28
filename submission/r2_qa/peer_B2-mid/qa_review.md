# QA review · Duy review Tùng · B2-mid

Nguồn: [nhánh Tùng tại commit c86eea2](https://github.com/AGeneration/K4-DAY11-Claude-Pro/tree/c86eea2158ffe6b32fc9d394d254de125b1f2b9a).
R1 không đổi giữa `c86eea2` và HEAD `0bf94b0` của Tùng.

- Người review: Vũ Minh Duy, có trợ lý hỗ trợ soát ảnh và XML. Người được review: Hoàng Công Tùng. Vòng QA theo
  `team.json`: duy → tung.
- R1: **24F8-C550**, SHA256 `24f8c5502fa27f3285abfc93b6d53a787de5097e8ddbbdcd4dad43a650621354`. Bản gốc giữ tại
  [source_tung/annotations.xml](source_tung/annotations.xml), gồm 17 box và 14 polygon trên 3 ảnh 060000/086220/102750.
  Overlay: [qa_overlay.html](qa_overlay.html), tạo bằng `lab11.py qa --slice B2-mid --code 24F8-C550`.
- Đã soát ảnh gốc, nhãn R1 và rules v1.0.0 **trước** khi đọc bản rework. Không mở reference, model, compare hay findings
  của Tùng để lấy đáp án QA. Phần đối chiếu rework được ghi riêng ở cuối.
- L1…Ln là thứ tự box cao ≥ 40 px trong từng frame của R1, đúng cách đánh số trong overlay. Các dòng `r2_qa,B2-mid`
  trong [findings.csv](../../findings.csv) có `cell=L_only` và để trống `why`.

## Nhận xét trên bản R1

1. **QA-TUNG-01 · 060000, L2, R05, P2:** ThreeWheeler ở mép phải (987;856;1079;1109) có nửa trái bị đầu xe L1 che,
   nhưng `occluded=false`. Giá trị `truncated=true` đúng vì xe bị biên khung cắt. Đề nghị đặt `occluded=true`.
   Bằng chứng: [tung-060000.png](screenshots/tung-060000.png).
2. **QA-TUNG-02 · 060000, polygon `crowd_or_group` bên trái (x≈11–84, y≈868–979), R06/R01, P1, chờ phân xử:** trong
   polygon có khoảng 3 người đi bộ. Người mặc hồng ngoài cùng bên trái thấy rõ từ đầu tới chân và cao khoảng 100 px,
   vượt ngưỡng H=40. Theo R06, `crowd_or_group` chỉ dùng khi không tách được từng vật. Đề nghị tách được người nào thì
   box người đó. Bằng chứng: [tung-060000.png](screenshots/tung-060000.png).
3. **QA-TUNG-03 · 060000, L1, R02, P2:** đáy box ở y=1377 cắt khoảng 20 px bánh trước, trong khi bánh chạm đất ở
   y≈1398. Mép trái (x=375) và mép trên (y=680) lại hơi rộng so với thân xe. Đề nghị bám sát phần nhìn thấy.
   Bằng chứng: [tung-060000.png](screenshots/tung-060000.png).
4. **QA-TUNG-04 · 086220, sau L4/L5, R01, P1:** có hai phương tiện bị che một phần nhưng chưa có box: xe màu trắng
   (≈325–375; 963–1005) sau L5 và ô tô màu bạc (≈393–440; 975–1020) sau L4. Chiều cao nhìn thấy khoảng 42–47 px,
   sát ngưỡng. Đề nghị Tùng đo lại trên CVAT rồi box nếu ≥ 40 px.
   Bằng chứng: [tung-086220-L4L5-zoom.png](screenshots/tung-086220-L4L5-zoom.png).
5. **QA-TUNG-05 · 086220, trong box L1 (≈960–1075; 1120–1290), R03, P2, chờ phân xử:** góc dưới phải có đèn pha tròn
   và phuộc trước của một xe hai bánh đứng cạnh ThreeWheeler L1, bị L1 che phần lớn. Chưa chắc đây là xe riêng hay chi
   tiết của L1, nên đề nghị Tùng soi lại trên CVAT.
   Bằng chứng: [tung-086220-L1-right-zoom.png](screenshots/tung-086220-L1-right-zoom.png).
6. **QA-TUNG-06 · 102750, L5, R04, P1, chờ phân xử:** L5 `Truck` (0;845;88;962) có khoang kín mui cong, nhìn thấy
   người ngồi bên trong và không thấy thùng hàng. Dáng này giống xe chở khách (tempo/ThreeWheeler) hơn là xe tải.
   Đề nghị Tùng chỉ ra thùng hàng hoặc đổi class.
   Bằng chứng: [tung-102750-left-zoom.png](screenshots/tung-102750-left-zoom.png).
7. **QA-TUNG-07 · 102750, giữa L3 và L4 (≈175–212; 891–938), R01, P1:** có một ThreeWheeler mui vàng kem bị L4 che
   một phần, cao khoảng 45 px, nhưng chưa có box. Bằng chứng:
   [tung-102750-left-zoom.png](screenshots/tung-102750-left-zoom.png).

## Những điểm giữ với căn cứ ảnh

- Cả 3 ảnh đều có polygon `ego_body` bao đúng tay/chân người lái xe ego ở góc trái dưới (R07). Hai polygon
  `lens_border` import sẵn vẫn giữ nguyên (R08).
- 060000: L6 Bike (người lái + xe máy) là một box duy nhất, đúng R03. L3 và L5 là ThreeWheeler, đúng dáng.
- 086220: L2 Bike đúng R03. L6 Bike sau L1 có `occluded=true`, đúng R05. Polygon `unreadable` nhỏ (264–281) chỉ bao
  một vật mờ.
- 102750: L1 Truck có thùng chở hàng và bị biên phải cắt nên `truncated=true`, đúng. L2, L3, L4 là ThreeWheeler.
  Hai polygon `unreadable` bao hai xe ở xa, bị ngược sáng.

Những ghi nhận này không có nghĩa là mọi đỉnh polygon hay mọi vật nhỏ dưới 40 px đã được duyệt.

## Đối chiếu bổ sung với rework mới nhất

Rework **CF64-2680**, SHA256 `cf642680db772af685f943306b1fe4a299b5c2f6c4b6e2bd33c7be121d90432a`, commit `0bf94b0`.
Bản gốc giữ tại [source_tung/annotations-v2.xml](source_tung/annotations-v2.xml). Phần này không thay thế các nhận xét
trên R1 và không mở reference hay model.

- QA-TUNG-01: L2 vẫn `occluded=false`, **chưa xử lý**.
- QA-TUNG-02: **đã xử lý**. Polygon crowd bên trái được thay bằng 3 Pedestrian (8;877;46;957), (38;865;64;979),
  (61;874;76;952).
- QA-TUNG-03: hình học L1 giữ nguyên, **chưa xử lý** (P2).
- QA-TUNG-04, 05: không có box mới ở các vị trí này, **chưa xử lý**.
- QA-TUNG-06: L5 vẫn là `Truck`, **chưa xử lý**. Bản rework còn đổi L3 từ ThreeWheeler (114;892;169;949) thành
  `Truck` (88;892;169;949). Nhìn ảnh gốc, tôi thấy L3 có mui cong giống xe ba bánh. Đây là ca D04 của Tùng, và tôi đề
  nghị Tùng dẫn thêm bằng chứng về thùng hàng.
- QA-TUNG-07: chưa có box ở ≈175–212, **chưa xử lý**.
- **Mới phát sinh trong rework, R09:** hai box nằm gần như trọn trong polygon ignore: Pedestrian (187;870;202;912)
  nằm trong `crowd_or_group` (163–214; 868–915) ở 060000, và Truck (333;903;366;953) nằm trong `unreadable`
  (332–370; 915–954) ở 102750. Đề nghị giữ box và bỏ polygon, hoặc ngược lại.

Các đề nghị trên đã ghi trong hồ sơ này và giao cho Tùng. Tôi không sửa nhãn hay file bài làm nào của Tùng; trên nhánh
Tùng chỉ cập nhật `TEAMMATES.md` để ghi nhận QA đã giao. Đây là
QA có trợ lý hỗ trợ, không mạo nhận Tùng hay Coach đã đồng ý với các ca còn mở.
