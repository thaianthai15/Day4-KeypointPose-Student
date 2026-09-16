# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Nguyễn An Thái   Nhóm: ______   Ngày: 16/09/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 355/59/79|
| Thời gian trung bình mỗi ảnh | 4p |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_ear : 48%
2. right_ear : 28%
3. left_wrist : 21&

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Các khớp tai có tỷ lệ `v=1` cao vì thường bị tóc, đầu hoặc góc nhìn che khuất. 
Cổ chân và đầu gối có tỷ lệ `v=1` thấp hơn nhưng vẫn khó xác định khi cơ thể bị cắt ở phía dưới hoặc bị quần áo/vật thể che. 
Tỷ lệ `v=1` cao thể hiện khớp thường bị che, nhưng không hoàn toàn đồng nghĩa với việc khớp đó khó xác định vị trí giải phẫu. 
Ví dụ, tai có thể xác định được vị trí gần đầu dù bị tóc che, nên cần đặt điểm và chọn `v=1`, không chọn `v=0`.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.881 | 0.897 |
| OKS@0.50 | 0.931 | 0.966 |
| OKS@0.75 | 0.897 | 0.931 |
| Lỗi `dao_trai_phai` | 1 | 0 |
| Lỗi `nham_nguoi` | 2 | 1 |
| Lỗi `xoa_khop_bi_che` | 5 | 3 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- train_01.jpg / người thứ 2 / ban đầu đặt left_knee, right_knee ra khỏi khung hình, vẫn để label, nhưng sau đó để outside vì đã ra khỏi khung hình
- train_13.jog / người thứ 3 / ban đầu không label người ở xa nhất vì mờ, không rõ, nhưng sau đó đã label lại cả skeleton
- train_16.jpg / người thứ 2 / ban đầu không label right_eye và right_ear vì nghĩ bị che, nhưng sau đó đã label lại vì vẫn có thể nhìn thấy

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?
- `train_02.txt`, người #1:
  - `left_shoulder/right_shoulder` có dấu hiệu bị đảo.
  - `left_hip/right_hip` có dấu hiệu bị đảo.
- Ảnh dễ, trong quá trình label thì bị rối do quá nhiều điểm 
<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.845 | 0.845 | 0.0 |
| pose_mAP50-95 | 0.6853 | 0.6908 | 0.0055 |
| pose_precision | 0.9734 | 0.9792 |0.0058 |
| pose_recall | 0.8462 | 0.8462 | 0.0 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
- `pose_mAP50-95` tăng từ `0.6853` lên `0.6908`, chênh lệch: 0.0055
Điều này cho thấy sau fine-tune, model có cải thiện nhẹ về độ chính xác vị trí keypoint trên tập test.
Tuy nhiên, mức tăng nhỏ nên chưa thể kết luận rằng 20 ảnh đã giúp model học được một khái niệm hoàn toàn mới. Có thể tập dữ liệu đã giúp model thích nghi nhẹ với tư thế, góc nhìn hoặc kiểu ảnh trong bộ dữ liệu này.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
   box_mAP50-95 = 0.8041 - pose_mAP50-95 = 0.6908 -> chênh lệch: 0.1133
Model xác định bounding box của người tốt hơn xác định chính xác skeleton. Với Keypoint Pose, model phải dự đoán vị trí của 17 khớp trên mỗi người, trong khi bounding box chỉ cần bao quanh toàn bộ người. Các khớp như tai, khuỷu tay, đầu gối và cổ chân thường bị che, nằm ngoài ảnh hoặc khó xác định vị trí, nên pose mAP thấp hơn box mAP.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):
Một lỗi được ghi nhận trong kết quả đánh giá là lỗi nhầm người:
Ảnh: train_03.jpg
Người: #1
Keypoint: right_hip
Loại lỗi: nhầm người
Model hoặc nhãn dự đoán đã đặt keypoint right_hip sang cơ thể bên cạnh thay vì đúng người cần gán.
4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
Trong kết quả so sánh nhãn với gold, skeleton có OKS thấp nhất là:
train_13.jpg
Người #1
OKS = 0.000
Nguyên nhân: thiếu hẳn một người
Đúng là model đã đúng, tôi đã không label người ở xa nhất trong khung hình do nghĩ bị mờ.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
Ví dụ: train_01.jpg, người #2, keypoint left_knee.

Khi kiểm tra bằng công cụ, keypoint left_knee có tọa độ chuẩn hóa y = 1.001, tức là nằm ra ngoài khung ảnh. Vì vậy, keypoint này không được gán v=2 và phải chuyển thành v=0. Không nên đặt chấm xuống dưới ảnh hoặc đoán vị trí phần chân không xuất hiện. Rule được sử dụng là: keypoint nhìn thấy rõ thì v=2, keypoint bị che nhưng vẫn nằm trong ảnh thì v=1, còn keypoint nằm ngoài khung ảnh thì v=0.
