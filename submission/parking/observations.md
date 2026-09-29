# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): 
  1. Vạch thứ nhất: Đoạn sơn trắng phân chia ô đỗ ở tiền cảnh gần trung tâm bên phải (chạy chéo từ khoảng x=416, y=648 xuống sát mép dưới x=534, y=719), phân chia rõ ranh giới giữa hai ô đỗ xe phía trước.
  2. Vạch thứ hai: Đoạn sơn trắng phân chia ô đỗ ở tiền cảnh phía bên phải (chạy từ x=725, y=667 kéo dài về phía góc phải ảnh x=960, y=705).
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Không vẽ dải sơn mờ phân cách lối đi ở hậu cảnh xa và các đường phản quang/vệt nước đọng gần hàng rào xa, vì chúng chỉ là mép đường hoặc chỉ dẫn hướng di chuyển của bãi xe, không thực hiện chức năng phân chia giới hạn của một ô đỗ xe riêng biệt.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Polygon `free_space` bao trùm phần mặt đường nhựa trống của lối xe chạy chính giữa hàng ô đỗ tiền cảnh và dãy ô đỗ trung cảnh (từ x=0 đến x=960, y trong khoảng 550 đến 650). Ranh giới dừng lại trước các vạch đỗ xe của dãy tiếp theo và mép ngoài lối đi; không có vật cản (xe, người, bồn cây) che khuất trong phạm vi lối đi này.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): Không có.

