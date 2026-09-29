# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 8 | 0 | 0 | 3 | 3 | — |
| mid | 9 | 0 | 0 | 4 | 3 | — |
| edge | 3 | 0 | 1 | 1 | 2 | SPURIOUS (1) |

## Nhận xét

- Zone người (L) và model (M) gãy nhiều nhất: Người gán nhãn (L) đạt độ chính xác gần như tuyệt đối ở vùng center và mid (0 missing, 0 spurious); chỉ xuất hiện 1 lỗi SPURIOUS ở vùng edge do biến dạng quang học mạnh ở rìa ngoài vòng kính. Ngược lại, model (M) gãy nhiều nhất ở vùng mid (4 missing, 3 thừa) và center (3 missing, 3 thừa), tỷ lệ bỏ sót và phát hiện giả của model chiếm tới 35-40% tổng số đối tượng.
- Giả thuyết nguyên nhân và giới hạn slice: Model YOLO26m bị hiện tượng domain gap/shift khi suy luận trên ảnh camera fisheye góc rộng có độ méo hình học cầu lớn, dẫn đến việc ước lượng bounding box bị trượt IoU hoặc nhầm lẫn vật thể nhỏ/bị che khuất một phần trong nền phức tạp. Giới hạn slice 3 frame cung cấp tập mẫu kiểm chứng nhanh (20 đối tượng), chưa đại diện đủ cho các điều kiện ánh sáng cực đoan, ban đêm hoặc mật độ giao thông dày đặc của toàn bộ hệ thống SVM 4 camera.

