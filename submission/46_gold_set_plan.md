# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Ngược sáng chói bình minh/hoàng hôn; người đi bộ cắt ngang sát mũi xe; mưa đọng ống kính | Độ tương phản giảm mạnh, méo hình lớn ở mép dưới sát đầu xe ego, vật thể bị cắt bởi lens border | Giữ nguyên không gian ảnh fisheye gốc (raw); lưu thông số intrinsic/extrinsic và timestamp đồng bộ | 2 annotator gán nhãn độc lập (double-blind) + 1 senior reviewer phân xử đồng thuận (consensus) |
| rear | Thiếu sáng ban đêm; lùi chuồng sát chướng ngại vật thấp; đèn pha xe sau rọi trực diện | Bị bão hòa sáng do đèn pha rọi thẳng; bóng đen gầm xe dễ nhầm là vật cản hoặc bỏ sót chướng ngại vật | Giữ nguyên ảnh raw và mapping mặt đất phẳng (ground plane) để tính toán khoảng cách an toàn | Kiểm tra chéo giữa camera lùi và cảm biến khoảng cách/sonar; review độc lập trước khi chốt nhãn |
| left | Xe máy lách sát khe gương hông; phương tiện đi vào vùng seam trước-trái / sau-trái | Méo cong cực hạn ở rìa gương; một vật bị chia cắt xuất hiện đồng thời trên 2 camera ở vùng chồng | Giữ nguyên ranh giới lens_border và ma trận biến đổi sang hệ tọa độ xe ego | So sánh song song frame của camera hông và camera trước/sau để xác thực identity trước khi chốt |
| right | Cập lề sát vỉa hè; chướng ngại vật thấp, cành cây, người đi bộ khuất bóng râm bên phải | Dễ nhầm lẫn giữa vỉa hè, rác ven đường và chướng ngại vật thực sự; góc chết cột A/B | Giữ nguyên ảnh fisheye gốc và tọa độ gắn camera để kiểm tra chiều cao chướng ngại vật | 2 reviewer độc lập rà soát kỹ ngưỡng kích thước (H>=40px) và thuộc tính occluded/truncated |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): Khi có sự thay đổi về phần cứng cảm biến (thay loại ống kính, độ phân giải, góc mở FOV), vị trí gắn camera trên thân xe (extrinsic thay đổi), hoặc khi guideline gán nhãn có sự cập nhật (thay đổi định nghĩa class, ngưỡng lọc kích thước H, quy ước rider/vehicle).
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: Cần bằng chứng đồng bộ thời gian chính xác (hardware-synchronized timestamp), ma trận hiệu chuẩn ngoại (extrinsic calibration) chính xác giữa hai camera liền kề, và thuật toán tính toán giao thoa 3D trên hệ quy chiếu thân xe (ego coordinates). Nếu chưa đủ 3 yếu tố này, quy định (policy) bắt buộc phải gán nhãn hai box độc lập trên từng camera tương ứng, không được tùy tiện gộp chung track ID.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: Tập ảnh ADASIND chỉ thu thập từ một camera hướng trước với điều kiện vận hành và góc nhìn hạn chế, không đại diện cho đặc tính quang học, mức độ che khuất của thân xe (như thân xe bên hông hay cản sau), và các vấn đề vùng chồng (seam) phức tạp của hệ thống 4 camera SVM quanh xe.

