# Visibility report

- Thư mục nhãn: `dataset/labels/train`
- 20 ảnh, 29 skeleton, trung bình 14.28 khớp có v > 0 mỗi người
- Tổng: v=2 355 | v=1 59 | v=0 79

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 0 | 7 | 0% |
| 1 | left_eye | 21 | 1 | 7 | 3% |
| 2 | right_eye | 22 | 1 | 6 | 3% |
| 3 | left_ear | 11 | 14 | 4 | 48% |
| 4 | right_ear | 17 | 8 | 4 | 28% |
| 5 | left_shoulder | 27 | 2 | 0 | 7% |
| 6 | right_shoulder | 28 | 1 | 0 | 3% |
| 7 | left_elbow | 23 | 2 | 4 | 7% |
| 8 | right_elbow | 26 | 1 | 2 | 3% |
| 9 | left_wrist | 19 | 6 | 4 | 21% |
| 10 | right_wrist | 20 | 6 | 3 | 21% |
| 11 | left_hip | 24 | 5 | 0 | 17% |
| 12 | right_hip | 27 | 2 | 0 | 7% |
| 13 | left_knee | 18 | 3 | 8 | 10% |
| 14 | right_knee | 20 | 1 | 8 | 3% |
| 15 | left_ankle | 15 | 3 | 11 | 10% |
| 16 | right_ankle | 15 | 3 | 11 | 10% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
