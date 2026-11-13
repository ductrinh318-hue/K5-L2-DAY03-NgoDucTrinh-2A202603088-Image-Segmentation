# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603088
- Công cụ đã dùng: Polygon, Brush (tô và tẩy thủ công, không dùng SAM)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

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

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh 1 của task `medium_instance`, chiếc ô tô con (`car`) nằm ở khu vực trung tâm phía trước mặt đường.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi dùng công cụ Polygon chấm sát theo đường viền ngoài cùng của thân xe, bánh xe và gương chiếu hậu; dừng ranh giới tại mép tiếp xúc với mặt đường và các vật thể phía trước, không tự vẽ đoán phần gầm hoặc góc xe bị che khuất.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: không dùng.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `hard_panoptic`, ảnh đường phố góc rộng (khu vực dãy xe ô tô chạy dọc hai làn đường và vỉa hè bên phải).
- Lỗi thuộc loại: gộp-tách / biên
- Bằng chứng tôi nhìn thấy: Khi kiểm tra bảng Objects bên phải trước khi export, tôi phát hiện hai chiếc xe ô tô chạy nối đuôi nhau ở làn đường bên trái có viền mask hơi dính sát và một người đi xe máy (`person` + `motorcycle`) ban đầu bị tô chung một màu/một object.
- Quy tắc và hành động sửa: Áp dụng quy tắc tách riêng từng cá thể (thing) độc lập, tôi xóa object gộp, phóng to vùng đó và dùng Brush cỡ nhỏ kết hợp Polygon vẽ lại thành hai mask tách biệt (`person` riêng cho người lái, `motorcycle` riêng cho chiếc xe, và tách rạch ròi từng chiếc `car`).
- Sau sửa đã Save và export lại chưa? Đã bấm Save (`Ctrl + S`) trên CVAT và export lại file `hard_panoptic.zip` (định dạng COCO 1.0, tắt Save images) ghi đè vào thư mục `submissions/`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp4_curb` — Dải đất trồng cây và bãi đỗ xe bê tông phía bên phải lối đi bộ | Có thể gộp cả bãi đỗ xe lát xi măng trắng bên phải (nơi có xe SUV trắng đỗ) vào `sidewalk` vì màu sắc giống hệt lối đi bộ, hoặc dừng ranh giới ở mép lối đi bộ trước hàng rào sắt. | Quy tắc phân chia `road`–`sidewalk` dựa trên bó vỉa (curb) và chức năng sử dụng, không chỉ dựa vào màu sắc vật liệu bề mặt. | Tôi quyết định tô `sidewalk` từ mặt trên đá bó vỉa (gồm dải đất trồng cây và lối bê tông đi bộ) và dừng lại ở hàng rào sắt ngăn cách bãi đỗ xe. Nhờ coach xác nhận giúp phần dải đất trồng cây sát bó vỉa có tính vào `sidewalk` không. |
| 2. `cp1_holes` — Kính chắn gió trong suốt ở đầu xe mô tô và khung ben nâng bánh sau | Có thể khoét rỗng phần kính chắn gió vì nhìn xuyên thấu thấy thùng xe phía sau, và có thể gộp khung ben nâng màu đỏ ở bánh sau vào chiếc xe. | Quy tắc giữ nguyên phần kính trong suốt thuộc vật thể trong mask instance, chỉ chừa lỗ nền thật và không gộp phụ kiện rời đặt dưới đất. | Tôi tô phủ kín phần kính chắn gió vào mask `motorcycle` và đi viền sát lốp sau để tách rời khung ben nâng màu đỏ. |
| 3. `hard_panoptic` / `cp6_coverage` — Các hàng cột trụ inox đỡ mái hiên tòa nhà kính bên phải (`cp6_coverage`) | Có thể tách riêng các cột trụ inox thành `pole` hoặc gộp chung vào khối cấu trúc tòa nhà `building`. | Trong schema của `cp6_coverage` chỉ có các lớp nền chính (`building`, `sidewalk`, `road`, `sky`), các cột trụ này gắn liền kết cấu mái hiên tòa nhà. | Tôi gộp toàn bộ mái hiên và các cột trụ inox vào lớp `building`, chỉ chừa lại khoảng trống nhìn xuyên qua giữa các cột để tô `sidewalk` và `road` phía sau. |