# Tự đánh giá — Nguyễn Sỹ Kiên · G09

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S02_rgb.png` | `child_seat` | `seat_flip` | Ghế nằm bên phải ảnh ($x \approx 552 \rightarrow 845$) nhưng lúc đầu gán `rear_right` do nhìn theo màn hình thay vì tính theo xe (camera nhìn lùi: phải ảnh là ghế sau bên trái `rear_left`) | Đã sửa trong v2 |
| `S04_rgb.png` | `child_seat` | `wrong_class` | Vật thể ở vị trí $x \approx 0 \rightarrow 373$ là nôi sơ sinh xách tay (dáng thấp, $y \ge 322\text{ px}$, có quai vòm) nhưng gán nhầm thành `child_seat` | Đã sửa trong v2 (`infant_seat`) |
| `D01.png` | `face` / `face13` | `ok` | Nhận diện đúng đốm chói lóa của đèn LED hồng ngoại 940nm trên tròng kính, gán `unknown` cho mắt và bật cờ `occluded = 1` cho các điểm mí mắt thay vì đoán | Đạt chuẩn Rule 4.4-1 |
| `D04.png` | `face` / `face13` | `ok` | Góc quay đầu nghiêng nhìn gương phải, phân biệt đúng mắt trái hướng về camera thấy rõ khe mở (`eye_left = open`, cờ `0`) và mắt phải bị khuất (`eye_right = unknown`, cờ `1`) | Đạt chuẩn Rule 4.5 |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

- **Lỗi:** Nhầm lẫn nhãn giữa ghế trẻ em lớn (`child_seat`) và nôi sơ sinh (`infant_seat`) trên ảnh OMS, cùng với việc thỉnh thoảng bị quán tính phản xạ gán vị trí ghế theo mắt nhìn trên ảnh thay vì tính theo xe.
- **Vì sao mình mắc:** Chưa chú ý kỹ đặc điểm chiều cao của đối tượng ($y_{tl} \approx 200$ là ghế cao có tựa đầu, còn $y_{tl} \approx 320$ là nôi thấp) và chưa luôn luôn đặt bản thân vào vị trí người ngồi trong xe nhìn về phía trước khi camera OMS quay ngược lại.
- **Lần sau tránh bằng cách:** 
  1. Luôn so sánh chiều cao $y_{tl}$ với mốc tựa lưng ghế để phân loại dứt điểm giữa `child_seat` và `infant_seat`.
  2. Vẽ một quy ước trực quan ngay trước màn hình: "Trái ảnh = Bên phải xe (`rear_right`) — Phải ảnh = Bên trái xe (`rear_left`)".

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
- **Dòng học hỏi:** `S08_rgb.png`, đối tượng ghế ở vị trí $x \approx 548 \rightarrow 840$. Bạn Nguyễn Bảo Khánh gán là `child_seat`, trong khi mình gán là `infant_seat`.
- **Bài học:** Chiếc ghế này có phần tựa lưng vươn cao lên tận toạ độ $y = 202.5\text{ px}$ (tổng chiều cao $415\text{ px}$, giống hệt ghế `child_seat` ở S01 và S02), hoàn toàn khác với nôi sơ sinh có vòm thấp. Khi đối chiếu với bạn Khánh và kiểm tra lại toạ độ hình học, mình nhận ra bạn Khánh đã quan sát chính xác kết cấu khung ghế. Mình đã sửa lại thành `child_seat` trong bản `export_final_v2.zip`.

