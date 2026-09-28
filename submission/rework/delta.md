# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 9 | 12 | 4 | 1 | 3 | 2 |
| mid | 4 | 5 | 1 | 0 | 1 | 0 |
| edge | 2 | 2 | 0 | 0 | 0 | 0 |

## Findings action=rework
- adasind_019560.jpg L7 SPURIOUS: không áp dụng
- adasind_019560.jpg ego_body IGNORE_SCOPE: không áp dụng
- adasind_069450.jpg XML_box6_H24.46 STRUCTURE: không áp dụng
- adasind_117120.jpg XML_box2_box3_box6 STRUCTURE: không áp dụng
- adasind_062370.jpg L3+R9 BOX_GEOMETRY: đã sửa
- adasind_062370.jpg L4+R4 WRONG_CLASS: đã sửa
- adasind_062370.jpg R8 MISSING: đã sửa
- adasind_117120.jpg R3 MISSING: đã sửa
- adasind_062370.jpg L3 SPURIOUS: đã sửa
- adasind_062370.jpg L4 SPURIOUS: đã sửa
- adasind_062370.jpg R4+M6 MISSING: đã sửa
- adasind_062370.jpg R8 MISSING: đã sửa
- adasind_062370.jpg R9+M7 MISSING: đã sửa
- adasind_117120.jpg R3+M5 MISSING: đã sửa
- adasind_069450.jpg XML_box6_H24.46 STRUCTURE: không áp dụng
- adasind_117120.jpg XML_box2_box3_box6 STRUCTURE: không áp dụng
- adasind_270517.jpg L3 ATTRIBUTE: không áp dụng

## Giải thích bản export CVAT cuối

R1 E4B2-125A giữ nguyên. Rework **823C-842B** là XML lấy nguyên bytes từ B2-dense-rework-cvat-export.zip do CVAT xuất sau import vào job30/task47. Mã 00BC-F291 là bản local trước vòng CVAT, được giữ trong lịch sử lock. cvat_roundtrip.json ghi tác vụ import/export đều finished; so sánh toàn bộ nhãn xác nhận không mất/đổi hình, class, thuộc tính hoặc group.

Matched 15→19, missing 5→1, spurious 4→2. Đã sửa van, Bike và Truck bị thiếu ở 062370; Car vẽ thiếu ở 117120; bỏ ba box dưới H40. Giữ các ca reference nghi trùng và Bus/ThreeWheeler còn cần QA. Không sửa số bằng tay hoặc ép nhãn theo reference.

Các mã XML_box... không được hàm rework ánh xạ thành L/R nên có dòng không áp dụng; đã kiểm trực tiếp nhãn sau export. C0 và QA B4-center của Duy không thuộc bản sửa B2-dense này. Việc hoàn thành vòng CVAT không đồng nghĩa các escalation đã được người nhận phê duyệt.
