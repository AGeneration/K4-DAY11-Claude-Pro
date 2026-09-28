# QA review · B4-center

Mã khóa: 34BC-63D5

**Hình thức:** cold review chính bản khoá của mình (`exports/r1-final.zip`, mã khớp `34BC-63D5`). Nhóm 3 người (anh, duy, tung) nhưng không nhận được export đã khoá của người kế bên trong thời gian chờ, nên theo `docs/03-roles-rotation-vi.md` chuyển sang cold review sau ≥5 phút kể từ lúc khoá. Chỉ dùng ảnh gốc, `qa_overlay.html` và `docs/02-rules-vi.md`; **chưa mở** teaching reference, model overlay hay worked HTML.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_295948.jpg | L4 | R03 | Bike [574,606,1080,1716]: người quấn khăn caro ngồi trên xe đạp sát bên phải camera, bị khung phải và vòng kính đáy cắt. Luật chỉ nói người lái + xe hai bánh = một Bike; nếu người này thực ra là người đạp của chính xe gắn camera (xích lô) thì R07 `ego_body` hoặc "người ngồi trong phương tiện" mới áp dụng. Ảnh tĩnh không cho thấy khung xe nối với camera. Cần người soát thứ hai xem frame lân cận. |
| adasind_271039.jpg | L14+L2 | R03 | Pedestrian L14 [432,814,465,892] (áo sọc trắng) đứng ngay sau xe máy đỗ L2 [422,868,454,949]; hông ngang tầm yên. Nếu đang ngồi trên yên thì R03 yêu cầu gộp thành một Bike. Ảnh không thấy rõ chân nên đang tách Pedestrian + Bike; ghi là chưa chắc. |
| adasind_270517.jpg | L8 | R01 | ThreeWheeler [117,765,149,807] cao 42 px — chỉ vượt H=40 hai pixel; hình mờ, class suy từ tỉ lệ cao/rộng (xe ba bánh nhìn từ sau). Một chênh 3 px ở mép trên/dưới sẽ đẩy vật ra ngoài phạm vi. |
| adasind_270517.jpg | x0-12,y757-885 | R01 | Dải tối sát mép trái khung (x=0–12, y≈757–885, cao ~128 px) không có box. Có thể là người đứng bị khung cắt (khi đó cần box `truncated`) hoặc cột/thân cây. Không đọc được class từ 12 px bề rộng; nêu để người soát quyết định có dùng `unreadable` hay không. |
| adasind_270517.jpg | L2 | R02 | ThreeWheeler [450,713,816,1005]: mép dưới đặt ở y=1005 nằm trong ô làm mờ riêng tư (y≈890–1020), tức là suy đoán chứ không phải phần nhìn thấy. Polygon K12 cùng group cũng được kéo xuống qua ô blur. Hình học đáy xe cần ghi rõ là ước lượng. |
| adasind_295948.jpg | L7 | R03 | Bike [0,894,138,1210] gộp xe đạp chở thùng "PDF" với người áo xanh ngọc. Cánh tay nối tới quai thùng đi ra từ mép trái khung, không chắc thuộc người áo xanh; nếu người áo xanh chỉ đứng sau xe đạp thì phải tách Pedestrian + Bike. |

Không thấy vi phạm R07 ở 271039 (không có `ego_body`), R08 (lens_border giữ bản import, bám vành kính) hay R09 (không box nào nằm ≥50% trong ignore).

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
