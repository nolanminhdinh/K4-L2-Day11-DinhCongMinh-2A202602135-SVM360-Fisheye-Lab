# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy tắc riêng? Vì sao?
   - Trả lời: Đây không phải là lỗi `DUPLICATE` mà bắt buộc cần một quy tắc xử lý riêng (Seam / Cross-Camera Policy). Ở hệ thống SVM 360, các góc xe có vùng chồng lấn (overlap/seam) giữa hai camera liền kề (ví dụ Front và Left). Một vật thể thực tế tại vị trí này sẽ xuất hiện trên cả hai luồng ảnh với hai góc nhìn, độ chiếu sáng và méo thấu kính khác nhau. Trong không gian ảnh 2D gốc của từng camera, mỗi box đại diện cho phép đo hợp lệ của cảm biến đó. Không được tự ý xóa một bên hay gán là DUPLICATE nếu chưa có pipeline hợp nhất BEV 3D; việc coi là DUPLICATE sẽ làm mất thông tin an toàn của camera thành phần.

2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.
   - Trả lời:
     + Giữ cùng track ID: Khi đối tượng duy trì sự hiện diện liên tục và quỹ đạo di chuyển logic trong tầm nhìn của camera.
     + Thêm keyframe: Khi đối tượng thay đổi hướng đột ngột, thay đổi dáng điệu/kích thước do đến gần hoặc méo hình fisheye tăng cao.
     + Trạng thái Outside: Khi đối tượng tạm thời khuất sau cột cản/thân xe hoặc ra ngoài rìa kính (lens_border) trong vài frame rồi xuất hiện lại.
     + Bằng chứng cần trước khi nối track qua 2 camera: (1) Timestamp đồng bộ phần cứng (hardware sync) chính xác cấp mili-giây, (2) Ma trận hiệu chuẩn ngoại (extrinsic calibration) chuyển đổi tọa độ pixel về tọa độ xe ego 3D, và (3) Chính sách gộp track (association policy) có ngưỡng IoU 3D và đối sánh đặc trưng nhận dạng (Re-ID).

3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`), bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?
   - Trả lời: Tại frame `adasind_140160.jpg` đối tượng vùng unreadable tọa độ (856, 868): Reference cố gắng vẽ box nhỏ mờ trong bóng cây, nhưng tôi nhận định đối tượng này mất ranh giới đặc trưng thị giác do thiếu sáng. Tôi đã giữ quan điểm dựa trên quy tắc R06/R11, gán nhãn `ignore_region` (`reason="unreadable"`) và lập phiếu leo thang `30_escalation_ticket.md`. Nếu làm lại slice này, tôi sẽ soi kỹ ngay từ bước P2 phần giao nhau giữa thân xe ego và rìa ảnh để không vẽ dư box L6 tại `adasind_128310.jpg`, giúp tiết kiệm thời gian sửa chữa ở vòng rework.
