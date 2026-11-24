# Sơ đồ lớp 12A8

Trang web tĩnh hiển thị và **chỉnh sửa trực tiếp** sơ đồ chỗ ngồi lớp 12A8. Dữ liệu lưu trên Firebase (Firestore), mọi người mở link đều thấy thay đổi ngay.

## Các file

| File | Nội dung |
|---|---|
| `index.html` | Toàn bộ trang web (1 file duy nhất, không cần build) |
| `SoDoLop12A8.xlsx` | File Excel cũ từ thời dùng Google Sheet — không còn được web đọc |

## Dữ liệu trên Firebase

- Project dùng chung: `linhtinh-web-2026` (cùng các web khác), Firestore database `(default)`.
- Chỉ dùng collection **`sodolop12a8`**, tài liệu `layout` (sơ đồ hiện tại, dạng 1 chuỗi JSON).
- Rules cho phép ai có link đọc/ghi hai tài liệu `layout` và `backup`, mỗi tài liệu dưới 100KB, không xóa được. Khi sửa rules chung của project nhớ giữ nguyên khối `match /sodolop12a8/...` này.
- Lần đầu mở mà chưa có dữ liệu, web tự ghi sơ đồ mặc định (`DEFAULT_GROUPS` trong `index.html`) lên Firebase.
- Cấu hình kết nối nằm ở `CONFIG.FIREBASE` trong `index.html` (khóa web của Firebase vốn công khai, bảo vệ bằng rules).

## Chức năng trên web

- **👩‍🎓 / 🧑‍🏫** — đổi giữa góc nhìn học sinh và góc nhìn giáo viên (tự xoay 180°).
- **Kéo thả** một học sinh sang ô khác để đổi chỗ (điện thoại: giữ ~0,3 giây rồi kéo). Thả vào ô trống thì chuyển chỗ.
- **Sửa tên**: bấm đúp vào ô (điện thoại: chạm một lần). Để trống tên = bỏ trống ô.
- Bàn giáo viên mặc định **trên - phải** (góc nhìn học sinh), đổi `CONFIG.DESK` trong `index.html` nếu cần.
- **↩️ Hoàn tác** — tối đa 50 bước, mất khi tải lại trang.
- **🖼️ Tải ảnh PNG / 📄 Tải PDF** — luôn dựng ở bề rộng cố định 1280px và PDF luôn A4 ngang, nên xuất trên điện thoại cũng giống máy tính.

Mọi thay đổi tự lưu lên Firebase. Nếu mất kết nối Firebase, web hiện sơ đồ mặc định ở chế độ chỉ xem và báo lỗi rõ ràng.

## Deploy lên GitHub Pages

Vào repo → **Settings → Pages** → *Source*: `Deploy from a branch` → nhánh `main`, thư mục `/ (root)`.
