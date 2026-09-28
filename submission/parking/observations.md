# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Cả hai nằm ở khu vực giữa-trái bãi đỗ, khoảng giữa
  chiều dọc ảnh (ảnh gốc 960x720). Vạch 1 ngắn, ở x≈176–246, y≈521–562. Vạch 2 dài hơn, nằm ngay bên phải
  vạch 1, x≈281–419, y≈518–552. Cả hai là đoạn sơn trắng chéo, phân chia ranh giới giữa các ô đỗ liền kề,
  nhìn rõ, không bị che.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Vạch trắng ở sát mép dưới-trái khung hình không được vẽ
  vì bị khung ảnh cắt ngang, chỉ thấy một đoạn ngắn, không đủ căn cứ xác nhận đây là ranh giới trọn vẹn của
  một ô đỗ hay chỉ là phần dư của vạch khác.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Vẽ lại sau khi nhận ra hiểu sai ban đầu — `free_space`
  là **lối xe chạy** trong bãi, không phải mọi khoảng mặt đường trống. Polygon hiện là một dải ngang chạy hết
  chiều rộng ảnh, nằm ở khoảng giữa ảnh theo chiều dọc (y≈521–678/720), tương ứng với lối đi giữa hai hàng ô
  đỗ; không chạm tới hàng rào phía xa, không đè lên xe/vật cản. Không có phần nào bị che khuất trong vùng đã
  khoanh.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): Không có — sau khi sửa lại theo đúng nghĩa
  “lối xe chạy”, vùng khoanh không còn giao với vật thể/khu vực mơ hồ nào ở bản vẽ trước.
