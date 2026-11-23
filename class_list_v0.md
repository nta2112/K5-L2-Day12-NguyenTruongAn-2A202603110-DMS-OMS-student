# Danh sách lớp v0 — Nguyen Truong An · G01

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| ví dụ | eye_state | open / closed / unknown | Phát hiện buồn ngủ (mắt nhắm lâu) | Có, trừ khi kính phản xạ |
| 1 | glasses | none / clear / sun / unknown | Nhận diện kính  phát hiện mắt | Có, nhưng kính râm có thể trông trong suốt, khó phân biệt clear/sun |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện tài xế mất tập trung | khó nội suy hướng nhìn |
| 3 | hand | left / right · driver / passenger | Nhận biết tay trên vô lăng; phát hiện tay buông hoặc dùng điện thoại khi lái | Có |
| 4 | on_wheel | yes / no / unknown | Cảnh báo tay rời vô lăng kéo dài trong chế độ lái thủ công | Có |
| 5 | phone | held / mounted / lap | Cấm tài xế cầm điện thoại khi lái; ghi log vi phạm | Có |
| 6 | face13 | 13 điểm + cờ occluded/outside | Đo tư thế đầu chính xác hơn box, phục vụ theo dõi hướng nhìn | Có |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| ví dụ | infant_seat | có / không, theo ghế | Nhắc quên trẻ trong xe; tắt túi khí ghế trước | Có (hình dạng) |
| 1 | person (seat) | rear_left / rear_middle / rear_right | Đếm người trên xe, phát hiện bỏ quên trẻ ngủ trong xe | Có |
| 2 | seatbelt | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây an toàn; phát hiện dây sai vị trí | Lúc có lúc không rõ |
| 3 | child_seat (occupied) | no / unknown | Tắt túi khí ghế có ghế trẻ em; nhắc kiểm tra ghế sau khi rời xe | Có |
| 4 | object (type) | bag / box / cup / other | Phát hiện vật lăn lổng có thể văng khi phanh gấp | Có hình dạng |
| 5 | infant_seat (facing) | rear / front | Ghế cho trẻ sơ sinh để rear an toàn hơn | Có (hướng ghế) |
| 6 | frame_meta (camera_blocked) | yes / no | Biết khi nào camera bị che để cảnh báo "hệ thống không hoạt động" | chỉ thấy khi khung tối hoặc toàn đen |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: SVIRO không có ai thắt dây an toàn, vậy lớp `worn_correct`/`worn_incorrect` chỉ học được từ D##. Khi train model OMS đa cảm biến, nên gộp `seatbelt` thành 1 lớp "không chắc" cho nguồn IR-sim, hay giữ 4 giá trị và chấp nhận mất lớp worn_* trên SVIRO?
   Khung ví dụ: S05_rgb 
   Bạn tạm gán thế nào và vì sao: gán `not_worn` vì thấy rõ không có dây; không dùng `worn_*` dù guideline cho phép để tránh dạy model rằng IR-sim cũng nhận ra dây.
2. Câu hỏi: Ảnh D## xoay 90°, `gaze_zone` đòi suy hướng nhìn trong hệ toạ độ của xe trong khi ảnh chỉ thấy tài xế, không thấy xe. Tiêu chí nào để phân biệt `road` với `center`/`cluster` khi chỉ có đầu và mắt?
   Khung ví dụ: D03
   Bạn tạm gán thế nào và vì sao: nhìn hướng trục mắt + hướng mặt so với trục dọc ảnh; không chắc thì `other` + ghi chú — nhưng điều này làm lớp `other` phình to.
