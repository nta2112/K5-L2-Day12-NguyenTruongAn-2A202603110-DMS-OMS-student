# Tự đánh giá — Nguyen Truong An · G01

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S06_rgb | infant_seat | seat_flip | Ban đầu để seat=driver (mặc định CVAT), sửa lại rear_left | có |
| S05_rgb | child_seat | guess | occupied đã điền no cho ghế không thấy rõ bên trong; sửa thành unknown | có |
| D01 | face13 (right_eye_*) | flag | 4 điểm mắt phải ở ngoài/bị che nhưng chưa bật cờ; xem lại trên CVAT và đặt cờ outside | có |
| D04 | hand | lr_flip | 2 box hand từng cùng side=right (bắt ở checkpoint trước); đã sửa 1 box thành left | có |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: quên đổi giá trị mặc định của thuộc tính khi vẽ box mới (seat=driver, occupied hiểu nhầm là có "yes").

Vì sao mình mắc: CVAT tự điền giá trị đầu danh sách; mình vẽ xong là sang box tiếp theo mà không mở DETAILS kiểm tra lại.

Lần sau tránh bằng cách: sau mỗi box, lập tức mở DETAILS xác nhận từng thuộc tính trước khi Ctrl+S; nhớ 3 giá trị "không tồn tại" của guideline (occupied=yes, worn_* trên SVIRO, light≠unknown trên SVIRO).

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:

- D01.png · person · seatbelt: mình `worn_incorrect`, bạn `worn_correct`. Khi soi lại trên CVAT, dải dây đi từ vai xuống hông phía đối diện nên bạn đúng theo 4.7 — mình vội vàng vì thấy dải lệch vai trên ảnh nhỏ. Bài học: trước khi kết luận worn_incorrect phải thấy rõ dải dưới nách/sau lưng, không suy từ box nhỏ.
- S05_ir.png · child_seat · occupied: bạn điền `yes` — giá trị không tồn tại trong schema (4.8), mình đúng khi giữ `no`/`unknown`. Hai người nhất quán cũng không có nghĩa là đúng; guideline mới là căn cứ.
