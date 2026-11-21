# Danh sách lớp v0 — Nguyễn Sỹ Kiên · G09

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face.eye_left / eye_right` | `open`, `closed`, `unknown` | Phát hiện tài xế buồn ngủ hoặc ngủ gật (mắt nhắm liên tục > 1.5–2 giây) để tính chỉ số PERCLOS (Percentage of Eye Closure) kích hoạt chuông cảnh báo | Có, thấy rõ khe mắt trên camera NIR; trừ trường hợp đốm phản xạ LED trên kính hoặc kính râm tối thì ghi `unknown` |
| 2 | `face.gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Giám sát mức độ tập trung của tài xế (Distraction Detection); cảnh báo khi mắt rời khỏi vùng đường (`road`) quá 2 giây (ví dụ nhìn xuống đùi `lap` hoặc bảng điều khiển `center`) | Có, ước lượng được dựa trên hướng đầu (Head Pose) và vị trí con ngươi trên ảnh NIR |
| 3 | `face.glasses` | `none`, `clear`, `sun`, `unknown` | Nhận diện phụ kiện mắt để bộ lọc thuật toán điều chỉnh tham số nhận diện mắt phù hợp (tránh false positive khi tài xế đeo kính cận có phản quang hoặc kính râm) | Có, kính cận thấy rõ gọng và tròng trong suốt; kính râm có thể trong suốt dưới ánh sáng hồng ngoại |
| 4 | `face13` | Skeleton 13 điểm (mắt, mũi, môi) | Ước lượng tư thế 3D của đầu (Head Pose Estimation: Yaw, Pitch, Roll) để hỗ trợ tính hướng nhìn và nhận diện hành vi ngáp (Yawning Detection) qua độ mở môi | Có, 13 điểm đặt chính xác theo mép viền giải phẫu; điểm bị che do góc nghiêng/tay cầm vật phải đánh cờ `occluded` |
| 5 | `hand.on_wheel` | `yes`, `no`, `unknown` | Phát hiện tài xế có đang đặt tay trên vô lăng hay không (Hands-Off Detection - HOD) khi xe bật chế độ tự lái Level 2 / ADAS, bắt buộc tài xế sẵn sàng tiếp quản | Có, phân biệt rõ vị trí bàn tay so với vành vô lăng trên ảnh NIR |
| 6 | `phone.state` | `held`, `mounted`, `lap` | Phát hiện tài xế sử dụng điện thoại khi đang lái xe (hành vi gây mất tập trung thị giác và thao tác tay nghiêm trọng) để phát âm thanh nhắc nhở | Có, nhận diện được khi thấy rõ hình dạng cạnh chữ nhật, góc máy hoặc bề mặt màn hình phát sáng |
| 7 | `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Kiểm tra tài xế đã thắt dây an toàn đúng cách hay chưa để kích hoạt chuông cảnh báo và cấu hình lực kích hoạt túi khí khi xảy ra va chạm | Có, thấy được đường chéo dây an toàn nếu tương phản tốt với áo dưới ánh sáng NIR |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person.seat` | `driver`, `front_passenger`, `rear_left`, `rear_middle`, `rear_right` | Xác định vị trí người ngồi trên xe để điều chỉnh vùng điều hòa (Smart HVAC Zone Control) và chỉ kích hoạt cảnh báo thắt dây / túi khí tại đúng ghế có người | Có, nhận dạng rõ hình dáng cơ thể người qua hình khối đầu và thân |
| 2 | `child_seat.seat` | Ghế theo xe, `occupied: no, unknown` | Phát hiện ghế an toàn trẻ em (cho trẻ từ 1–7 tuổi) nhằm điều chỉnh áp lực túi khí rèm và túi khí bên hông để tránh chấn thương cho trẻ em | Có, nhận diện dễ dàng qua kích thước lớn và tựa lưng cao đặc trưng |
| 3 | `infant_seat.facing` | Ghế theo xe, `facing: rear, front` | Phát hiện nôi xách sơ sinh (đặc biệt nôi lắp ngược `rear-facing`) để tự động ngắt túi khí ghế trước (tránh túi khí va đập nguy hiểm) và bật tính năng chống bỏ quên trẻ (Child Presence Detection - CPD theo chuẩn Euro NCAP) | Có, nhận diện qua kiểu dáng nôi thấp và quai xách vòm cong |
| 4 | `object.type` | `bag`, `box`, `cup`, `other`, kèm `seat` | Phân biệt đồ vật (hành lý, ba lô, thùng hàng) để tránh báo động giả cảnh báo thắt dây an toàn (SBR False Alarm) khi chỉ đặt hành lý nặng lên ghế ngồi | Có, nhận diện dựa trên hình khối học của đồ vật (hình hộp, hình trụ, quai xách) |
| 5 | `frame_meta.camera_blocked` | `yes`, `no` | Hệ thống tự chẩn đoán (Self-Diagnostic): phát hiện camera trong cabin bị che khuất (do hành lý che, bụi bẩn, hoặc áo che) để thông báo cho tài xế kiểm tra | Có, thấy rõ toàn bộ hoặc phần lớn khung hình bị mờ đục hoặc tối đen bất thường |
| 6 | `person.seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Cảnh báo nhắc nhở thắt dây an toàn cho hành khách hàng ghế sau (Seatbelt Reminder - SBR bắt buộc theo quy định an toàn xe mới) | Có, thấy được nếu dải dây an toàn có độ tương phản độ sáng với áo trên ảnh IR |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Quy định gán nhãn thuộc tính `facing` của `infant_seat` được tính theo hướng nhìn của khuôn mặt em bé (face orientation) hay theo hướng của phần đỉnh kết cấu nôi/quai xách so với chiều tiến của xe?
   - **Khung ví dụ:** `S03_rgb.png` (và `S05_rgb.png`, `S06_rgb.png`).
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `facing = rear` vì theo quy chuẩn kỹ thuật an toàn xe hơi quốc tế, nôi xách sơ sinh (Group 0/0+) luôn bắt buộc phải lắp ngược chiều xe chạy (rear-facing, mặt em bé nhìn về phía sau xe) để bảo vệ đốt sống cổ của trẻ sơ sinh khi phanh gấp. Khi review chéo với bạn Nguyễn Bảo Khánh, bạn gán `front` do quan sát theo hướng mở của vòm quai nôi. Cần văn bản guideline chuẩn hóa định nghĩa này để thống nhất dữ liệu huấn luyện.
2. **Câu hỏi:** Trong trường hợp đồ vật đặt bên trong ghế trẻ em hoặc nôi em bé (ví dụ nôi sơ sinh có phủ khăn hoặc đặt túi đồ bên trong), kích thước bounding box của `child_seat`/`infant_seat` nên ôm sát phần khung ghế nhìn thấy được hay ôm trọn cả phần đồ vật bên trong?
   - **Khung ví dụ:** `S01_rgb.png` / `S01_ir.png` (ghế trẻ em có chứa đồ vật).
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán 2 bounding box riêng biệt (`child_seat` và `object`) ôm sát từng thực thể theo Rule 4.8. Tuy nhiên, trong bài toán Object Detection, hai box chồng chéo với IoU cao dễ bị thuật toán Non-Maximum Suppression (NMS) triệt tiêu box nhỏ hơn nếu chọn nhầm threshold. Guideline cần hướng dẫn rõ xem có nên thiết lập mối quan hệ cha-con (hierarchical relation / attribute) thay vì 2 box phẳng trùng toạ độ hay không.
