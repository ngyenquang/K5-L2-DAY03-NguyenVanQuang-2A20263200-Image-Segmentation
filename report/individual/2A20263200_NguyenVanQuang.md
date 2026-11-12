# Báo cáo thực hành Day 3 

- Mã học viên theo lớp: 2A20263200
- Ngày / CVAT local: 11–12/11/2026 / CVAT local
- Công cụ đã dùng: CVAT local (Brush/Polygon, gợi ý biên có sẵn trong CVAT)

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

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh `000000181542.jpg`, vẽ theo thứ tự từ trái qua phải, object đầu tiên là người (`person`).
- Class và quy tắc tôi dùng để chọn biên:   lớp `person`. Sử dụng Brush để tô theo đường viền vật thể, bám sát biên thực tế, không lấy phần nền và không bỏ sót phần thuộc đối tượng.
- Nếu không dùng gợi ý: Không dùng. Tôi tự xác định vùng cần phân đoạn dựa trên hình ảnh gốc, sử dụng công cụ Brush (cọ) để tô lên toàn bộ vùng đối tượng cần gán nhãn. Tôi điều chỉnh kích thước cọ phù hợp, tô sát đường viền, đảm bảo không bỏ sót phần đối tượng và tránh tô nhầm sang vùng nền.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: medium_instance, ảnh `000000373353.jpg` (mask #13 `car`, #12 `person`) và ảnh `000000458325.jpg` (mask #15 `car`).
- Lỗi thuộc loại: gộp-tách.
- Bằng chứng tôi nhìn thấy: vẽ chồng mask lên ảnh thì mask #13 phủ toàn bộ taxi hai bên đường như một object, mask #15 phủ toàn bộ xe đỗ hai bên đường như một object, mask #12 gộp cả nhóm người đi bộ. Ở ảnh `000000181542.jpg`, mask #6 `person` gồm cả người phụ nữ ở giữa và người lái xe máy bên trái. Đề yêu cầu mỗi vật đếm được là một mask riêng.
- Quy tắc và hành động sửa: quy tắc là một vật đếm được = một instance. Hướng sửa: tách từng xe, từng người thành mask riêng trong CVAT. Chưa sửa vì hết thời gian lab; các mask gộp vẫn còn trong bài nộp.
- Sau sửa đã Save và export lại chưa? Chưa. Tính đến lúc viết, `medium_instance.zip` vẫn là bản export cũ chứa các mask gộp.


## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `000000181542.jpg`, xe máy bên phải (mask #3 và #4) | Phần vàng giữa người lái và xe có thể thuộc cùng xe máy, hoặc là một vật riêng | Mask #4 `motorcycle` đang tách khỏi mask #3 `motorcycle` | Chưa kịp quyết định lại; hiện giữ hai mask như đã export. Câu hỏi coach: bộ phận rời của một xe tính chung một instance không? |
| `000000373353.jpg`, hàng taxi ở xa (mask #13) | Mỗi xe một instance, hoặc gộp xe nhỏ ở xa thành một | Đề yêu cầu mỗi vật đếm được một mask, nhưng xe ở xa rất nhỏ và chồng lên nhau | Hiện đang gộp. Câu hỏi coach: vật xa, nhỏ, chồng lấn có bắt buộc tách riêng không? |
| `000000181542.jpg`, xe buýt phía sau (mask #7, #2) | Người nhìn thấy qua cửa kính tính là `person`, hoặc là một phần của `bus` | Mask #2 `person` có vẻ phủ cả các bóng người trong cửa sổ xe buýt | Chưa kịp quyết định lại; giữ như đã export. Câu hỏi coach: người trong xe có gán `person` riêng không? |
