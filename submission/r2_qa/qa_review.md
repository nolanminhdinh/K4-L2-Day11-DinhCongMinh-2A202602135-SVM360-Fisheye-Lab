# QA review · B4-edge

Mã khóa: 4378-2470

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_236370.jpg | L3 | R05 | Xe ô tô ở mép trái (0, 730, 54, 784) bị cắt bởi biên ảnh, gán đúng truncated=true theo quy tắc R05. |
| adasind_236370.jpg | L2 | R05 | Xe hai bánh ở sát rìa kính (900, 881, 1014, 1015) được gán edge_zone=true hợp lệ theo quy định vùng rìa. |
| adasind_258420.jpg | L2 | R01 | Xe ba bánh ThreeWheeler (290, 762, 452, 946) ôm sát thân xe, phân loại đúng ThreeWheeler không nhầm sang Car. |
| adasind_310008.jpg | L5 | R05 | Người đi bộ ở mép trái (16, 867, 80, 1033) bị người đi bộ L4 che một phần, bật occluded=true chính xác. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
