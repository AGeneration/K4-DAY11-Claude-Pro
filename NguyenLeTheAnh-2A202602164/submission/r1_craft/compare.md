# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_062370.jpg
- L3+R9 center BOX_GEOMETRY
- L4+R4 mid WRONG_CLASS
- R7 center MISSING
- R8 center MISSING
## adasind_069450.jpg
## adasind_117120.jpg
- L3 center SPURIOUS
- L7 center SPURIOUS
- R3 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 13 | 9 | 4 | 3 |
| mid | 5 | 4 | 1 | 1 |
| edge | 2 | 2 | 0 | 0 |
