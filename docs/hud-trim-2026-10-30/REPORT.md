# Chỉnh khung điều khiển, mặt đồng hồ và cần số — 30/10/2026

Đã phát hành lên https://blueline2026.pages.dev/.
Deployment cuối: `a703320a-2eee-4a7e-9c4f-55476b818ae8`, trạng thái `deploy: success`.
Bản cố định: https://a703320a.blueline2026.pages.dev/.

## Thay đổi theo yêu cầu

- Bỏ nền, đường viền và bóng của khung chung bao ngoài các cụm. Giữ nền riêng từng cụm để chữ dễ đọc. Cảnh 3D được vẽ toàn màn hình phía sau các khoảng trống; căn hình ảnh để xe và phần đường quan sát không nằm dưới bảng. Cabin có mức dịch khung nhỏ hơn góc bám theo xe.
- Cần số chỉ hiện P/R/N/D, bỏ chữ Đỗ/Lùi/Mo/Tiến và tiêu đề Cần số. Giữ tên trợ năng và chú thích khi trỏ chuột.
- Mặt đồng hồ có thang 0–180 km/h khớp cung tốc độ, vạch chia gọn, số đọc chính rõ và RPM rút gọn đơn vị. Không đổi tốc độ thực hay thuật toán điều khiển xe.
- Cụm số có hàng trạng thái riêng, bỏ giới hạn chiều cao gây cắt chữ. Trạng thái N được rút gọn. Thông báo dài tạm hiện phía trên cụm; trên điện thoại được nâng lên trên cả hàng Xe/ADAS/360°.
- Bổ sung bố cục cho cửa sổ máy tính từ 840 px; giữ kiểm soát chạm và các module hiện có.

## Kiểm tra

- `npm run build`: đạt. Còn cảnh báo kích thước gói Three.js khoảng 552 kB, không phải lỗi build.
- Bảy nhóm test đạt: `pedal-console-input-test`, `touch-steering-test`, `render-geometry-test`, `render-runtime-test`, `view-quality-test`, `cockpit-view-test`, `cabin-look-test`.
- Trình duyệt local: góc bám xe/cabin; 1440×900, 844×390, 568×320; thao tác P/N/D và thông báo dài. Thông báo P có `scrollHeight = clientHeight = 32`, không bị cắt, nằm trên hàng chọn bảng và trong màn hình.
- Bản công khai: tải đúng `index-rIIhL-fY.js`, `index-DylNDPBC.css`; bốn nút số có nội dung chính xác P/R/N/D; khung chung có viền 0 và nền trong suốt.
- Trạng thái số ở bản công khai 1440×900 và 844×390 nằm trong cụm, không bị cắt. Không tràn ngang và không có lỗi console mức error trong phiên cuối.
- Ảnh: `live-desktop.jpg`, `live-phone.jpg`. Đây là kiểm tra trình duyệt trên laptop, chưa phải điện thoại vật lý.

## Đồng bộ nguồn

Mã đã sửa tại workspace và phát hành trực tiếp qua Cloudflare. GitHub vẫn chưa có commit đồng bộ do công cụ ghi trước đó bị từ chối HTTP 403. Không đổi cấu hình tự build; lần build từ mã GitHub cũ có thể ghi đè bản mới.

`source-update.zip` chứa đủ 14 tệp nguồn/test cần đồng bộ, gồm cả các thay đổi giao diện trước đó. Các thuật toán ADAS, vật lý, giao thông và tài sản xe không thay đổi trong đợt này. Bộ test trên không phải kiểm thử lại toàn bộ các tình huống giao thông.
