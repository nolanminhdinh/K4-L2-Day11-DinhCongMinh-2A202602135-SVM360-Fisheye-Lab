# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Vùng méo quang học biên (edge zone: adasind_128310.jpg, adasind_140160.jpg) | 5 ca (SPURIOUS, BOX_GEOMETRY, truncated) | Méo thấu kính fisheye ở rìa đạt cực đại, vật thể bị kéo giãn cong phi tuyến tính và cắt bởi lens_border, dễ gây nhầm lẫn ranh giới box | Ảnh fisheye gốc, đa giác lens_border, overlay so sánh L-R-M và bảng IoU sweep ở ngưỡng 0.5 và 0.7 |
| Vùng che khuất và bóng râm (mid zone: adasind_140160.jpg, adasind_230910.jpg) | 6 ca model SPURIOUS (M_only) và 1 ca IGNORE_SCOPE (unreadable) | Độ tương phản thấp trong bóng cây gây domain gap nặng cho model AI và dễ làm annotator phân vân giữa box mờ và ignore region | Ảnh crop chi tiết vùng bóng râm, model_compare.html, mã finding RM_noL và vé escalation ticket |

Giới hạn của kết luận từ ba frame ADASIND: Slice 3 frame chỉ cung cấp quan sát trên một góc nhìn camera trước duy nhất trong điều kiện ban ngày tiêu chuẩn. Kích thước mẫu nhỏ (20-23 đối tượng) chỉ đủ để phát hiện các lỗi định tính và kiểm chứng quy trình, không thể đại diện cho tỷ lệ phân phối lỗi thống kê của toàn bộ hệ thống SVM đa camera.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi:
- Để tránh hiện tượng tương quan chuỗi thời gian (temporal correlation - nhiều frame liên tiếp trong cùng một cảnh quay), quy trình lấy mẫu cần áp dụng khoảng cách tối thiểu giữa các frame (frame skipping, ví dụ 1 frame mỗi 3-5 giây) và phân tầng theo các điều kiện vận hành (ODD: ban ngày, chạng vạng, ban đêm, mưa, bãi đỗ ngầm hẹp).
- Kế hoạch này tập trung phân bổ tỷ trọng lớn cho các ca khó (hard cases chiếm ~43% tổng số 200 frame) nhằm tìm kiếm và rà soát lỗi biên (edge cases). Do đó, tỷ lệ lỗi trên tập 200 frame này chỉ mang tính định hướng chẩn đoán rủi ro (risk hunting), không đại diện cho tỷ lệ lỗi tự nhiên (prevalence / baseline error rate) trên 50.000 frame vận hành thực tế.
