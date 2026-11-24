# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): nguyendangkhoa        Người kiểm (học viên): Lê Đức Lương  
Ngày: 2026-11-24                              Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): nguyendangkhoa-front.zip, nguyendangkhoa-fisheye.zip (rev 1)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm)                 Số nhãn đã kiểm (shape + tag): 42  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 8 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 6 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 10 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 4 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 5 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 2 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 14 | 0 | chính |
| QC1-12 file | lỗi file | 42 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A02 | lane#2 | chính | Polyline R1 kết thúc sớm khoảng 25 px trước điểm xa nhất còn thấy vạch |
| 2 | QC1-07 | B04 | drivable#1 | chính | Polygon drivable direct lấn nhẹ khoảng 6 px lên cản sau xe mình |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A06 | Vạch qua đường bị mờ góc trái, có cần gán trùm hết không? | Đã trao đổi: Ước lượng theo cung và vẽ bao trọn |

## Quyết định
Lỗi nặng: 0    Lỗi chính: 2 / 42 nhãn = 4.8%    Lỗi nhẹ: 0    Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): Release  
Lý do (theo luật của phiếu): Không có lỗi nặng và tỉ lệ lỗi chính 4.8% ≤ 5.0% (đạt ngưỡng chấp nhận).  

---
*Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng.*
