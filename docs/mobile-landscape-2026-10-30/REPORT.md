# BlueLine — giao diện điện thoại xoay ngang, 30/10/2026

## Kết quả

Đã sửa mã nguồn tại laptop và triển khai bản production lên https://blueline2026.pages.dev/.

- Deployment: `2ab22874-389b-4a60-85ca-b29d6ea702d9`, trạng thái Cloudflare `deploy: success`.
- URL cố định của bản này: https://2ab22874.blueline2026.pages.dev/.
- Trình duyệt trên URL chính tải đúng `index-E0kl9YTS.js` và `index-B6P9opG2.css` của bản build đã kiểm tra.

## Thay đổi

- Bố cục riêng khi màn hình nằm ngang, rộng tối đa 1024 CSS px và cao tối đa 540 CSS px.
- Nút giữ đánh lái và xi nhan bên trái; ga/phanh bên phải. Các điều khiển hiện có được chuyển vị trí, không nhân bản bộ điều khiển.
- Ba mục ở giữa: Xe, ADAS và 360°. Đồng hồ tốc độ, số đang chọn, trạng thái hỗ trợ và khoảng cách màu vàng luôn có chỗ hiển thị.
- Camera nằm trong bảng dưới; có thể vừa lái vừa quan sát. Vào R mở mục camera lùi. Trạng thái cảm biến sau và cảnh báo lùi dùng dữ liệu mô phỏng hiện có.
- Cài đặt/tình huống mở thành bảng cuộn riêng, có nút đóng; công tắc ADAS và điều chỉnh ACC vẫn nối tới logic hiện có.
- Giữ ga/lái không bị xóa chỉ vì chuyển giữa các mục Xe / ADAS / 360°. Xoay màn hình hoặc mở bảng cài đặt sẽ nhả lệnh đang giữ.
- Menu bắt đầu gọn hơn và có hướng dẫn nút chạm. Thêm vùng an toàn cho tai thỏ/thanh home, chiều cao `dvh` và nhắc xoay ngang khi đang ở màn hình dọc.
- Không sửa thuật toán ADAS, vật lý, giao thông, chất lượng đồ họa hoặc âm thanh trong đợt này.

## Kiểm tra đã thực hiện

| Kiểm tra | Kết quả |
| --- | --- |
| `npm run build` | Đạt, TypeScript và Vite production build |
| `pedal-console-input-test` | Đạt: bàn đạp, nhiều pointer, hủy pointer, focus và PRND |
| `drive-input-test` | Đạt: bàn phím, các phím phanh, lái và nhả lệnh |
| `cockpit-view-test` | Đạt kiểm tra hình học, không thay cho kiểm tra hình ảnh |
| `cabin-look-test` | Đạt |
| 568×320, 667×375 | Xem trực tiếp, các nút chính trong màn hình, không tràn ngang |
| 844×390 | Xem menu bắt đầu, ba mục điều khiển, cabin cùng camera, bảng cài đặt |
| 932×430 | Kiểm tra các nút lái/bàn đạp và bộ chọn khoảng cách nằm trong màn hình |
| 1280×720 sau khi đổi kích thước | Điều khiển trở về cụm máy tính; mỗi ID điều khiển chỉ có một phần tử |
| 390×844 | Nhắc xoay ngang xuất hiện; rời bố cục ngang đúng |
| Thao tác trên localhost | Giữ ga tăng tốc, phanh về 0, vào R tự chuyển mục camera; công tắc ACC đổi trạng thái |
| URL Cloudflare công khai ở 844×390 | Đúng bản build, hiện bố cục mới và camera; không có lỗi console mức error hoặc nội dung `boot-error` trong phiên kiểm tra |

Ảnh minh chứng nằm cùng thư mục. Các kích thước trên được kiểm tra bằng trình duyệt trên laptop, không phải điện thoại vật lý.

## Giới hạn và mã nguồn GitHub

- Chưa kiểm tra Safari/iOS và Chrome/Android trên máy thật, thao tác đa chạm vật lý, nhiệt độ máy hoặc FPS trên từng dòng điện thoại. Bộ test đa pointer là kiểm tra logic, không thay cho thử phần cứng.
- Vite vẫn cảnh báo gói Three.js khoảng 552 kB trước gzip; đây là cảnh báo kích thước, build không thất bại.
- Plugin GitHub đọc được `LuSvRicon/blueline2026` nhưng thao tác tạo tree bị HTTP 403 `Resource not accessible by integration`. Không có commit GitHub mới được tạo.
- Đã dùng API Cloudflare và quyền upload ngắn hạn của chính dự án để phát hành bộ 23 tài sản trong `dist`, tái sử dụng các tài sản đã có, rồi tạo deployment production. Không đổi kết nối GitHub hay cài đặt tự build.
- **GitHub vẫn là mã cũ. Lần build tiếp theo từ GitHub có thể thay giao diện mới bằng mã đó.** Gói `source-update.zip` chứa đủ năm tệp cần đồng bộ vào gốc repository: `index.html`, `src/main.ts`, `src/ui/CockpitLayout.ts`, `src/ui/IntroOverlay.ts`, `src/ui/mobile.css`.
- ADAS vẫn là mô hình mô phỏng; đợt kiểm tra này không chứng nhận các thuật toán trên xe thật hoặc mọi tình huống giao thông.
