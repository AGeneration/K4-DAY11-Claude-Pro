# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): hai vạch chéo ở hàng ô giữa ảnh — vạch thứ nhất từ khoảng
  (176, 524) xuống (247, 564), vạch thứ hai từ khoảng (280, 520) xuống (421, 554). Mỗi vạch là một đoạn sơn ngăn hai
  ô cạnh nhau; polyline bắt đầu nơi vạch tách khỏi vạch ngang đầu ô và dừng tại đầu mút sơn nhìn thấy, không kéo dài
  qua phần nhựa đường trống.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: vạch ngang dài ở y ≈ 520–535 chạy liên tục gần hết bề ngang ảnh.
  Nó là đường đầu ô/biên hàng dùng chung cho cả dãy, không tách riêng một ô nên không gán `parking_line`. Các vạch ở
  tiền cảnh (đáy ảnh, ví dụ đoạn từ (402, 652) tới (525, 720)) cũng không vẽ trong bài này vì chúng bị khung ảnh cắt,
  không thấy vạch đầu ô tương ứng để chắc chúng chia ô nào.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: polygon phủ lối xe chạy trống giữa hàng ô giữa ảnh và
  hàng ô tiền cảnh, cạnh trên dừng ngay dưới đầu mút các vạch chia ô (từ y ≈ 581 ở mép trái lên y ≈ 521 ở mép phải, nơi
  dãy ô kết thúc), cạnh dưới là đường thẳng từ (0, 680) tới (956, 589), dừng trước đầu các vạch tiền cảnh; hai bên
  dừng ở mép khung ảnh. Không có xe hay vật che trong vùng này; xe đỏ ở xa
  (≈ 205, 467) nằm ngoài polygon.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): các vạch mờ ở xa gần xe đỏ (y < 505) quá nhỏ và bị
  chói, không phân biệt được vạch chia ô với vạch lối đi nên không vẽ. Ranh giới trái/phải của `free_space` bị khung
  ảnh cắt — lối xe chạy thực tế còn tiếp tục ngoài khung, polygon chỉ mô tả phần nhìn thấy.
