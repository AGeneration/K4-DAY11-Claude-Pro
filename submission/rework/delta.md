# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 9 | 12 | 4 | 1 | 3 | 2 |
| mid | 4 | 5 | 1 | 0 | 1 | 0 |
| edge | 2 | 2 | 0 | 0 | 0 | 0 |

## Findings action=rework
- adasind_019560.jpg L7 SPURIOUS: không áp dụng
- adasind_019560.jpg ego_body IGNORE_SCOPE: không áp dụng
- adasind_062370.jpg L4 WRONG_CLASS: đã sửa
- adasind_069450.jpg XML_box6_H24.46 STRUCTURE: không áp dụng
- adasind_069450.jpg XML_box6_H24.46 STRUCTURE: không áp dụng
- adasind_117120.jpg XML_box2_box3_box6 STRUCTURE: không áp dụng
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

## Giải thích job30

R1 E4B2-125A là nguyên export CVAT job30, đủ ba ảnh. Rework 00BC-F291 là đề xuất sửa tại máy; provenance.json ghi rõ chưa xác minh import/re-export CVAT. Lock chứng minh bytes, không chứng minh đã thao tác trên CVAT.

Matched 15→19, missing 5→1, spurious 4→2: sửa class van, siết Bike, thêm Truck bị che ở 062370; sửa Car vẽ thiếu ở 117120. Bỏ ba box thật dưới H=40 không làm đổi metric vì matcher đã lọc chúng. Giữ Bus/ThreeWheeler 117120 chờ QA; không sửa reference R7 nghi trùng.

Các mã XML_box... không được hàm rework ánh xạ thành L/R in-scope, nên báo “không áp dụng”; đã kiểm trực tiếp XML sửa. C0 không thuộc B2 và chưa được sửa trong bản rework này. Bảng số không chỉnh tay.
