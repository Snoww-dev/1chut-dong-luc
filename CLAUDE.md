# CLAUDE

## Tổng quan
Đây là một trang web tĩnh hiển thị các câu nói truyền cảm hứng và hài hước bằng tiếng Việt. Toàn bộ ứng dụng được triển khai trong một file duy nhất: `index.html`. Nội dung gồm HTML, CSS, và JavaScript đều được nhúng trực tiếp.

## Chức năng chính
- Hiển thị câu nói ngẫu nhiên khi bấm nút `Cho tôi một câu`
- Cho phép người dùng thêm câu mới qua modal với:
  - nội dung câu
  - tác giả
  - hình ảnh kèm theo (dán link hoặc tải file)
- Lưu trữ câu người dùng thêm trong `localStorage` với khóa `inspire_custom_quotes_v1`
- Hiển thị hình ảnh kèm câu nếu có
- Hỗ trợ thay đổi giao diện màu sắc bằng panel theme
- Lưu trữ theme đã chọn trong `localStorage` với khóa `inspire_theme_v1`

## Cấu trúc chính
- `baseQuotes`: mảng câu mặc định (hàng trăm câu nói)
- `custom`: mảng câu người dùng thêm, nạp trước từ `localStorage`
- `allQuotes()`: trả về danh sách ghép `baseQuotes.concat(custom)`
- `pick()`: chọn ngẫu nhiên một câu, tránh lặp ngay câu vừa hiển thị
- `show(t, a, img)`: hiển thị nội dung câu, tác giả và ảnh nếu có

## Modal thêm câu mới
- Mở modal: `openModal()`
- Đóng modal: `closeModal()`
- Lưu câu mới: `saveBtn.addEventListener('click', ...)`
- Kiểm tra nội dung tối thiểu 3 ký tự
- Nếu người dùng chọn tải file ảnh, file được đọc bằng `FileReader` và mã hóa Base64
- Nếu ảnh quá lớn hoặc lưu `localStorage` thất bại, hiện thông báo lỗi

## Theme và màu sắc
- Bây giờ giao diện chọn theme hiển thị danh sách ảnh/video có sẵn trong thư mục `img/`
- Chọn ảnh sẽ áp dụng làm background tĩnh
- Chọn video sẽ phát làm background lặp lại
- Mặc định nếu không chọn vẫn giữ nền gradient tối sẵn có
- Có nút reset về giao diện mặc định

## UI / CSS
- Giao diện tối, sử dụng font `Fraunces` và `Be Vietnam Pro`
- Hiệu ứng chuyển đổi mềm mại cho câu và hình ảnh
- Panel theme cố định, overlay modal, nút bo tròn
- Background có hoạ tiết noise mờ bằng SVG data URI

## Điểm đáng chú ý
- Ứng dụng chạy hoàn toàn client-side, không có backend
- Dữ liệu người dùng chỉ lưu cục bộ trong trình duyệt, không đồng bộ
- Mã HTML và JavaScript được gộp chung trong một file, dễ copy/paste nhưng khó bảo trì với dự án lớn
- Ảnh file được lưu dưới dạng Base64 vào `localStorage`, có thể gây tốn dung lượng nếu ảnh quá lớn

## Gợi ý cải tiến
- Tách CSS/JS ra file riêng để dễ bảo trì
- Thêm thông báo số lượng câu đã lưu hoặc tổng câu hiện có
- Hạn chế kích thước ảnh và thêm cơ chế xóa câu người dùng
- Kiểm tra đầy đủ giá trị URL ảnh trước khi hiển thị
- Thêm tính năng chọn ngẫu nhiên câu theo nhóm chủ đề
