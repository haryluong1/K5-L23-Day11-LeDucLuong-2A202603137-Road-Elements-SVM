# Báo cáo cá nhân — Ngày 11
Họ tên: Lê Đức Lương               Mã học viên: 2A202603137  
Phiên bản CVAT (Help → About): CVAT v2.82.0  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-24 12:12     Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane (polyline), road_curb (polyline), crosswalk (polygon), drivable (polygon), traffic_light (rectangle), traffic_sign (rectangle) |
| Thuộc tính và giá trị | Đúng | Khớp hoàn toàn với configs/road_v1_labels.json từ src/road_lab/taxonomy.py |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source (mỗi tag có thuộc tính select tên 'value') |
Cách kết thúc polyline trên bản CVAT này: Nhấn phím N (hoặc click chuột đúp vào điểm cuối)  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ Tag ở thanh bên trái, chọn label tag, mở tab Details để chọn giá trị 'value' tương ứng  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 16 | 2 | 22 | 17 | 2 |
| front-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 5 | 11 | 7 | 10 | 2 | 1 |
| fisheye-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A03, A05, A06, A09, A12 | lane | vẽ thêm vạch giả vs không vẽ | không vẽ L1 hoặc R1 | Thực tế đường không có vạch sơn hoặc bị che hoàn toàn, tuân thủ nguyên tắc không vẽ vạch không có |
| A10 | traffic_sign | biển chính gộp biển phụ vs tách biển phụ riêng | tách biển phụ riêng | Guideline Road v1.0 yêu cầu biển phụ có hộp riêng, group = supplementary |
| B05, B06, B07, B08 | lane | position L1/R1 vs other | other | Quy tắc fisheye camera hai bên sườn xe bắt buộc position = other |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Nguyễn Đăng Khoa    Quyết định nhận được: Release  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-04 | 1 | Đồng ý | Đã chỉnh lại chiều polyline trên A11 |
| QC1-05 | 1 | Đồng ý | Đã gộp vạch L2 trên A01 |
| QC1-11 | 1 | Đồng ý | Đã thêm điểm uốn cong cho polyline trên B08 |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| leducluong-front.zip | Có | 87 | 87 | Có (front) |
| leducluong-fisheye.zip | Có | 36 | 36 | Có (fisheye_*) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `docs/images/screens/01_project_labels.png`
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): `docs/images/screens/02_front_annotated.png`
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: `docs/images/screens/03_fisheye_annotated.png`
4. Một đoạn XML có `<polyline label="lane">`: `docs/images/screens/04_xml_snippet.png`

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
- Lỗi hay gặp nhất: Quên sửa thuộc tính mặc định của lane (mặc định luôn là L1 / solid / white / single) và chọn nhầm tag camera fisheye (fisheye_left / fisheye_right).
- Cách tránh: Tuân thủ quy trình 6 bước, luôn gắn tag camera theo đúng hậu tố file đầu tiên và kiểm tra Details ngay sau khi vẽ xong từng shape.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
- Nhãn đi vào bài toán nhận diện làn đường (LKA - Lane Keeping Assist) và bài toán xác định vùng di chuyển (Drivable Area Segmentation).
- Nếu gán nhầm thuộc tính position từ L1 thành L2 hoặc vẽ ngược chiều polyline (từ xa về gần), mô hình học máy và thuật toán điều khiển bám làn sẽ ước lượng sai tim làn và hướng di chuyển của xe, dẫn tới hệ thống LKA can thiệp đánh lái sai lệch gây nguy hiểm.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
*(Tính trên vạch L1 ảnh A01 bằng lệnh `python -m road_lab.rowanchor leducluong-front.zip --image A01 --position L1`)*
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 108.0 | 155.4 | 202.8 | 250.3 | 297.7 |
| x của bạn kia | 109.5 | 156.0 | 201.2 | 252.0 | 299.1 |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?
   - Hàng xa xe nhất (y = 560) sẽ nằm ngoài phạm vi vẽ của polyline và bị đổi thành "không có làn".
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?
   - Ở hàng 720 hai bạn lệch 1.5 px; ở hàng 560 lệch 1.4 px.
   - Lệch ở hàng 720 (ngay sát bánh xe trước) ảnh hưởng nghiêm trọng hơn tới LKA vì nó quyết định trực tiếp tới góc đánh lái tức thời và việc giữ xe đúng giữa làn.
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?
   - Giá trị tọa độ x theo phép nội suy toán học không đổi, nhưng thứ tự lưu trữ điểm bị đảo lộn khiến checker báo lỗi QC1-04 và các thuật toán bám chuỗi điểm theo hướng tiến của xe sẽ nhận diện sai hướng chuyển động.
