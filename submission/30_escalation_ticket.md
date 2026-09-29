# Escalation ticket

## Ticket 1

- **Frame:** adasind_140160.jpg
- **Ảnh chụp:** submission/screenshots/escalation_ticket_1.png
- **Expected impact:** Nếu reference gán box cho các đối tượng quá mờ trong bóng râm (dưới ngưỡng nhận diện hình học rõ ràng), mô hình AI khi học sẽ bị nhiễu do nhầm lẫn giữa bóng cây và phương tiện, kéo tụt chỉ số phát hiện thực tế trên xe tự hành.
- **Owner:** data_ops
- **Recommendation:** Thống nhất cập nhật nhãn chuẩn: chuyển đổi đối tượng tại tọa độ (856, 868) sang polygon `ignore_region` với lý do `reason="unreadable"` theo quy tắc R06/R11, loại bỏ khỏi tập tính toán mAP bắt buộc.
