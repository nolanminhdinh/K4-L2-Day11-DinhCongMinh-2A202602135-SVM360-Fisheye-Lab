# Sensor context

- **Rig:** Cảm biến là camera fisheye (mắt cá) trường nhìn siêu rộng (FOV xấp xỉ 180°–195°), được gắn ở vị trí phía trước xe (thường ở nắp ca-pô, lưới tản nhiệt hoặc kính chắn gió hướng ra trước). Góc nhìn bao quát toàn bộ quang cảnh phía trước cùng hai bên hông xe, với đặc trưng méo hình quang học dạng cầu (fisheye distortion) tăng dần từ tâm ra viền.
- **ego_body:** Thân xe ego xuất hiện ở phần đáy khung hình (vùng cản trước, mép ca-pô hoặc góc nắp máy), xuất hiện ở 46/48 frame trong tập ảnh ADASIND (ngoại trừ một số frame như `006840` và `271039` không nhìn thấy thân xe). Vùng này bị camera gắn trên xe thu vào và cần được gán nhãn loại trừ qua polygon `ego_body`.
- **Vòng kính (lens circle):** Vòng kính hiển thị dưới dạng đường tròn quang học lớn nằm ở trung tâm ảnh, chiếm khoảng 85%–90% diện tích khung hình chữ nhật. Phần không gian 4 góc và rìa ngoài vòng kính là các góc tối/vành đen không mang thông tin thị giác, được phân định bởi polygon `lens_border`.

