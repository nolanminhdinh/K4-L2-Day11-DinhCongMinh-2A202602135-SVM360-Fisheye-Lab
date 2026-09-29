# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_019560.jpg
- L1 edge SPURIOUS
- L2 edge SPURIOUS
- L3 edge SPURIOUS
- L4 edge SPURIOUS
- L5 edge SPURIOUS
- L6 mid SPURIOUS
- R1 center MISSING
- R2 center MISSING
- R3 edge MISSING
- R4 mid MISSING
- R5 center MISSING
- R6 mid MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 3 | 0 | 3 | 0 |
| mid | 2 | 0 | 2 | 1 |
| edge | 1 | 0 | 1 | 5 |
