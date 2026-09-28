# Quan sát vạch ô đỗ

- Export có đúng ảnh `parking-lot-core.jpg` 960 × 720, ba polyline `parking_line` và một polygon `free_space`.
- Ba vạch chia ô đã chọn nằm ở nửa trái ảnh: vạch gần dọc từ (47.56;571.93) đến (59.76;521.23); vạch chéo từ (248.53;563.86) đến (176.83;524.26); vạch chéo kế bên từ (420.63;554.13) đến (278.51;517.90). Chúng phân chia các ô cạnh nhau; đường vẽ dừng ở phần sơn nhìn thấy, không nối thành đường xuyên vùng không có vạch.
- Em không vẽ mép dải đường sáng nằm ngang ở phía xa gần hàng cây, vì đó không phải ranh giới rõ ràng của một ô đỗ riêng.
- Polygon `free_space` bao phần lối xe chạy trống ở phía trước các vạch chia ô. Em dừng vùng này trước các ô đỗ ở tiền cảnh, không phủ lên xe hoặc vật cản.
- Ca chưa chắc cần hỏi người soát: Không có.
- Bằng chứng đối chiếu XML với ảnh gốc: [ảnh chụp overlay parking](../screenshots/01-parking.png). Đây là ảnh chụp trang overlay local, không phải giao diện CVAT.
- Giới hạn: `free_space` mô tả mặt đường trống nhìn thấy tại thời điểm chụp; không suy ra độ sâu, độ bám, khoảng sáng gầm hay khả năng xe tự hành đi an toàn.
