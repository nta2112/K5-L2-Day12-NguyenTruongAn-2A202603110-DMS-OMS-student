# Khai báo dùng AI — Nguyen Truong An

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude Code (CLI) | Hướng dẫn quy trình lab: tạo project/task CVAT, ý nghĩa các label/thuộc tính theo Guideline Cabin v1.0, cách phân biệt trái/phải theo người vs theo xe | Hiểu đề và quy trình; tự gán nhãn trên CVAT theo hướng dẫn | Có — đối chiếu từng ý với GUIDE.md; cabin_check check 0 lỗi ở Checkpoint A/B và lần cuối |
| 2 | Claude Code (CLI) | Ý nghĩa thuộc tính frame_meta (modality/light/camera_blocked) và light cho ảnh NIR | Gán modality đúng theo loại ảnh; light=unknown cho D## | Có — cabin_check không còn WARN về light ở lần kiểm cuối |


