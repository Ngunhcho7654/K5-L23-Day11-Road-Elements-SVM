# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Lê Tuấn Khôi (`2A202603024`, `khoi`)        Người kiểm (học viên): Hà Khánh (`2A202603221`, `hakhanh`)  
Ngày: 2026-11-21                              Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `khoi-front.zip` (`sha256: de411067e560…`, 12 ảnh A01–A12), `khoi-fisheye.zip` (`sha256: d370bfebe318…`, 8 ảnh B01–B08); ảnh thêm nhận kèm riêng: `khoi-front-extra.zip` (`sha256: f5948326cba0…`, A13–A16), `khoi-fisheye-extra.zip` (`sha256: eeb1d225db24…`, B09–B12) — *chưa kèm file `khoi-manifest.json` nên chưa có số `revision`*.  
Số ảnh kiểm: 6 (`A04`, `A06`, `A08`, `A10`, `B04`, `B08`) (+ 2 ảnh thêm, ghi riêng: `A14`, `B11`)   Số nhãn đã kiểm (shape + tag): 86 (62 shape trong file + 24 vị trí tag kiểm trên 6 ảnh, trong đó 20 tag có mặt và 4 tag bị thiếu ở `A08`)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 4 | 1 nặng, 3 nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 7 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 18 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 18 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 18 | 4 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 18 | 3 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 27 | 4 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 13 | 5 | 1 nặng, 4 chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 17 | 4 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 13 | 5 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 11 | 0 | chính |
| QC1-12 file | lỗi file | 86 | 1 | nhẹ |

*Ghi chú số mục kiểm trên 6 ảnh cốt lõi (`A04, A06, A08, A10, B04, B08`): `QC1-01` = 4 tag × 6 ảnh = 24; `QC1-02` = 7 vạch L1/R1 thấy được (`A04`: L1/R1, `A06`: L1 [R1 miễn], `A08`: R1 [L1 ghi Ca mơ hồ], `A10`: L1/R1, `B04`: L1, `B08`: camera hai bên không dùng L1/R1); `QC1-03..06` = 18 polyline `lane`; `QC1-07` = 27 hình (`drivable` 13 + `crosswalk` 4 + `road_curb` 10); `QC1-08` = 13 (9 hộp `traffic_light` đã gán + 4 cụm đèn rõ ≥ 8 px bị bỏ sót); `QC1-09` = 17 (9 `traffic_light` + 8 `traffic_sign` đã gán); `QC1-10` = 13 (8 hộp `traffic_sign` đã gán + 5 tấm biển rõ ≥ 8 px bị bỏ sót); `QC1-11` = 11 shape trên 2 ảnh fisheye (`B04`: 7 + `B08`: 4); `QC1-12` = 86 nhãn đã kiểm và 4 file zip bàn giao.*

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | `A08_c0deebc1-16cfa791.jpg` | `tag:camera` | nặng | Thiếu hoàn toàn `tag:camera` (đúng là `front`; ảnh A08 không có tag nào). |
| 2 | QC1-01 | `A08_c0deebc1-16cfa791.jpg` | `tag:timeofday` | nhẹ | Thiếu `tag:timeofday` (đúng là `day`). |
| 3 | QC1-01 | `A08_c0deebc1-16cfa791.jpg` | `tag:weather` | nhẹ | Thiếu `tag:weather` (đúng là `overcast`). |
| 4 | QC1-01 | `A08_c0deebc1-16cfa791.jpg` | `tag:source` | nhẹ | Thiếu `tag:source` (đúng là `real`). |
| 5 | QC1-03 | `A04_b7a8e795-0ff55db2.jpg` | `lane#9@(64,552)` | nặng | Gán nhầm `position = R1` cho nét vàng bên trái làn xe đang đi (ảnh thành hai vạch `R1`: một ở bên trái và `lane#0@(718,535)` ở bên phải; vạch này nằm ở vị trí `L1`). |
| 6 | QC1-04 | `A10_b6ff1331-f6d3fba8.jpg` | `lane#3@(1183,659)` | chính | Vạch `R1` chỉ vẽ bằng 2 điểm và dừng sớm tại `(951,511)` trước giọt nước/xe bên phải, bỏ qua đoạn vạch trắng đứt còn thấy tiếp phía trước và không nối qua đoạn che ngắn kèm `occluded`. |
| 7 | QC1-05 | `A04_b7a8e795-0ff55db2.jpg` | `lane#8@(24,553)` + `lane#9@(64,552)` | chính | Vạch vàng đôi tim đường bị tách thành 2 polyline riêng lẻ (`kind = single`) thay vì gộp thành 1 polyline duy nhất `kind = double`. |
| 8 | QC1-05 | `A06_b8c66e31-37045eec.jpg` | `lane#5@(449,417)` + `lane#6@(441,416)` | chính | Vạch vàng đôi `L1` bị tách thành 2 polyline cùng `position = L1` (`road_check lint` cũng báo `QC1-05`). |
| 9 | QC1-05 | `A08_c0deebc1-16cfa791.jpg` | `lane#6@(761,445)` + `lane#7@(655,321)` | chính | Vạch `R1` (trắng đứt bên phải làn xe) bị tách thành 2 polyline liên tiếp cùng `position = R1`, mỗi đoạn chỉ 2 điểm (`road_check lint` cũng báo `QC1-05`). |
| 10 | QC1-05 | `A08_c0deebc1-16cfa791.jpg` | `lane#9@(46,358)` + `lane#10@(413,295)` | chính | Vạch `L2` bị tách thành 2 polyline liên tiếp cùng `position = L2` (`road_check lint` cũng báo `QC1-05`). |
| 11 | QC1-06 | `A04_b7a8e795-0ff55db2.jpg` | `lane#8@(24,553)` | chính | Sai thuộc tính vạch vàng đôi tim đường: gán `color = white`, `kind = single` (đúng là `color = yellow`, `kind = double`). |
| 12 | QC1-06 | `A06_b8c66e31-37045eec.jpg` | `lane#5@(449,417)` | chính | Sai thuộc tính vạch vàng đôi tim đường: gán `style = dashed`, `color = white` (đúng là `style = solid`, `color = yellow`). |
| 13 | QC1-06 | `A06_b8c66e31-37045eec.jpg` | `lane#6@(441,416)` | chính | Sai màu vạch vàng đôi tim đường: gán `color = white` (đúng là `color = yellow`). |
| 14 | QC1-07 | `A08_c0deebc1-16cfa791.jpg` | `drivable#19@(817,498)` | chính | Làn cùng chiều bên phải làn xe đang đi nhưng gán `area_type = direct` (đúng là `alternative`). |
| 15 | QC1-07 | `A08_c0deebc1-16cfa791.jpg` | `drivable#20@(1280,479)` | chính | Làn cùng chiều ngoài cùng bên phải nhưng gán `area_type = direct` (đúng là `alternative`). |
| 16 | QC1-07 | `A10_b6ff1331-f6d3fba8.jpg` | `drivable#5@(451,603)` | chính | Vùng `drivable` (`direct`) dừng cắt ngang ngay sau đuôi xe Subaru phía trước (vi phạm quy tắc không khoét lỗ / dừng trước xe khác). |
| 17 | QC1-07 | `A10_b6ff1331-f6d3fba8.jpg` | `drivable#0@(2,511)` | chính | Gán `area_type = direct` cho dải đỗ xe sát lề trái (có xe đỗ bên trong), vi phạm quy tắc không đưa dải đỗ xe sát lề vào `direct`. |
| 18 | QC1-08 | `A06_b8c66e31-37045eec.jpg` | `traffic_light#0@(935,292)` | nặng | Đèn hướng về xe (`facing = front`, `type = vehicle`) thực tế đang sáng **xanh (`green`)** ở bóng dưới cùng nhưng gán sai `color = red`. |
| 19 | QC1-08 | `A06_b8c66e31-37045eec.jpg` | `traffic_light` (bỏ sót, dầm cầu trái `~(298,128)`) | chính | Bỏ sót cụm đèn giao thông chính hướng về xe đang sáng xanh treo dưới dầm cầu vượt bên trái (cao ~29 px ≥ 8 px). |
| 20 | QC1-08 | `A06_b8c66e31-37045eec.jpg` | `traffic_light` (bỏ sót, dầm cầu giữa `~(516,148)`) | chính | Bỏ sót cụm đèn giao thông chính hướng về xe đang sáng xanh treo dưới dầm cầu vượt chính giữa (cao ~30 px ≥ 8 px). |
| 21 | QC1-08 | `A10_b6ff1331-f6d3fba8.jpg` | `traffic_light` (bỏ sót, giao lộ `~(743,175)`) | chính | Bỏ sót cụm đèn giao thông đang sáng đỏ phía trước bên phải xe cứu thương (cao ~30 px ≥ 8 px). |
| 22 | QC1-08 | `B04_05535_RV.png` | `traffic_light` (bỏ sót, cột phải `~(1067,239)`) | chính | Bỏ sót cụm đèn mũi tên đỏ trên cột bên phải ngay dưới biển cấm `No Entry` (cao ~32 px ≥ 8 px, `edge_zone = true`). |
| 23 | QC1-09 | `A06_b8c66e31-37045eec.jpg` | `traffic_sign#4@(660,212)` | chính | Biển `ONE WAY` (hiệu lệnh hướng đi) gán sai `group = information` (đúng theo bảng biển Mỹ Road v1.0 là `mandatory`). |
| 24 | QC1-09 | `A06_b8c66e31-37045eec.jpg` | `traffic_sign#2@(563,304)` | chính | Biển công trường hình thoi màu cam gán `group = other` (đúng theo bảng biển Mỹ Road v1.0 là `warning`). |
| 25 | QC1-09 | `A08_c0deebc1-16cfa791.jpg` | `traffic_light#17@(295,138)` | chính | Cụm đèn quay ngang sang chiều vuông góc (giống `traffic_light#15@(205,101)`) nhưng gán sai `facing = front` (đúng là `side`). |
| 26 | QC1-09 | `B04_05535_RV.png` | `traffic_sign#1@(1062,164)` | chính | Biển cấm đi ngược chiều (`No Entry`, hình tròn đỏ gạch ngang trắng) gán sai `group = warning` (đúng là `prohibitory`). |
| 27 | QC1-10 | `A08_c0deebc1-16cfa791.jpg` | `traffic_sign` (bỏ sót, `~(777,36)`) | chính | Bỏ sót biển phụ `PASSENGER CARS ONLY` gắn ngay phía trên biển `Harlem River Dr / RFK Br` (cao ~29 px; cần hộp riêng `group = supplementary`). |
| 28 | QC1-10 | `A10_b6ff1331-f6d3fba8.jpg` | `traffic_sign` (bỏ sót, cột trái `~(47,47)`) | chính | Bỏ sót biển cấm `NO PARKING ANYTIME` trên cùng ở cột bên trái (cao ~48 px, `group = prohibitory`). |
| 29 | QC1-10 | `A10_b6ff1331-f6d3fba8.jpg` | `traffic_sign` (bỏ sót, cột trái `~(49,91)`) | chính | Bỏ sót biển cấm `NO STANDING ANY TIME` (nền đỏ) ở vị trí thứ 2 trên cột trái (cao ~43 px, `group = prohibitory`). |
| 30 | QC1-10 | `A10_b6ff1331-f6d3fba8.jpg` | `traffic_sign` (bỏ sót, cột trái `~(50,132)`) | chính | Bỏ sót biển phụ `ACS` ngay dưới biển `NO STANDING` trên cột trái (cao ~14 px; cần hộp riêng `group = supplementary`). |
| 31 | QC1-10 | `A10_b6ff1331-f6d3fba8.jpg` | `traffic_sign` (bỏ sót, cột trái `~(51,144)`) | chính | Bỏ sót biển cấm đỗ hình chữ `P` gạch chéo dưới cùng trên cột trái (cao ~34 px, `group = prohibitory`). |
| 32 | QC1-12 | Toàn lô (4 file zip) | `khoi-front.zip`, `khoi-front-extra.zip`, `khoi-fisheye.zip`, `khoi-fisheye-extra.zip` | nhẹ | Cả 4 file đều mở được chuẩn `CVAT for images 1.1`, `contains_images = false`, không có label/thuộc tính lạ; nhưng đang nộp tách 4 file zip thay vì gộp 2 file (`khoi-front.zip` A01–A16, `khoi-fisheye.zip` B01–B12) và chưa kèm `khoi-manifest.json` theo đặc tả bàn giao Road v1.0. |

**Ảnh được ghi "không lỗi" trong 6 ảnh cốt lõi:**
- `B08_05783_MVR.png` (`khoi-fisheye.zip`, 4 shape + 4 tag = 8 nhãn): **không ghi nhận lỗi**. Đủ 4 tag chính xác (`camera = fisheye_right`, `timeofday = day`, `weather = clear`, `source = real`); `lane#0@(216,623)` dùng đúng `position = other` (quy tắc camera hai bên), đúng `dashed / white / single` và bám tâm vạch; `crosswalk#1@(450,686)` bao trọn vùng ngựa vạn và dừng sát thân xe; `road_curb#3@(393,175)` đi theo cung mép vỉa hè (13 điểm); `drivable#2@(1009,140)` (`direct`) không tràn vỉa hè và không gán vào thân xe hay vùng tối viền ảnh.

**Ghi chú riêng 2 ảnh thêm đã xem thêm (không tính vào mẫu số 6 ảnh cốt lõi ở trên):**
- `A14_ca04d99f-c1282bb7.jpg` (`khoi-front-extra.zip`): vạch vàng đôi `L1` bị tách làm 2 polyline (`lane#2`, `lane#3`) và gán sai `color = white` (`QC1-05`, `QC1-06`); `drivable#6@(474,472)` (`direct`) khoét lỗ hình chữ nhật quanh xe taxi vàng (`QC1-07`); bỏ sót 2 cụm đèn xanh treo phía trước và biển `ONE WAY` (`QC1-08`, `QC1-10`). Bên phải không có vạch `R1` thấy được nên miễn `QC1-02`.
- `B11_07282_RV.png` (`khoi-fisheye-extra.zip`): làm tốt quy tắc bỏ qua vạch ô đỗ người khuyết tật (không gán `lane`, tránh được bẫy `QC1-03`) và không gán thân xe; chỉ sai thuộc tính `drivable#0@(922,591)` đang để `area_type = alternative` thay vì `direct` (`QC1-07`).

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| `A06_b8c66e31-37045eec.jpg` | Bên phải làn xe đi không có vạch sơn kẻ làn `R1` (chỉ có dãy trụ cầu vượt và mép vỉa hè); xác nhận miễn cảnh báo `QC1-02` cho `R1` trên `A06` (tương tự `A05`, `A09`, `A14`)? | |
| `A08_c0deebc1-16cfa791.jpg` | Vệt dọc mờ bên trái làn xe (`lane#8@(256,424)`) nhìn giống khe nhựa đường hơn là vạch sơn kẻ làn; nên tính là lỗi thừa `QC1-03` (nặng) hay chấp nhận giữ là `L1`? *(Phiếu tạm chưa tính lỗi nặng cho vạch này để chờ lead chốt.)* | |
| `A06_b8c66e31-37045eec.jpg` / toàn lô | Ảnh trời nhiều mây sáng nhưng đường khô: ranh giới giữa `weather = clear` và `overcast` khi chấm có chấp nhận cả hai nếu hợp lý không? | |

## Quyết định
Lỗi nặng: 3   Lỗi chính: 25 / 86 nhãn = 29,1 %   Lỗi nhẹ: 4   Ca chờ lead: 0 (ảnh hưởng tới kết luận; có 3 câu hỏi chờ lead thống nhất cho lần sửa)  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô có **3 lỗi nặng** (`QC1-01` thiếu `tag:camera` ở `A08`, `QC1-03` gán nhầm `position = R1` cho nét vàng bên trái ở `A04`, `QC1-08` đèn sáng xanh nhưng gán `color = red` trên đèn `facing = front` ở `A06`) **và** tỉ lệ lỗi chính là **25 / 86 = 29,1 %** (> ngưỡng 5 %). Theo thang mức lỗi Road v1.0, chỉ cần ≥ 1 lỗi nặng hoặc lỗi chính > 5 % đã đủ trả về **Rework**. Khi sửa lại (`revision 2`), đề nghị bạn rà thêm các ảnh ngoài mẫu 6 ảnh (lưu ý `road_check lint` cũng báo thiếu toàn bộ 4 tag ở `A12` và tách polyline `L1`/`L2` ở `A09`, `A11`, `A12`, `A14`), gộp về 2 file `khoi-front.zip` và `khoi-fisheye.zip`, và tạo `khoi-manifest.json` bằng `road_check lint --manifest`.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
