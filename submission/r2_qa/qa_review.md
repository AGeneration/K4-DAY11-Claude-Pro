# QA review · B2-dense

Mã khóa: E4B2-125A

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_062370.jpg | L4 | R04 | Box gán `Truck`, hình dạng trên ảnh giống xe van/minivan chở khách đỗ trước cửa hàng. R04 quy định van chở người → `Car`. Đề nghị kiểm tra lại đây là van chở người hay xe tải chở hàng. |
| adasind_069450.jpg | L6 | R01 | Box `Car` cao ~24px, dưới ngưỡng H=40px. R01: vật thấp hơn H không bắt buộc có box. Đề nghị xác nhận có cần giữ box này không. |
| adasind_117120.jpg | L3 | R01 | Box `Car` cao ~21px, dưới ngưỡng H=40px, cùng lý do R01 như trên. |
| adasind_117120.jpg | L6 | R01 | Box `Car` cao ~33px, dưới ngưỡng H=40px, cùng lý do R01 như trên. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
