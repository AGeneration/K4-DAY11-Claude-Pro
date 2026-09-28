# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_060000.jpg
- L4 center IGNORE_SCOPE
- R5 mid MISSING
- R6 mid MISSING
- R7 center MISSING
- R9 center MISSING
- R10 mid MISSING
## adasind_086220.jpg
- L6 center SPURIOUS
## adasind_102750.jpg
- L2 center SPURIOUS
- R5 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 9 | 6 | 3 | 2 |
| mid | 8 | 5 | 3 | 0 |
| edge | 3 | 3 | 0 | 0 |
