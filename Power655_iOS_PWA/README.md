# Power 6/55 — iOS / PWA

## Nội dung gói

- `index.html`: ứng dụng HTML/CSS/JavaScript không dùng thư viện bên ngoài.
- `sw.js`: bộ nhớ đệm ngoại tuyến (Service Worker).
- `manifest.webmanifest`: cấu hình ứng dụng khi thêm vào Màn hình chính.
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`: biểu tượng.

## Cách dùng tốt nhất trên iPhone — web app ngoại tuyến

1. Đưa **toàn bộ các tệp trong thư mục này** lên một website tĩnh có HTTPS (ví dụ GitHub Pages). Không chỉ tải riêng `index.html`.
2. Trên iPhone, mở đường dẫn HTTPS của website bằng **Safari**, khi có kết nối Internet.
3. Đợi trang tải xong, nhấn **Chia sẻ** > **Thêm vào Màn hình chính** (*Add to Home Screen*) > **Thêm**. Nếu Safari cho lựa chọn **Open as Web App**, bật lựa chọn này.
4. Mở biểu tượng Power 6/55 trên Màn hình chính. Sau khi tài nguyên đã được cache trong lần online đầu, công cụ có thể tạo số ngay cả khi mất kết nối.
5. Nhấn **Lưu lịch sử** để giữ từng lần tạo. Dùng **Sao lưu JSON** để có bản sao trước khi thay iPhone/xóa dữ liệu Safari.

> **Chú ý:** Không thể bảo đảm ngoại tuyến nếu chưa từng mở thành công khi online, hoặc nếu iOS đã xóa cache/dữ liệu trang. Lịch sử lưu trên thiết bị chứ không đồng bộ iCloud.

### Đưa lên GitHub Pages (cách cơ bản)

1. Tạo repository GitHub (có thể đặt tên `power655-ios`).
2. Upload **6 tệp** của thư mục vào thư mục gốc của repository.
3. Trong Settings > Pages: chọn **Deploy from a branch**, branch `main`, folder `/(root)`.
4. Sau khi GitHub Pages triển khai, mở URL HTTPS trong Safari. Đường dẫn thường có dạng `https://TEN-TAI-KHOAN.github.io/power655-ios/` (đây chỉ là ví dụ; hãy sử dụng URL do GitHub cung cấp).
5. Tiếp tục các bước Thêm vào Màn hình chính ở trên.

## Nếu chỉ muốn dùng 1 file HTML

Dùng file **`Power655_iOS.html`** được cung cấp riêng. Đây là HTML độc lập, có thể chạy trên trình duyệt / ứng dụng xem HTML có hỗ trợ JavaScript. Trên iOS, bấm trực tiếp file `.html` trong ứng dụng **Tệp / Files** thường mở qua **Quick Look**, nơi JavaScript có thể không chạy. Vì vậy, **không thể hứa rằng chỉ mở file trong Files là bấm Tạo số được**. Gói PWA/HTTPS phía trên là cách ổn định hơn.

## Thuật toán, xác suất, giới hạn

- **Cân bằng 3–3:** chọn 3 số khác nhau từ 01–31 và 3 số khác nhau từ 32–55.
- **Ngẫu nhiên 6/55:** chọn 6 số khác nhau từ 01–55.
- Mặc định 10 bộ, có thể chọn 5/10/20/50; không lặp nguyên bộ trong cùng một lần tạo.
- Ưu tiên `crypto.getRandomValues()` với rejection sampling; chỉ dùng `Math.random()` nếu Web Crypto không tồn tại trong môi trường chạy.
- Chế độ 3–3 chỉ bao phủ 9.097.880 trong 28.989.675 tổ hợp có thể có (xấp xỉ 31,38%). **Không làm tăng xác suất trúng thưởng**.
- Không có server, tài khoản, dữ liệu Vietlott, dự đoán kết quả hoặc đồng bộ lịch sử.
- Lịch sử lưu bằng `localStorage` (nếu có quyền), tối đa 30 lần. File JSON sao lưu có thể được nhập lại.

## Kiểm thử

Kiểm tra việc tạo 5/10/20/50 bộ ở hai chế độ, số không trùng trong mỗi bộ, không trùng giữa các bộ cùng lần tạo, nút Sao chép, Lưu/Mở/Xóa lịch sử, xuất/nhập JSON, và chế độ offline của URL HTTPS sau khi cài đặt.
