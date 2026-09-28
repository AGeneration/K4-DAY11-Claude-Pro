# Sensor context

- Rig: quan sát trên frame `adasind_019560.jpg` (1080 × 1920, ảnh dọc): camera fisheye nhìn về phía trước theo
  chiều đi của xe, đặt khá thấp và gần làn đường. Bóng đổ trên mặt đường ở đáy ảnh có dáng người đội mũ bảo hiểm trên
  xe hai bánh, nên có vẻ camera gắn trên xe máy/xe hai bánh chứ không phải ô tô — đây là suy luận từ ảnh, ADASIND
  không kèm tài liệu rig nên chưa xác nhận được vị trí gắn và độ cao.
- `ego_body` nhìn thấy ở đâu trong frame: một phần thân xe tối màu ở mép trái, khoảng x 0–140, y 1070–1560 (có thể
  là tay lái/gương/ốp đầu xe). Bóng của người lái trên mặt đường ở đáy ảnh **không** phải `ego_body` vì nó là bóng
  trên đường, không phải thân xe. Ở một số frame khác (ví dụ `adasind_006840.jpg`, `adasind_271039.jpg`) không thấy
  thân xe, nên vị trí này không cố định cho mọi frame.
- Vòng kính (lens circle) nằm ở vị trí nào trong ảnh, chiếm khoảng bao nhiêu phần khung hình: vòng tròn gần như tâm
  ảnh, từ khoảng y 115 tới y 1700, bề ngang chạm/bị cắt ở hai mép trái phải (≈ 1080 px). Vùng hợp lệ chiếm khoảng
  70–75% diện tích khung; phần đen ngoài vòng (đầu ảnh, đáy ảnh và bốn góc) là `lens_border`. Méo rõ nhất ở rìa vòng:
  cột điện và mép mái hiên bị uốn cong khi gần viền.
