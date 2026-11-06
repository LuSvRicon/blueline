# BlueLine — thiết kế bảng điều khiển máy tính và điện thoại

Ngày: 30/10/2026. Production: https://blueline2026.pages.dev/.

Deployment `5f270cda-89a4-43a1-a4ca-f44e0db54d2c` đã thành công. Bản cố định: https://5f270cda.blueline2026.pages.dev/.

## Những gì đã thay đổi

- Thống nhất màu sắc, kiểu chữ, độ tương phản, viền và phản hồi tương tác. Giảm chi tiết trang trí lặp lại; giữ số liệu lấy từ mô phỏng hiện có.
- Máy tính có bảng điều khiển cao 208 px, hoặc 220 px trên màn hình lớn. Giữ cụm cần số, đồng hồ tốc độ, hỗ trợ lái, bàn đạp và camera ở dưới cảnh lái. Tại 1440×900, bảng bắt đầu ở y=666; phần trên được dành cho cảnh lái.
- Có bố cục riêng cho cửa sổ 960–1179 px: ưu tiên số đọc và điều khiển; camera vẫn nằm dưới. Thu gọn camera sẽ bỏ cột trống, có thể mở lại từ thanh công cụ.
- Điện thoại giữ hai vùng thao tác hai bên. Phanh lớn hơn ga; xi nhan cao 44 px; bàn đạp cao 84 px. Xe / ADAS / 360° dùng chung vùng giữa; tốc độ, số đang chọn, trạng thái và khoảng cách vẫn có chỗ hiển thị.
- Bổ sung lựa chọn Nút / Kéo, có nhớ lựa chọn trong trình duyệt. Kéo vô lăng dùng chuyển động tương đối của ngón tay, qua bộ điều khiển lái có làm mượt hiện có. Thả hoặc mất chạm sẽ trả lái; ngón tay thứ hai không chiếm quyền lái. Không yêu cầu quyền cảm biến chuyển động của điện thoại.
- Bảng cài đặt có nền đóng bên ngoài; Esc đóng bảng trước khi dùng để tạm dừng. Khi bảng đang mở, lệnh lái của người dùng được nhả và khóa; thế giới mô phỏng tiếp tục chạy. Khi đóng bảng cần thao tác mới, không khôi phục lệnh đang giữ cũ.
- Giữ phản hồi riêng của ga, phanh chân, phanh ADAS và phanh đỗ. Thông số màu vàng, trạng thái hỗ trợ và cảnh báo dùng dữ liệu đang có, không tạo đồng hồ giả.
- Không thay thuật toán ACC/AEB, giao thông, vật lý xe, mô hình 3D hay chất lượng đồ họa trong đợt này.

## Kiểm tra

`npm run build`: đạt. Vite còn cảnh báo gói Three.js khoảng 552 kB trước gzip; build không thất bại.

Năm nhóm test đạt:

1. `touch-steering-test`: độ kéo và hướng lái, giới hạn đầu vào, bắt đầu ở mép không giật lái, ga độc lập, ngón tay thứ hai, thả/hủy/mất chạm, reset, tạm dừng, đổi kiểu điều khiển và khóa đầu vào khi mở bảng.
2. `drive-input-test`: các phím điều khiển và xử lý mất focus/chuyển chế độ.
3. `pedal-console-input-test`: bàn đạp nhiều pointer, nhả lệnh, focus và PRND/động cơ/phanh đỗ trong phát lại.
4. `cockpit-view-test`: hình học cabin/gương/camera; kết quả hình học không thay cho đánh giá hình ảnh.
5. `cabin-look-test`: thao tác nhìn quanh và các trường hợp ngắt đầu vào.

Kiểm tra trực tiếp bằng trình duyệt:

- Local: 568×320, 844×390, 1024×768, 1180×720, 1280×720 và 1920×1080. Kiểm tra vùng hiển thị, điều khiển, camera thu gọn/mở lại và không tràn ngang.
- Kéo vô lăng bằng thao tác chuột thật trong trình duyệt: bánh lái thay đổi góc; khi kết thúc kéo không còn trạng thái giữ.
- Mở cài đặt ADAS: nút lái bị khóa; Esc đóng bảng, nút lái hoạt động lại và mô phỏng không bị tự tạm dừng.
- Production 1440×900: đúng bố cục máy tính, không tràn ngang, thanh công cụ vừa khung.
- Production 844×390: đúng bố cục điện thoại, chọn được Kéo và camera 360°, bật/tắt ACC đổi trạng thái; Esc đóng bảng.
- Production 568×320: pad lái 108×57 px; xi nhan khoảng 51×44 px; bàn đạp cao 84 px. Tất cả nằm trong màn hình, không có ID điều khiển bị nhân đôi.
- Trang công khai tải đúng `index-DO_TJFOl.js` và `index-bo5mIr7s.css`. Không có lỗi console mức error hoặc nội dung `boot-error` trong phiên kiểm tra cuối.

Ảnh chụp bản công khai: `live-desktop-1440x900.jpg`, `live-phone-844x390.jpg`, `live-phone-568x320.jpg`.

## Giới hạn và đồng bộ nguồn

- Đây là kiểm tra trình duyệt trên laptop với kích thước màn hình thay đổi và fixture sự kiện. Chưa kiểm tra đa chạm vật lý, Safari/iOS, Chrome/Android, nhiệt độ và FPS trên điện thoại thật. Không khẳng định đã đạt mức tốt nhất thế giới hoặc chạy mượt trên mọi thiết bị.
- Năm nhóm kiểm tra ở trên phục vụ thay đổi giao diện/đầu vào. Không chạy lại toàn bộ bộ tình huống giao thông và không chứng nhận ADAS như xe thật trong đợt này.
- Mã sửa đã ở workspace laptop. GitHub chưa có commit đồng bộ: công cụ GitHub trước đó từ chối quyền ghi với HTTP 403. Đã phát hành trực tiếp các tài sản build lên chính dự án Cloudflare, tái sử dụng các mô hình/tài sản không đổi.
- Không đổi cài đặt tự build của Cloudflare. Lần build từ repository cũ có thể ghi đè giao diện mới; cần đồng bộ gói `source-update.zip` vào repository trước lần build đó. Gói chứa 12 tệp nguồn/test và giữ đúng cấu trúc thư mục, bao gồm cả các thay đổi điện thoại của bản trước.
- Có bản sao các tệp trước đợt sửa tại `backups/station-ui-20261030` và lịch sử thay đổi qua Git để đối chiếu.
