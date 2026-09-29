# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | MISSING | 1 |
| center | B3 | SPURIOUS | 4 |
| center | C0 | MISSING | 1 |
| edge | B3 | ATTRIBUTE | 1 |
| edge | B3 | BOX_GEOMETRY | 1 |
| edge | B3 | MISSING | 1 |
| edge | B3 | SPURIOUS | 4 |
| edge | C0 | SPURIOUS | 2 |
| mid | B3 | ATTRIBUTE | 1 |
| mid | B3 | BOX_GEOMETRY | 3 |
| mid | B3 | MISSING | 1 |
| mid | B3 | SPURIOUS | 3 |
| unknown | B3 | IGNORE_SCOPE | 1 |

## Top defects
- SPURIOUS: 13 (ví dụ frame adasind_019560.jpg)
- MISSING: 4 (ví dụ frame adasind_019560.jpg)
- BOX_GEOMETRY: 4 (ví dụ frame adasind_140160.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Lỗi SPURIOUS chiếm ưu thế lớn (13 ca), trong đó phần lớn thuộc về model YOLO26m (nguyên nhân `E4_model_domain`) do sự dịch chuyển miền dữ liệu (domain gap). Ảnh fisheye có độ cong quang học lớn khiến các vật thể ngoại cảnh như hàng rào, bóng cây hoặc vệt phản quang mặt đường bị model dự đoán nhầm thành phương tiện. Về phía người gán nhãn, lỗi SPURIOUS ban đầu xuất hiện do chưa quen ranh giới cắt với rìa kính lens_border và ngưỡng kích thước H=40px (`E1_annotator_error`).
- Cách sửa và ai nhận việc (`owner`): 
  1. Với lỗi annotator: Học viên (`annotator`) đã thực hiện rework (P5) trên CVAT, xóa bỏ box thừa L6 tại `adasind_128310.jpg` và rà soát lại các box sát biên, đưa số lượng spurious về 0 ở bản v2 (chứng minh qua `delta.md`).
  2. Với lỗi model: Nhóm phát triển AI (`ai_team`) cần bổ sung kỹ thuật fisheye augmentation và huấn luyện lại bộ trích xuất đặc trưng trên tập dữ liệu camera góc rộng đa camera.
- Bằng chứng: Dòng finding `adasind_128310.jpg:L6` trong `findings.csv`, báo cáo so sánh `model_compare.html` và `delta.md`. Quy tắc đối chiếu: R01 (ngưỡng H=40) và R05 (thuộc tính truncated/occluded). Ảnh minh chứng lưu tại `submission/screenshots/`.

