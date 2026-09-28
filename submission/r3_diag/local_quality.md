# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `34bc63d57a96f592abe7c1091da7c700bdd63c7f56317727ad46796d863f768b`; slice `B4-center`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_270517.jpg, adasind_271039.jpg, adasind_295948.jpg. Frame thiếu trong export: không.
TP=18; FP=6; FN=2; số lần đối chiếu=25; mean IoU của TP=0.800.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.720 | 0.936 | 0.880 |
| precision | 0.750 | 0.733 | 0.500 |
| recall | 0.900 | 0.931 | 0.800 |
| jaccard | 0.692 | 0.677 | 0.500 |
| dice | 0.818 | 0.803 | 0.667 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 1 | 0 | 0.960 | 0.750 | 1.000 | 0.750 | 0.857 |
| Car | 4 | 0 | 1 | 0.960 | 1.000 | 0.800 | 0.800 | 0.889 |
| Pedestrian | 6 | 2 | 1 | 0.880 | 0.750 | 0.857 | 0.667 | 0.800 |
| ThreeWheeler | 4 | 2 | 0 | 0.920 | 0.667 | 1.000 | 0.667 | 0.800 |
| Truck | 1 | 1 | 0 | 0.960 | 0.500 | 1.000 | 0.500 | 0.667 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_270517.jpg | 7 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_271039.jpg | 9 | 5 | 1 | 0.600 | 0.643 | 0.900 |
| adasind_295948.jpg | 2 | 1 | 1 | 0.667 | 0.667 | 0.667 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 4 | 0 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 6 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 4 | 0 | 0 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 1 | 0 | 2 | 2 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
