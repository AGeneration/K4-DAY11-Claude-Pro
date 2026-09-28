# Nguồn ảnh bằng chứng

PNG là screenshot Chrome headless của overlay local từ XML/ảnh gốc, không phải giao diện CVAT và không chứng minh thao tác Save/export.

- 01: parking XML đã có và ảnh core.
- 02: C0 đã khóa, rider L1/L2/L7/L8.
- 03/04: box trong hai ảnh đầu; geometry/class không đổi giữa job29 và job30.
- 05: reference R5/R7 nghi trùng và Truck R8 bị che, sau reveal.
- 06: model đóng băng, chỉ số M sau lọc H≥40 như báo cáo.
- 07: nguyên nhãn job30 trên ảnh đúng 117120; chỉ số XML toàn bộ box, khác chỉ số L sau lọc H.

Nguồn đầy đủ có trong assets và submission; mọi crop/zoom chỉ để đọc bằng chứng, không thay tọa độ nhãn. Các trang HTML tạm và profile trình duyệt không thuộc bài nộp.

Ảnh duy-270517.png, duy-271039.png, duy-295948.png: ảnh gốc và overlay R1 Duy 34BC-63D5, lấy tại commit 79fdaac; chụp bằng Chrome cục bộ, không phải CVAT và không có reference/model. Số L thuộc R1; rework đổi thứ tự nên dùng mapping trong qa_review.md.
