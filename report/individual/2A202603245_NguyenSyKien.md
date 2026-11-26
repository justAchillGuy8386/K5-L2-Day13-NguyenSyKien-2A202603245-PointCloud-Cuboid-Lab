# Báo cáo Day 13 — Nguyễn Sỹ Kiên, 2A202603245

> **Cách dùng mẫu này:** đổi tên file thành `<MSSV>_<HoTen>.md` (họ tên không dấu, viết liền), ví dụ `2A202600123_NguyenVanAn.md`. Đổi tên, đừng chép thành file thứ hai.
>
> Xoá mọi dấu TODO và dòng gợi ý (dòng bắt đầu bằng `>`). Mỗi con số lấy từ **bảng A** hoặc **phiếu tự kiểm** trong `submission/`, kèm đơn vị (m, °). Ảnh để trong `report/individual/images/` (nộp LMS trong file zip, không commit); trong báo cáo chỉ ghi **tên file ảnh**. Báo cáo này nằm trên repo public: không chép biển số, chữ trên biển hiệu hay biển chỉ đường, tên đường, địa danh; nhắc tới bạn khác thì ghi MSSV, không ghi họ tên. Cả báo cáo ~2 trang.

## 1. Kết luận trước
- **Mã số:** `2A202603245`
- **Task:** `D13-2A202603245`
- **10 frame của bạn:** `s01f24`, `s01f51`, `s02f13`, `s02f40`, `s03f17`, `s03f42`, `s04f18`, `s04f44`, `s05f14`, `s05f33`
- **Hệ điều hành:** Windows 11 Home
- **Trình duyệt:** Google Chrome
- **Phiên bản CVAT (tên tài khoản → About):** Server `2.81.0`, UI `2.81.0`
- **MSSV bạn ngồi cạnh:** 2A202603101

Tổng cộng đã gán **73 cuboid** trên 10 frame (`56 Car`, `14 Cyclist`, `2 Pedestrian`, `1 Truck`); bốn frame cuối có ít cuboid nhất là `s03f42`, `s04f44`, `s05f14`, `s05f33` (mỗi frame **5 cuboid** do tập trung vào các phương tiện rõ nét trong tầm gần–trung và tránh đoán các cụm quá thưa ở xa). Phiếu `selfcheck` cờ **35/73 cuboid** (chủ yếu do chiều rộng `Car`/`Cyclist` hơi vượt ngưỡng tự kiểm, kèm 2 cờ đáy chìm và 2 cờ điểm sát mép). Mình tự tin nhất ở phần căn hướng đầu xe (`yaw_deg` các xe cùng chiều quanh `265°–278°`) và độ cao đáy đa số chạm mặt đường; phần còn yếu nhất là kiểm soát kích thước bề ngang/dài ở các xe cỡ lớn (> 6,0 m), phân biệt kỹ `Car` với `Truck`/`Bus` ở tầm xa, và căn lại yaw cho một số hộp `Pedestrian`/`Cyclist` hoặc xe cắt ngang còn ở `0,0°`.

- **Đổi góc nhìn:** kéo chuột trái trong khung 3D để xoay (xoay thẳng góc từ trên xuống để quan sát toàn cảnh), kéo chuột phải để dời khung nhìn, lăn con lăn chuột để phóng to/thu nhỏ; nháy đúp vào khoảng trống để đưa về góc nhìn mặc định.
- **Vẽ và chỉnh một cuboid:** chọn công cụ cuboid trên thanh trái → chọn class → bấm **Shape** (không dùng Track), đưa hộp đến cụm điểm và nháy đúp để đặt (`N` vẽ tiếp, `Esc` hủy); chọn hộp rồi dời tâm, chỉnh dài/rộng và xoay hướng ở khung **Top**, chỉnh đáy chạm mặt đường và chiều cao ở **Side** và **Front** (không xoay ở hai khung này).
- **Bật mũi tên hướng và xem ảnh camera:** tích **Appearance → Cuboid orientation** để bật vạch đỏ `+X` hướng về đầu xe; sau khi bấm **Save** (`Ctrl+S`), chạy `python scripts/lab.py preview` để xem các cuboid chiếu lên 7 ảnh camera trong `work/xem/`.

## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ: `s01f24` và `s01f51`. Ảnh: `t1-s01f24-3d.png`, `t1-s01f24-top.png`, `t1-s01f51-3d.png`, `t1-s01f51-top.png`.

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| `s01f24` | TODO(học viên) | Thấp hơn LiDAR khoảng 1,7 m (`z_bottom` các hộp gần quanh −1,50 m đến −1,75 m) | Khoảng 36,31 m (`Car` #10) | `Car`, `Cyclist`, `Pedestrian` | Phía sau (`+y`) có 4 `Car` (#2 ở 6,59 m, #3 ở 12,40 m, #4 ở 19,21 m, #10 ở 36,31 m); bên phải (`−x`) có 3 `Cyclist` (#5–7) và 2 `Pedestrian` (#8–9) | TODO(học viên) |
| `s01f51` | TODO(học viên) | Thấp hơn LiDAR khoảng 1,7 m (`z_bottom` các `Car` quanh −1,65 m đến −1,88 m) | Khoảng 29,28 m (`Car` #7) | `Car`, `Cyclist` | Phía sau (`+y`) có 4 `Car` (#1, #2, #6, #7 ở 6,64–29,28 m); bên phải (`−x`) có 2 `Cyclist` (#8, #9 ở 10,13–11,59 m) | TODO(học viên) |

- 3 điều **chỉ camera** cho biết: TODO(học viên)
- 3 điều **chỉ LiDAR** cho biết: khoảng cách ngang/3D chính xác theo mét tới từng vật (6,26 m tới 36,31 m ở `s01f24`); kích thước hình học 3D thực theo mét (như `Car` #1 dài 4,000 m, rộng 1,900 m, cao 1,500 m); và số điểm + vị trí các vật nằm ngoài góc nhìn `cam01` trong vùng 360° (4 `Car` phía sau ở `s01f24`, 2 `Cyclist` bên phải ở `s01f51`).

Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ / ghi chú từ dữ liệu (`bangA` & `tukiem`) |
|---|---|---|
| `s02f13` | TODO(học viên) | 9 `Car` trong 20,18 m; `#5` có `z_bottom = −2,174 m` (hơi chìm) |
| `s02f40` | TODO(học viên) | Có 2 `Car` ở tầm xa 36,13–37,32 m (`#4`, `#7`) và 2 `Car` góc `0,0°` (`#3`, `#5`) |
| `s03f17` | TODO(học viên) | Có 1 `Truck` gần ở 7,75 m (`#2`, 3354 điểm) và 5 `Cyclist` quanh 10,25–22,89 m |
| `s03f42` | TODO(học viên) | `Car` `#4` rất xa ở 46,74 m còn 45 điểm; `Cyclist` `#5` ở 23,14 m chỉ có 5 điểm |
| `s04f18` | TODO(học viên) | 8 hộp (`7 Car`, `1 Cyclist`) phân bố đều cả trước/sau/trái/phải trong 23,68 m |
| `s04f44` | TODO(học viên) | 5 hộp (`4 Car`, `1 Cyclist`) đều nằm phía trước và bên phải (`−y`, `−x`) |
| `s05f14` | TODO(học viên) | 5 `Car` ở cự ly gần–trung (`5,86–15,30 m`, đều có ≥ 684 điểm) |
| `s05f33` | TODO(học viên) | 4/5 `Car` nằm ở phía sau (`+y`), xa nhất 28,48 m (`#5`, `ground_gap_m = +0,34 m`) |

## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car.png`, `t2-b-bus-truck.png`, `t2-c-ped-cyclist.png`.

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | TODO(học viên) | | | | | |
| (b) xe buýt hoặc xe tải | TODO(học viên) | | | | | |
| (c) người đi bộ hoặc xe hai bánh | TODO(học viên) | | | | | |

TODO(học viên): vòng hiệu chuẩn: cuboid của bạn lệch so với các bạn ở điểm nào, cả lớp chốt cách hiểu guideline nào? Và các vật bạn **bỏ qua vì không đủ cơ sở** (frame, vị trí, mô tả, loại nghi vấn như UNCERTAIN_CLASS / LOW_VISIBILITY), hoặc ghi "không có".

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | TODO(học viên): `s03f17` (sau `Truck` #2 / `Car` #1) hoặc `s01f24` (sau `Car` #1 / #2) / `t4-1-bong-che.png` / task `D13-2A202603245` | Giả thuyết: vật kích thước lớn ở gần chắn hoàn toàn chùm tia LiDAR nên tia không chiếu tới vùng phía sau | Phía sau xe gần (`s03f17#1` ở 3,25 m, `s03f17#2` ở 7,75 m) xuất hiện vùng đen hình quạt mất hẳn điểm, trong khi hai bên ngoài góc che điểm mặt đường vẫn dày | Vùng trống sau vật che là vùng chưa quan sát được (không phải đường trống); vật bị che một phần phải bật `occluded` và bao trọn phần suy luận được |
| 2. Thưa ở xa | TODO(học viên): `s03f42` (`#4 Car`) / `t4-2-thua-o-xa.png` / task `D13-2A202603245` | Giả thuyết: ở cự ly xa (`46,74 m`) góc tách giữa các tia LiDAR mở rộng nên ít tia trúng bề mặt vật | Cụm `Car` ở `46,74 m` chỉ còn `45` điểm rời rạc theo vài đường quét ngang thân, khó thấy rõ mép bánh xe và viền ngoài | Chỉ vẽ nếu thấy khoảng 15–20% thể tích hoặc suy luận được từ camera/Bảng 4.3; nếu thiếu cơ sở thì bỏ qua, ghi `LOW_VISIBILITY` |
| 3. Phản xạ thấp / ít điểm bất thường | TODO(học viên): `s05f14` (`#4 Car`) hoặc `s03f42` (`#5 Cyclist`) / `t4-3-phan-xa-thap.png` / task `D13-2A202603245` | Giả thuyết: bề mặt vật tối màu hấp thụ tia hồng ngoại mạnh, kính xe phản xạ lệch hướng hoặc góc chiếu xiên làm tín hiệu hồi về yếu | `s05f14#4` ở `8,52 m` có intensity rất thấp (`max_I = 1,9`, `1039` điểm) so với `s05f14#1` cùng frame (`6,25 m`, `max_I = 95,5`, `4025` điểm); hoặc `s03f42#5` ở `23,14 m` chỉ còn `5` điểm | Ghi nhận nguyên nhân dưới dạng giả thuyết, không khẳng định chắc; chỉ gán khi có đủ bằng chứng camera, không nới hộp theo quầng nhiễu |
| 4. Điểm lạ | TODO(học viên): `s01f24` (dưới mặt đường ~30 m) / `t4-4-diem-la.png` / task `D13-2A202603245` | Giả thuyết: phản xạ đa đường (multipath) qua bề mặt kính/nhẵn hoặc nhiễu đo của cảm biến khiến tia trả sai khoảng cách | Xoay nghiêng khung 3D ở `s01f24` nhìn xuống phía trước bên trái cách ~30 m (`x ≈ +7,1 m, y ≈ −29,1 m`) thấy cụm `5` điểm nằm sâu dưới mặt đường ở `z ≈ −14,0 m` (thấp hơn mặt đường ~12,3 m) | Tuyệt đối không gán điểm lạ thành vật |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-2A202603245-bangA.csv`; số điểm lấy từ cột `points_in` của `submission/D13-2A202603245-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| `s01f24`, 1, `Car` | −0,996 m | 1,500 m | −1,746 m | 6,26 m | 6,34 m | 267,3° | Chạm đường (`ground_gap_m = +0,07 m`) |
| `s03f17`, 1, `Car` | −0,852 m | 1,716 m | −1,710 m | 3,25 m | 3,36 m | 267,8° | Chạm đường (`ground_gap_m = +0,06 m`) |
| `s03f42`, 4, `Car` | −1,198 m | 1,791 m | −2,093 m | 46,74 m | 46,75 m | 271,0° | Hơi chìm (thấp hơn −1,7 m khoảng 0,39 m; `ground_gap_m = −0,27 m`) |

- **(a) Cuboid gần nhất và xa nhất:**
  - Gần nhất: `s03f17, idx 1` (`Car`), `dist_m = 3,25 m`, `r = 3,36 m`.
  - Xa nhất: `s03f42, idx 4` (`Car`), `dist_m = 46,74 m`, `r = 46,75 m`.
- **(b) So sánh kích thước với Bảng 4.3:**
  - Người đi bộ (`s01f24, idx 9`, `Pedestrian`): `l = 0,744 m`, `w = 0,799 m`, `h = 1,830 m` → nằm trọn trong khoảng chuẩn của Người lớn (`l = 0,4–0,9 m`, `w = 0,5–0,9 m`, `h = 1,50–1,95 m`). Ngoài ra với xe hai bánh (`s01f24, idx 7`, `Cyclist`): `l = 1,943 m`, `w = 0,881 m`, `h = 1,848 m` → chiều dài và rộng khớp Xe máy có người (`1,8–2,3 m` × `0,70–0,95 m`), riêng `h = 1,848 m` vượt nhẹ ngưỡng trên `1,80 m` khoảng `0,048 m` do người lái ngồi cao/đội mũ bảo hiểm và bao trọn điểm trên đỉnh.
  - Xe con (`s01f24, idx 1`, `Car`): `l = 4,000 m`, `w = 1,900 m`, `h = 1,500 m` → nằm trong khoảng Sedan/hatchback (`3,8–5,0 m` × `1,70–1,90 m` × `1,40–1,60 m`). Với một số xe bị cờ bề ngang như `s01f24, idx 2` (`Car`, `l = 4,560 m`, `w = 2,450 m`, `h = 1,457 m`), chiều rộng `w = 2,450 m` vượt khoảng `1,70–2,10 m` do bao cả phần gương hai bên và kéo dư nhẹ mép ngang ở khung Top.
- **(c) Góc `yaw_deg`:** các xe con chạy cùng chiều phía trước (`−y`) đều có `yaw_deg` quanh **`270°`**, ví dụ `s01f24, idx 1` (`267,3°`), `s01f51, idx 3` (`268,6°`), `s04f18, idx 4` (`270,3°`). Trong bảng A hiện tại của các frame, các xe được gán chủ yếu là xe cùng chiều hoặc đứng đỗ dọc trục (`264,7°–278,2°`, trừ 2 xe `s02f40, idx 3` và `idx 5` đang ở `0,0°`), chưa có xe ngược chiều rõ ràng quanh `90°`.

Mật độ theo khoảng cách (4 cuboid `Car` ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| `s01f24`, 1, `Car` | 6,26 m | 2124 |
| `s01f24`, 3, `Car` | 12,40 m | 1363 |
| `s05f33`, 4, `Car` | 23,39 m | 278 |
| `s03f42`, 4, `Car` | 46,74 m | 45 |

- **Quy luật mật độ:** Khi khoảng cách từ LiDAR tới xe tăng gấp đôi ở tầm trung–xa (ví dụ từ `23,39 m` lên `46,74 m`), số điểm trong cuboid giảm mạnh chỉ còn khoảng **1/6** (từ `278` điểm xuống `45` điểm); xét trên toàn dải từ `6,26 m` (`2124` điểm) → `12,40 m` (`1363` điểm) → `23,39 m` (`278` điểm) → `46,74 m` (`45` điểm), số điểm giảm nhanh theo khoảng cách và khớp sát với đường cong trung vị trên slide (`1968` điểm ở `0–10 m`, `718` ở `10–20 m`, `214` ở `20–30 m`, `72` ở `30–40 m`).
- **Tự kiểm & sửa cuboid:** Sau khi đối chiếu `preview` (`work/xem/`) và phiếu `selfcheck`, đã sửa các cuboid trên CVAT gồm: (1) **`s01f24, idx 7` (`Cyclist`)** xoay lại hướng từ `0,0°` (`length < width`) sang `yaw_deg = 74,1°` với `l = 1,943 m`, `w = 0,881 m`; (2) **`s04f44, idx 5` (`Cyclist`)** hạ đáy từ `z_bottom = −1,235 m` (cờ lơ lửng `+0,58 m`) xuống `−1,885 m` (`ground_gap_m = −0,07 m`); ngoài ra còn chỉnh lại nhãn `s01f24, idx 10` từ `Cyclist` sang `Car`, hạ đáy `s03f17, idx 3`, bổ sung `s03f42, idx 5` và tinh chỉnh `s05f33, idx 2` & `idx 5`.
- **Cảnh báo giữ nguyên:** Các cờ bề ngang của xe cỡ lớn/SUV hoặc xe có gương rộng (`width` 2,30–2,74 m ở `Car`, `1,21–1,60 m` ở `Cyclist`) được giữ nguyên khi mép hộp đã ôm sát cụm điểm LiDAR thực tế; cờ chìm nhẹ `−0,27 m` ở `s03f42, idx 4` (`46,74 m`) giữ nguyên do ở cự ly rất xa điểm mặt đường thưa; 2 cờ điểm sát mép (`s01f24, idx 9` và `s03f42, idx 5`) giữ nguyên để tránh nới hộp lấn sang điểm nền/vật bên cạnh.

TODO(học viên): đổi kiểm: MSSV người đã kiểm chéo với bạn (`2A202603101`), hai con số nào được đối chiếu với bảng A, khớp hay lệch (lệch thì đã sửa gì).

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
- **(a) Ý nghĩa từ phía model học trên nhãn này:**
  - Nhãn cuboid 3D cần đo bằng **mét** trong hệ tọa độ thực thay vì pixel trên ảnh 2D vì mô hình nhận thức LiDAR cần dự đoán chính xác vị trí `(x, y, z)`, khoảng cách vật lý và kích thước thực (dài, rộng, cao) bất biến theo góc nhìn để hệ thống xe tự hành ước lượng quỹ đạo và tránh va chạm an toàn.
  - Vật thưa điểm cần quy tắc riêng (chỉ gán khi thấy khoảng 15–20% thể tích hoặc có đủ cơ sở từ camera/hình dạng; nếu không thì bỏ qua/ghi `LOW_VISIBILITY`) vì cụm chỉ có vài điểm rời rạc không đủ cơ sở suy luận kích thước và hướng thật — nếu đoán bừa sẽ tạo nhãn nhiễu khiến model học sai hướng hoặc sinh dự đoán ảo.
- **(b) Dùng AI:**
  - **Công cụ:** Antigravity (Gemini).
  - **Câu hỏi chính:** Giải thích hệ trục tọa độ VF (`+x` trái, `−y` trước, `+z` lên), quy trình các checkpoint, các lệnh `lab.py`/`check_submission.py`, đối chiếu công thức tính toán (`z_bottom`, `r`), kiểm tra lỗi và phân tích cảnh báo từ `D13-2A202603245-bangA.csv` và `D13-2A202603245-tukiem.csv`.
  - **Cách dùng kết quả:** Dùng danh sách cảnh báo để mở CVAT 3D và `work/xem/` tự kiểm tra và sửa lại các cuboid sai (`s01f24#7`, `s04f44#5`, `s03f42#5`…), đồng thời kiểm lại toàn bộ con số trong báo cáo khớp với CSV đã xuất.
- **(c) Điều còn chưa chắc:**
  - `s01f24, idx 10` ở khoảng cách `36,31 m` có kích thước hộp `6,300 m × 2,980 m × 2,552 m` và `ground_gap_m = −0,32 m`: chưa chắc hoàn toàn đây là xe con lớn bị bao dư điểm ở xa hay thuộc `Truck`/`Bus` (`UNCERTAIN_CLASS`, `LOW_VISIBILITY`).
  - Các xe `Car` ở tầm trung–xa có chiều dài quanh `6,01–6,54 m` hoặc chiều rộng `> 2,5 m` (như `s01f51#5`, `s02f40#4`, `s03f17#4`, `s04f18#6`, `s04f44#3`) và hai xe `s02f40#3`, `s02f40#5` có góc `yaw_deg = 0,0°`: cần rà soát kỹ thêm về ranh giới `Car` vs `Truck` và hướng di chuyển cắt ngang nếu có thêm thời gian trước khi chốt bài cuối.
