# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_270517.jpg
- L8 mid IGNORE_SCOPE
## adasind_271039.jpg
- L1 center SPURIOUS
- L2 center SPURIOUS
- L8 center SPURIOUS
- L13 center SPURIOUS
- L14 center SPURIOUS
- R10 center MISSING
## adasind_295948.jpg
- L1 mid IGNORE_SCOPE
- L2 mid IGNORE_SCOPE
- L3 center IGNORE_SCOPE
- L7 mid IGNORE_SCOPE
- L6+R1 center WRONG_CLASS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 12 | 10 | 2 | 6 |
| mid | 5 | 5 | 0 | 0 |
| edge | 3 | 3 | 0 | 0 |
