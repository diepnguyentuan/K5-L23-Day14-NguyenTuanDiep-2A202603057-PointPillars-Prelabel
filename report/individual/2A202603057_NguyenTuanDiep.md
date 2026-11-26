# Báo cáo Day 14 — Nguyễn Tuấn Điệp — 2A202603057

- Mã học viên dùng với `--student`: `2A202603057`
- `seed_tag` trong `frames_A.txt`: `393590736f`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- Tham số tôi nghĩ giảm công sửa nhiều nhất: Tăng `score_thr` (khoảng `0.4`–`0.5`) kết hợp tăng nhẹ `min_points` (khoảng `5`–`10`).
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?): Quan sát 3 ảnh BEV tập A (`s02f31`, `s03f52`, `s05f31`) và quá trình sửa tay trên CVAT cho thấy **box thừa nhiều áp đảo** so với box sót (cấu hình gốc sinh tới 102 box nhưng chỉ có 35 vật thể thật cần giữ). Phần lớn box thừa là các hộp `Cyclist`, `Pedestrian` và `Car` ảo ở lề đường/bụi cây/vùng xa có điểm tin cậy thấp (`score < 0.4`) và rất ít điểm LiDAR. Dù mỗi hộp xóa chỉ tốn `0.3` điểm (thấp hơn `1.0` điểm khi thêm hộp sót), tổng số hộp thừa quá lớn nên lọc bớt bằng `score_thr` và `min_points` được kỳ vọng sẽ giảm mạnh chi phí xóa mà không làm mất nhiều xe thật (chủ yếu là `Car`/`Bus` rõ điểm).

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | | | | |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_2A202603057/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_2A202603057/frames_B.txt --config d14_2A202603057/best_config.json --gt d14_2A202603057/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
