# TEAM — Ngày 12

Mã bộ ảnh: **G09** · Hình thức: nhóm / cá nhân: **nhóm**

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Sỹ Kiên | 2A202603245 | có | Nguyễn Bảo Khánh | 41 |
| Nguyễn Bảo Khánh | 2A202603233 | có | Nguyễn Sỹ Kiên | 41 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `S03_rgb.png`, `S05_rgb.png`, `S06_rgb.png` (đối tượng: `infant_seat`, trường thuộc tính: `facing`): Hai bạn bất đồng về hướng quay `facing = rear` (Kiên) hay `facing = front` (Khánh). Kiên căn cứ theo tiêu chuẩn kỹ thuật an toàn ô tô quốc tế quy định nôi sơ sinh Group 0+ bắt buộc lắp ngược chiều chuyển động (`rear-facing`), còn Khánh căn cứ theo hướng mở của vòm quai nôi nhìn về phía trước xe. Ca này đã được đưa vào Câu hỏi leo thang số 1.

## Cá nhân

Mỗi người một mục, 1–2 dòng mỗi ý.

### NguyenSyKien-2A202603245
- Phần mình làm: Tự gán đủ 22 ảnh cốt lõi trên CVAT, thực hiện kiểm tra tự động Checkpoint A, B và Final; xuất dữ liệu diff đối chiếu với bạn Nguyễn Bảo Khánh và phân tích, xử lý toàn bộ 41 dòng disagreement; cập nhật chỉnh sửa bản v2 đạt chuẩn 0 lỗi 0 cảnh báo; hoàn thiện bộ tài liệu báo cáo.
- Điều mình học được hôm nay: Hiểu sâu sắc hệ toạ độ không gian cabin xe hơi (nguyên tắc gọi tên ghế theo xe khi camera quan sát ngược chiều), cách nhận diện và phân biệt nôi sơ sinh xách tay với ghế an toàn trẻ em lớn dựa trên tỷ lệ kích thước hình học, và bản chất vật lý của camera NIR (hiện tượng mất màu sắc, đốm chói phản xạ trên tròng kính cần đánh cờ occluded/unknown thay vì phỏng đoán).
