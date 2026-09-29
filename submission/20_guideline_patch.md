# Guideline patch

- **Rule mới đề xuất:** R11 — Quy chuẩn phân định vật thể mờ/che khuất trong bóng râm (`unreadable` threshold). Nếu vật thể bị che khuất trên 60% diện tích hoặc nằm trong vùng bóng râm/chói sáng làm mất hoàn toàn đường bao nhận dạng (không nhận biết được bằng mắt người mà chỉ dựa vào suy đoán), bắt buộc sử dụng polygon `ignore_region` với attribute `reason="unreadable"`, không được vẽ bounding box phỏng đoán.
- **Áp dụng cho:** Toàn bộ 6 class chuyển động (`Car`, `Bus`, `Truck`, `ThreeWheeler`, `Bike`, `Pedestrian`) tại các vùng biên `mid` và `edge`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Luật hiện hành R06 chỉ nêu định nghĩa định tính "vật không đọc được vì mờ/che gần hết" nhưng chưa có ngưỡng che khuất cụ thể, dẫn đến sự bất đồng giữa teaching reference (vẽ box nhỏ mờ) và annotator (coi là don't-care).
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** Vòng Rework (P5) và các đợt mở rộng dữ liệu SVM 4 camera.
