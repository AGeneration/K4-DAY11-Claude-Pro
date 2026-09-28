# Sensor context

- **Rig:** Ảnh cho thấy camera fisheye hướng về phía trước trên một phương tiện đang đi trên đường. Không có tài liệu đủ để xác định chính xác vị trí gắn camera hoặc thông số hiệu chuẩn.
- **`ego_body`:** Ở phía dưới bên trái một số frame có thể thấy một phần xe gắn camera, như tay lái và phần thân xe. Chỉ khoanh vùng các bộ phận này khi chúng thực sự xuất hiện trong từng ảnh.
- **Vòng kính:** Vùng ảnh fisheye nằm gần giữa khung, chiếm gần hết chiều ngang và khoảng 80% chiều cao. Vành đen của ống kính hiện rõ ở phía trên, phía dưới và sát hai bên.
- **Annotation space:** Gán nhãn trên ảnh raw fisheye 1080 × 1920 của repo; box bám phần nhìn thấy theo R02, ngưỡng chiều cao H=40 theo R01. Không chuyển tọa độ sang ảnh undistort hay BEV.
- **Giới hạn dữ liệu:** ADASIND trong bài chỉ có một camera. Không có chuỗi đồng bộ front/rear/left/right, calibration đủ để ghép BEV, độ sâu hay ground truth khoảng cách. Zone center/mid/edge là vị trí bán kính trên ảnh, không chỉ khoảng cách vật tới xe.
- **Hai nguồn khác:** Task parking dùng ảnh camera thường; polygon free_space chỉ mô tả phần mặt đường trống nhìn thấy. Kế hoạch 200/50.000 frame cho bốn camera là đề xuất trên tình huống giả lập, không phải thống kê thu được từ slice B2-dense.
- **Phạm vi hiện tại:** Nguyên export job30 gồm 062370, 069450, 117120; cả ba là raw fisheye 1080×1920. Đã bỏ giảm frame3, giữ giảm stretch/k12 vì export không có polygon đối chứng.
- **Nguồn và hỗ trợ:** export_provenance.json lưu hash ZIP/XML; XML r1 không bị chỉnh sửa khi nhận. Review/phân tích được trợ lý hỗ trợ; không mạo nhận là review của Duy. Bản hai ảnh job29 trước đây đã được thay thế và chỉ giữ trong lịch sử local.
