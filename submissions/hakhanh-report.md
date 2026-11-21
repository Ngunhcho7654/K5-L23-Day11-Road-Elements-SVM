# Báo cáo cá nhân — Ngày 11
Họ tên: Hà Khánh              Mã học viên: 2A202603221  
Phiên bản CVAT (Help → About): [Cần bạn điền — xem Help → About trên CVAT lớp]  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-20 12:21:28 – 12:22:12 UTC (19:21–19:22 giờ VN, ghi trong `<dumped>` của 4 file export gốc); tạo manifest gộp `hakhanh-manifest.json` lúc `2026-11-21T02:08:12+00:00` (09:08 giờ VN)    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | Đã nạp từ `configs/road_v1_labels.json`: `lane`, `road_curb` (`polyline`); `crosswalk`, `drivable` (`polygon`); `traffic_light`, `traffic_sign` (`rectangle`). Kiểm bằng `road_check lint`: 0 lỗi `QC1-12`. |
| Thuộc tính và giá trị | Đúng | Đủ các thuộc tính `select` và `checkbox` (`edge_zone`) đúng tên và danh sách giá trị của Road v1.0; luôn mở **Details** sửa lại vì CVAT tự điền giá trị đầu danh sách (`L1 / solid / white / single`, `direct`, `clear`, `red`, `prohibitory`). |
| 4 tag ảnh | Đúng | Đủ 4 label kiểu `tag` (`camera`, `timeofday`, `weather`, `source`), mỗi tag có thuộc tính `value`; `hakhanh-manifest.json` xác nhận `images_all_tags`: 16/16 ảnh front và 12/12 ảnh fisheye. |
Cách kết thúc polyline trên bản CVAT này: Bấm phím **`N`** (hoặc bấm nút **Done / Finish** trên thanh công cụ vẽ).  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ **Tag** ở thanh bên trái, gắn lần lượt `camera` trước tiên rồi `timeofday`, `weather`, `source`; sau đó mở **Details** của từng tag trong bảng **Objects** để chọn đúng giá trị `value`.  

## 2. Số lượng đã gán
*(Đếm trực tiếp từ hai file bàn giao `submissions/hakhanh-front.zip` và `submissions/hakhanh-fisheye.zip`, khớp với `shapes_by_label` trong `submissions/hakhanh-manifest.json`.)*

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 30 | 9 | 4 | 25 | 43 | 48 |
| front-extra (đã làm 4 / 4) | 4 | 11 | 2 | 2 | 9 | 17 | 17 |
| fisheye | 8 | 8 | 13 | 7 | 10 | 10 | 8 |
| fisheye-extra (đã làm 4 / 4) | 4 | 1 | 4 | 4 | 4 | 2 | 1 |

*(Tổng cộng 28 ảnh: 289 shape + 112 tag = 401 nhãn; `hakhanh-front.zip`: 16 ảnh, 217 shape, 64 tag; `hakhanh-fisheye.zip`: 12 ảnh, 72 shape, 48 tag.)*

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| `A05_b2576c8c-2de20b8a.jpg` | `lane` (`L1`, `R1`) | Tự ước lượng vẽ `L1`/`R1` dọc mép đường hay không vẽ `lane` và chỉ vẽ `road_curb` | Không vẽ `L1`/`R1`; chỉ gán `road_curb` và `drivable` (`direct`, chừa dải xe đỗ hai bên) | Đường dân cư không có vạch sơn kẻ làn; theo Road v1.0 và `CHECKPOINTS.md`, không tự vẽ vạch không có trên ảnh, ghi nhận ca miễn cảnh báo `QC1-02` của `lint`. |
| `A09_c7e6d5d1-c8af9fe3.jpg` | `lane`, `drivable` | Gán `L1` cho vạch vàng đôi tim đường hay cho vạch trắng đứt ngay sát bên trái làn xe đang đi | Chọn `L1` là vạch trắng đứt sát trái xe, `L2` là vạch vàng đôi tim đường, miễn `R1` (bên phải là vỉa hè `road_curb`); `drivable` (`direct`) ở làn phải, `alternative` ở làn trái | Xe ego đang chạy ở làn sát phải (đường có 2 làn cùng chiều); theo Road v1.0, `position` luôn đếm từ làn xe đang đi ra hai bên nên vạch gần xe nhất bên trái là `L1`. |
| `A10_b6ff1331-f6d3fba8.jpg` | `lane` (`R1`), `traffic_sign` | (1) Dừng `R1` trước vùng bị giọt nước/xe bên phải che hay nối liền; (2) gộp hay tách tấm `ACS` dưới biển `NO STANDING` | (1) Nối liền `R1` qua đoạn che ngắn và bật `occluded = true`; (2) tách riêng 4 hộp biển trên cột trái, tấm `ACS` gán `group = supplementary` | Giọt nước và xe chỉ che một đoạn ngắn của `R1` trong khi phần vạch phía trước vẫn thấy; tấm `ACS` là biển phụ bổ nghĩa cho biển chính ngay trên nên phải tách hộp riêng theo mục 3 Road v1.0. |
| `B04_05535_RV.png` | `traffic_sign`, `traffic_light` | Biển tròn đỏ gạch ngang trắng (`No Entry`) thuộc `prohibitory` hay `warning`; biển và đèn mũi tên đỏ sát viền phải có cần bật `edge_zone` không | Gán `traffic_sign` `group = prohibitory`, `traffic_light` `color = red`, `facing = front`, và bật `edge_zone = true` cho cả hai | Biển `No Entry` có chức năng cấm đi vào (`prohibitory`), và tâm hộp của cả biển lẫn cụm đèn đều nằm ngoài vòng 80 % bán kính ảnh fisheye nên bắt buộc bật `edge_zone`. |
| `B11_07282_RV.png` | `lane`, `drivable` | Vạch kẻ ô đỗ xe người khuyết tật màu trắng/xanh có gán `lane` và đưa vào `drivable` không | Không gán `lane` cho vạch ô đỗ; `drivable` (`direct`) chỉ phủ mặt lối đi phía trước ô đỗ và dừng sát trên mép cản sau thân xe ego | Theo mục 4 Road v1.0, vạch ô đỗ không được gán `lane` (bẫy `QC1-03`), và không gán thân xe ego hay ô đỗ xe chuyên dụng vào vùng làn đi `direct`. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: [Chưa nhận phiếu — cần bạn điền sau khi nhận Phiếu QC 1 từ bạn kiểm]  Quyết định nhận được: [Chưa nhận — cần bạn điền]  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| [Điền sau khi nhận phiếu QC 1] | | | |

*Ghi chú minh bạch (không bịa số liệu): Hiện tại lô của tôi đang ở `revision: 1` và chưa nhận lại Phiếu QC 1 từ bạn kiểm chéo. Trước khi bàn giao `revision: 1`, tôi đã tự rà soát (Self-QC) bằng `road_check lint` và xem lại toàn bộ 28 ảnh overlay, qua đó tự phát hiện và sửa trước 6 nhóm lỗi nội bộ: (1) khôi phục ảnh `B05_05780_MVL.png` bị thiếu và các shape trọng tâm ở `B09/B10/B12`; (2) căn lại `L1`/`L2` ở `A09` khớp với làn phải (`QC1-03`); (3) xóa tag trùng và đổi `drivable` về `direct` kèm `road_curb` ở `B06`; (4) sửa màu vạch vàng đôi `L1` ở `A14` (`QC1-06`); (5) gỡ lỗi khoét lỗ `drivable` quanh xe phía trước ở `A10`, `A13`, `A14`, bổ sung `alternative` ở `A16` và sửa polygon tự cắt ở `B11` (`QC1-07`); (6) kiểm lại 7 cảnh báo `QC1-02` trên `hakhanh-manifest.json` (`A05` L1/R1, `A06` R1, `A07` L1, `A08` L1, `A09` R1, `A14` R1) đều là ca không có vạch sơn thấy được. Sau khi nhận Phiếu QC 1 từ bạn kiểm, bảng mục 4 này sẽ được cập nhật đầy đủ và nộp `revision: 2` nếu cần Rework.*

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `hakhanh-front.zip` (gộp `front` A01–A12 + `front-extra` A13–A16; 16 ảnh, `contains_images = false`) | Có (`road_check lint` PASS, `sha256: 07ef04ca2637…`) | `A01`: 9 / 9 | `A02`: 6 / 6 | Có (16/16 ảnh có `<tag label="camera">`, giá trị `front`) |
| `hakhanh-fisheye.zip` (gộp `fisheye` B01–B08 + `fisheye-extra` B09–B12; 12 ảnh, `contains_images = false`) | Có (`road_check lint` PASS, `sha256: b3eb41c26012…`) | `B01`: 5 / 5 | `B02`: 11 / 11 | Có (12/12 ảnh có `<tag label="camera">`, đúng hậu tố FV/RV/MVL/MVR) |

*(Số shape phía "job" đối chiếu từ bản export gốc trực tiếp từ CVAT trong `submissions/raw/hakhanh-front.zip` và `submissions/raw/hakhanh-fisheye.zip`; bạn nên đối chiếu thêm một lần trên giao diện CVAT khi chụp ảnh Mục 6.)*

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `[Cần bạn chụp và chèn ảnh màn hình tab Labels của project d11-road-hakhanh trên CVAT]`
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): `[Cần bạn chụp và chèn ảnh màn hình một ảnh front, ví dụ A08 hoặc A10 trên CVAT]`
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: `[Cần bạn chụp và chèn ảnh màn hình một ảnh fisheye phóng to polyline cong, ví dụ B03 hoặc B04 trên CVAT]`
4. Một đoạn XML có `<polyline label="lane">` *(trích nguyên văn từ `annotations.xml` trong `submissions/hakhanh-front.zip`, ảnh `A01_bc5fadac-fa6dd225.jpg`, vạch `R1`)*:

```xml
<polyline label="lane" source="file" occluded="0" points="666.00,695.00;620.00,656.00;550.00,599.00;484.00,549.00;435.00,514.00;412.00,499.00" z_order="2">
  <attribute name="position">R1</attribute>
  <attribute name="style">dashed</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Qua quá trình tự kiểm (Self-QC) toàn bộ 28 ảnh trước khi chốt `revision: 1`, hai nhóm lỗi tôi dễ mắc nhất là **`QC1-07`** (khoét lỗ vùng `drivable` quanh xe chạy phía trước ở `A10`, `A13`, `A14`, bỏ sót `alternative` ở `A16`, vẽ polygon tự cắt sát mép cản sau ở `B11`) và **`QC1-03` / `QC1-06`** (nhầm `L1`/`L2` khi xe đi ở làn phải trên `A09`, hoặc quên đổi thuộc tính mặc định `color = white` sang `yellow` trên vạch vàng đôi ở `A14`). Để tránh ở Ngày 20 (Road v1.x có thêm ca mưa, đêm và ô đỗ): (1) ngay khi vẽ xong mỗi `lane` hoặc `drivable`, mở **Details** kiểm tra thuộc tính trước khi chuyển sang hình tiếp theo; (2) khi vẽ `drivable`, luôn hình dung "đường trống không có xe khác" trước rồi mới cắt biên theo lề/capô/thân xe; (3) trước khi nhấn **Finish the job**, luôn chạy `road_check lint` và xem lại toàn bộ ảnh overlay để bắt lỗi hình học/thuộc tính mắt thường dễ bỏ sót.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Các nhãn Road v1.0 là ground truth trực tiếp cho các bài toán nhận thức đường của hệ thống ADAS/xe tự hành: `lane` (polyline) đi vào mô hình **phát hiện làn đường (lane detection — dạng row-anchor / curve fitting)** phục vụ giữ làn (LKA); `drivable`, `crosswalk` đi vào mô hình **phân vùng ngữ nghĩa (semantic segmentation)** mặt đường đi được; `traffic_light` và `traffic_sign` đi vào mô hình **phát hiện đối tượng (object detection + classification)**; còn 4 tag ảnh dùng để phân tầng tập train/val/test theo điều kiện vận hành (ODD).  
Chọn một lỗi đã sửa: **lỗi `QC1-07` khoét lỗ `drivable` quanh xe chạy phía trước** (đã gặp và sửa ở `A10`, `A13`, `A14`). Nếu giữ nhãn khoét lỗ này đưa vào huấn luyện mô hình phân vùng mặt đường (`drivable area segmentation`), mô hình sẽ học sai rằng phần mặt đường ngay dưới và phía sau xe khác thuộc lớp "không lái được" thay vì tách biệt bài toán hình học mặt đường (`drivable`) với bài toán phát hiện vật cản động (xe/người). Khi chạy thực tế trong giao thông đông, bản đồ vùng lái sẽ bị đứt đoạn hoặc biến dạng liên tục mỗi khi có xe phía trước, làm bộ lập kế hoạch đường đi (path planning) phanh gấp hoặc đổi quỹ đạo bất thường. *(Tương tự, lỗi `QC1-03` gán nhầm `L1`/`L2` ở `A09` nếu không sửa sẽ làm mô hình LKA ước lượng lệch tâm làn sang làn kế bên.)*

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
*(Chạy trực tiếp bằng `python -m road_lab.rowanchor` trên ảnh `A01_bc5fadac-fa6dd225.jpg`, vạch `position = R1`: bản của tôi là `lane#4@(666,695)` trong `hakhanh-front.zip`; bản của bạn Khôi là `lane#8@(707,720)` trong `khoi-front.zip`.)*

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | không có làn | 648.3 | 600.4 | 551.2 | 498.5 |
| x của bạn kia | 706.8 | 659.6 | 603.0 | 543.4 | 484.6 |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?  
   Nếu dừng polyline sớm hơn 40 px ở đầu xa (vượt qua mốc `y = 560` xuống dưới, tức điểm cuối có `y > 560`), hàng trên cùng nằm ngoài phạm vi polyline là **`y = 560`** sẽ đổi thành `"không có làn"` (vì đoạn thẳng không còn cắt ngang hàng neo đó nữa). Tương tự ở đầu gần xe, bản của tôi bắt đầu tại `y = 695` (ngắn hơn đáy ảnh 25 px) nên hàng **`y = 720`** đã thành `"không có làn"`; nếu thụt lên thêm 40 px (từ `y = 695` lên `y = 655`), hàng **`y = 680`** cũng sẽ mất và chuyển thành `"không có làn"`.
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?  
   - Ở hàng **`y = 720`**: bản của tôi là `"không có làn"` (vì điểm đầu đặt tại `y = 695`), còn bạn Khôi kéo tới đáy `y = 720` cho `x = 706.8` (khác biệt do điểm bắt đầu; nếu so ở hàng gần nhất có chung giá trị là `y = 680`, hai bên lệch `|648.3 − 659.6| = 11.3 px`).
   - Ở hàng **`y = 560`**: hai bên lệch `|498.5 − 484.6| = 13.9 px`.
   - **Ảnh hưởng LKA (slide 25):** Sai lệch ở **hàng gần xe (`y = 720`, hoặc `y = 680`) ảnh hưởng LKA nhiều hơn** tới quyết định giữ làn tức thời, vì đây là vị trí vạch ngay sát mũi xe dùng để tính độ lệch ngang (lateral offset) cho bộ điều khiển đánh lái; đúng với quy tắc trong Road v1.0 (*"Điểm đầu sát xe là điểm quan trọng nhất, đặt thật chính xác"*).
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?  
   - **Cách tính nội suy `x` theo hàng `y` không đổi** trên một vạch đơn điệu: hàm `x_at_y` trong `src/road_lab/geometry.py` duyệt từng đoạn `(a, b)` với `lo, hi = min(y1, y2), max(y1, y2)` nên cho ra đúng cùng một tập tọa độ `x` bất kể thứ tự điểm ngược hay xuôi.
   - **Script gặp khó:** `road_check.py` (cả `lint` lẫn `check`) sẽ bắt lỗi ngay — `lint` cảnh báo ngược chiều `QC1-04` khi `first[1] < last[1]`, còn `check` đánh lỗi chính `QC1-04` (*"vẽ ngược chiều (phải từ gần xe ra xa)"*) khi `s1 < s0` và không đo đúng điểm đầu gần xe / điểm dừng xa (`d_near`, `d_far`); ngoài ra `rowanchor.py` cũng in cảnh báo `"Chú ý: polyline đầu tiên vẽ từ xa về gần"`, và mọi pipeline huấn luyện/hậu xử lý giả định `points[0]` là điểm gần xe sẽ đọc ngược hướng làn.
