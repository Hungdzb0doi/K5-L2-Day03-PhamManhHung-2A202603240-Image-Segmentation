# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603240
- Ngày / CVAT local: 11/11/2026 / CVAT local
- Công cụ đã dùng: Polygon, Brush, SAM (Segment Anything)

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

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh số 1, chiếc xe ô tô màu trắng đỗ ở góc dưới cùng bên trái.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi dùng quy tắc phần nhìn thấy, vẽ sát mép gầm xe, không vẽ lẹm vào phần bóng râm dưới mặt đường. Vị trí đầu xe bị người đi bộ che khuất nên tôi vẽ bám sát viền người đi bộ, không tự suy đoán phần đầu xe bị che.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: SAM gợi ý khá chuẩn nhưng bị lem một chút ở kính chiếu hậu, tôi đã dùng Polygon để cắt phần dư đi cho đúng ranh giới thật của xe.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `medium_instance`, ảnh số 2, góc phải bên trên.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Lỗi gộp vật thể (hai xe sát nhau).
- Bằng chứng tôi nhìn thấy: Gợi ý SAM tự động gộp phần cản trước của xe đằng sau vào chung với xe đằng trước thành 1 mask duy nhất do chúng đỗ quá sát nhau và có cùng màu sắc.
- Quy tắc và hành động sửa: Áp dụng quy tắc "hai xe sát nhau vẫn là hai instance riêng biệt". Tôi đã dùng Polygon để xóa vùng bị gộp chung, sau đó tạo Object mới và vẽ lại ranh giới tách biệt rõ ràng cho xe thứ hai.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại file ZIP mới đè lên file cũ.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Chưa chạy script tự đánh giá.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Ảnh 3 (easy_semantic), lề đường bên trái | 1. Là lòng đường (road) do cùng chất liệu nhựa đường. 2. Là vỉa hè (sidewalk) do có vạch kẻ liền màu trắng phân cách. | Quy tắc phân định ranh giới theo chức năng sử dụng thực tế của khu vực. | Quyết định gán là `sidewalk` vì vạch kẻ liền chỉ ra đây là khu vực dành cho người đi bộ. |
| Ảnh cp1_holes, cửa sổ kính của xe bus | 1. Phải khoét lỗ vì nhìn xuyên qua thấy cây cối phía sau. 2. Thuộc khối thân xe nên không được khoét. | Quy tắc của cp1_holes là "Kính/khe nằm trong mask vật, không khoét tùy tiện". | Quyết định tô đặc vùng kính, gộp chung vào mask `bus`. |
| Ảnh 2 (hard_panoptic), chiếc xe ở tít đằng xa mờ mờ | 1. Bỏ qua không vẽ vì quá nhỏ và mờ (chỉ khoảng vài chục pixel). 2. Vẫn là 1 object xe nên phải vẽ. | Quy tắc vẽ phần nhìn thấy, vẫn xác định được hình khối cơ bản của xe ô tô. | Quyết định tạo một mask `car` nhỏ bao quanh bằng Brush. |