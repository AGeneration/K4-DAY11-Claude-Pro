# Bản rework B2-dense để import CVAT

File đã chuẩn bị: **B2-dense-rework-import.zip**. ZIP có đúng một file `annotations.xml`, nguyên bytes của `annotations-v2.xml` đã khóa **00BC-F291**. Không chứa ảnh/cache. Có thể dùng XML trực tiếp theo hướng dẫn repo.

## Những thay đổi đã thực hiện

- 062370: đổi van Truck thành Car theo R04; siết box Bike về (487;783;531;859); thêm Truck bị che tại (316;740;418;818).
- 069450: bỏ Car nhỏ có chiều cao 24.46 px, dưới ngưỡng R01.
- 117120: sửa Car vẽ thiếu thành (348;918;396;961); bỏ hai Car nhỏ dưới 40 px. Giữ Bus và ThreeWheeler còn tranh luận để QA phân xử.

R1 gốc E4B2-125A được giữ nguyên để đối chứng. Delta: matched 15→19, missing 5→1, spurious 4→2. Không thêm box reference nghi trùng để làm đẹp số.

## Thao tác còn lại trên CVAT

1. Mở đúng task B2-dense có ba ảnh 062370, 069450, 117120. Lưu bản export hiện tại trước khi import ghi đè nhãn.
2. Tại trang task, Actions → Upload annotations → CVAT 1.1; chọn `annotations-v2.xml` (hoặc ZIP nếu giao diện nhận ZIP).
3. Mở job kiểm ba frame, đặc biệt các thay đổi kể trên, rồi Ctrl+S. Export job dataset → CVAT for images 1.1, tắt Save images, tải ZIP mới.
4. Dùng ZIP mới để relock sau khi ghi lý do trong decision log; chạy lại `rework`, `triage`, `check` và cập nhật mã/hash/provenance nếu thay đổi. Không sửa trực tiếp XML đã khóa.

```powershell
py -3.11 lab11.py lock rework "DUONG_DAN_ZIP_CVAT_MOI" --relock
py -3.11 lab11.py rework
py -3.11 lab11.py triage
py -3.11 lab11.py check
```

ZIP này được đóng gói tại máy từ bản sửa có trợ lý hỗ trợ; chưa có vòng Save/export CVAT được xác minh. `package_audit.json` kiểm hash, tên ảnh, số hình và ZIP/XML khớp bytes; không tự chứng minh chất lượng hoặc thao tác CVAT. `rework_overlay.html` giúp xem nhãn sửa khi mở trong repo có assets/images; chỉ số L thuộc bản rework, không thay mã trong findings R1.
