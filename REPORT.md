# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602048
- Ngày / CVAT local: 17/09/2026 / CVAT local
- Công cụ đã dùng: Brush, Polygon

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000458325.jpg`, người đàn ông đang trượt ván
- Class và quy tắc tôi dùng để chọn biên: Class là person, biên bám sát thân người từ trên xuông dưới
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: không dùng
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: medium_instance, ảnh 000000181542.jpg, tập trung vào khu vực vỉa hè phía sau cửa hàng Chanel và phần cửa sổ xe buýt.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: thiếu-thừa vật, Gán thừa đối tượng (false positive), chủ yếu là các đối tượng nhỏ và mờ ở xa.
- Bằng chứng tôi nhìn thấy: Ở lần export đầu, kết quả có 86 annotations, trong đó riêng ảnh này có 40 object, trong khi ground truth chỉ ghi nhận 20 object. Sau khi kiểm tra, tôi nhận ra mình đã đánh nhãn cả những người đi bộ rất nhỏ ở phía xa và các hành khách mờ nhìn thấy sau cửa kính xe buýt.
- Quy tắc và hành động sửa: Tôi áp dụng nguyên tắc chỉ gán nhãn những cá thể có thể quan sát rõ và phân biệt độc lập. Các hành khách bên trong xe buýt không được tách thành những instance riêng. Tôi mở lại job trên CVAT, loại bỏ các mask person nhỏ và không đủ rõ, sau đó giảm tổng số object của task xuống còn 71, trùng với ground truth.
- Sau sửa đã Save và export lại chưa? Đã Save trên CVAT và export lại thành file medium_instance.zip mới trong thư mục submissions/

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

Sau khi chạy lại scorer, số object của bài nộp khớp hoàn toàn với ground truth: 71/71, count error = 0. Precision tăng từ 0.59 lên 0.70, số false positive giảm từ 35 xuống 21, còn mean matched IoU đạt 0.770. Scorecard của ba tier đạt 72.9/82, gồm Easy 17.9, Medium 25.0 và Hard 30.0.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp1_holes` (ảnh `000000144300.jpg`): Kính chắn gió và nan hoa mô tô | Khoét bỏ vùng kính chắn gió và nan hoa bánh xe vì nhìn xuyên qua thấy nền, hay giữ nguyên trong mask? | Quy tắc checkpoint: Kính xe, nan hoa, khe hở động cơ là một phần của vật thể, không khoét lỗ tùy tiện. | Quyết định giữ nguyên vẹn toàn bộ kính chắn gió và nan hoa bánh xe trong mask `motorcycle`, không khoét lỗ. |
| 2. `cp2_slice` (ảnh `000000017627.jpg`): Hai xe ô tô đỗ sát nhau ở bãi đỗ | SAM gộp 2 xe cạnh nhau (sedan đen và wagon trắng) thành 1 mask lớn hay tách rời? | Quy tắc instance: Hai vật cùng class nhưng là hai thực thể vật lý riêng biệt phải là 2 instance. | Quyết định dùng công cụ Slice (phím tắt Alt + J) cắt đôi đường biên tiếp giáp thành 2 mask `car` riêng. |
| 3. `cp4_curb` (ảnh `7d83710e-4697c3b2.jpg`): Ranh giới bó vỉa giữa đường và vỉa hè | Vùng mép đường sát vỉa hè cùng màu nhựa/bê tông tối: gán toàn bộ là `road` hay tách `sidewalk`? | Quy tắc semantic: Phân định ranh giới chức năng dựa vào gờ bó vỉa (curb) nhô cao hơn mặt đường xe chạy. | Quyết định phóng to 100%, lần theo mép gờ bó vỉa để gán phần lòng đường là `road` và phần gờ nâng cao là `sidewalk`. |