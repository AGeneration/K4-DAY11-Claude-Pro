# QA review · B2-dense · job30, đủ ba ảnh

Mã khóa: E4B2-125A. SHA256: e4b2125afb4550b6a2b0cc5c7f993756e14d34770cfef5bcba75200d6d04ef7e.
Nguồn: nguyên annotations.xml của ZIP job30, không lọc/đổi frame hoặc chỉnh nhãn trước khóa.

Lượt review này có trợ lý hỗ trợ. Hai ảnh đầu đã được review mù trong lượt job29 trước reveal; hình học/class của chúng không đổi trong job30. Đã xem reference/model hai ảnh đó ở lượt trước, nên không tuyên bố lượt cập nhật này hoàn toàn mù. 117120 được đọc từ ảnh và nhãn job30 trước khi đọc các ca reference/model của frame này. Không có file review của Duy và không mạo nhận người soát độc lập đã phê duyệt.

| frame | object_ref | rule_id | nhận xét trước chẩn đoán mới |
|---|---|---|---|
| adasind_062370.jpg | L4 | R04 | Van có khoang hành khách đang mang Truck; đề nghị Car. Nhận xét kế thừa lượt review mù trên cùng hình học/class. |
| adasind_069450.jpg | XML_box6_H24.46 | R01 | Box Car thứ 6 trong XML cao 24.46 px <40; đề nghị loại khỏi phạm vi. Không có mã L trong overlay in-scope. |
| adasind_117120.jpg | XML_box2_box3_box6 | R01/R02 | Các box Car thứ 2, 3, 6 trong XML cao lần lượt 37.43, 21.15, 32.77 px. Soát phần vật nhìn thấy trước khi quyết định bỏ hay sửa box vẽ thiếu; không đồng nhất chiều cao box sai với chiều cao vật. |
| adasind_062370.jpg | job_metadata | R02 | Export dạng job không có tên task; parser lấy tên label Bus. Cần xác minh tên raw_fisheye trên CVAT, chưa kết luận task đặt sai tên. |

Ảnh bằng chứng: ../screenshots/03-b2-van.png, ../screenshots/04-b2-scope.png, ../screenshots/07-job30-frame3.png. why của r2_qa giữ trống; phản hồi sau chẩn đoán nằm trong findings r3_diag và phần đọc kết quả.
