# Sơ đồ lớp 12A8

Trang web tĩnh hiển thị sơ đồ chỗ ngồi lớp 12A8, đọc dữ liệu trực tiếp từ Google Sheet.

## Các file

| File | Nội dung |
|---|---|
| `SoDoLop12A8.xlsx` | File Excel để upload lên Google Sheets (chỉ chứa **góc nhìn học sinh**) |
| `index.html` | Toàn bộ trang web (1 file duy nhất, không cần build) |

## Các bước sử dụng

### 1. Đưa Excel lên Google Sheets

1. Vào https://sheets.google.com → **Tệp → Nhập → Tải lên** → chọn `SoDoLop12A8.xlsx`.
2. Kiểm tra tab đầu tiên tên là **`SoDoLop`** (quan trọng — web đọc đúng tên tab này).
3. Bấm **Chia sẻ** → mục *Quyền truy cập chung* → chọn **Bất kỳ ai có đường liên kết** → vai trò **Người xem**.

### 2. Nối web với Sheet

**Đã cấu hình sẵn** trong `index.html` với Sheet hiện tại:

```js
const CONFIG = {
  SHEET_ID:   "1p1EpjqGQT0Tai5Sdi6LUvem5wtlOI7qfsient6o5wRM",
  SHEET_NAME: "SoDoLop",
  TITLE:      "SƠ ĐỒ LỚP 12A8",
  DESK:       "Trên - Phải"
};
```

Nếu sau này đổi sang Sheet khác, lấy ID là phần nằm giữa `/d/` và `/edit` trong link rồi thay vào `SHEET_ID`.

> Cách khác, không cần sửa code: mở web rồi bấm nút **⚙️** và dán link vào (lưu trong trình duyệt của bạn),
> hoặc thêm tham số vào URL: `index.html?sheet=<ID>`

### 3. Deploy lên GitHub Pages

```bash
git init
git add .
git commit -m "So do lop 12A8"
git branch -M main
git remote add origin https://github.com/<tên-tài-khoản>/<tên-repo>.git
git push -u origin main
```

Vào repo trên GitHub → **Settings → Pages** → *Source*: `Deploy from a branch` → chọn nhánh `main`, thư mục `/ (root)` → **Save**.
Sau ~1 phút web sẽ chạy ở `https://<tên-tài-khoản>.github.io/<tên-repo>/`.

## Cách nhập liệu trong Sheet

Chỉ nhập **góc nhìn học sinh**. Góc nhìn giáo viên web tự xoay 180°.

### Chỗ ngồi

| Hàng | Dãy 1 - A | Dãy 1 - B | Dãy 2 - A | Dãy 2 - B | Dãy 3 - A | Dãy 3 - B |
|---|---|---|---|---|---|---|

- **Hàng 1** = bàn đầu, gần bàn giáo viên nhất. Hàng lớn nhất = bàn cuối.
- **A** = chỗ bên trái, **B** = chỗ bên phải (theo góc nhìn học sinh).
- Ô trống = chỗ ngồi trống, web hiển thị ô rỗng màu xám.
- Hàng trống hoàn toàn ở cuối bảng sẽ tự động bị ẩn.

**Thêm hàng:** thêm dòng mới bên dưới, cột `Hàng` ghi số tiếp theo.
**Thêm dãy:** thêm 2 cột mới tên đúng định dạng `Dãy 4 - A`, `Dãy 4 - B` — web tự nhận.

### Bàn giáo viên

Cột **`Bàn giáo viên`** (ô màu cam, cột `I`) — điền **một giá trị duy nhất ở dòng đầu tiên**:

| Giá trị | Góc nhìn học sinh | Góc nhìn giáo viên (web tự xoay) |
|---|---|---|
| `Trên - Trái` | trên, bên trái | dưới, bên phải |
| `Trên - Giữa` | trên, ở giữa | dưới, ở giữa |
| `Trên - Phải` | trên, bên phải | **dưới, bên trái** ← sơ đồ hiện tại |
| `Dưới - Trái` | dưới, bên trái | trên, bên phải |
| `Dưới - Giữa` | dưới, ở giữa | trên, ở giữa |
| `Dưới - Phải` | dưới, bên phải | trên, bên trái |

Chỉ khai báo theo **góc nhìn học sinh**; góc nhìn giáo viên web tự xoay 180° cả trên/dưới lẫn trái/phải.
Bỏ trống hoặc thiếu cột → web dùng mặc định `Trên - Phải`.

Sửa Sheet xong chỉ cần bấm **🔄 Tải lại dữ liệu** trên web (hoặc tải lại trang) là thấy thay đổi.

## Chức năng trên web

- **👩‍🎓 / 🧑‍🏫** — đổi giữa góc nhìn học sinh và góc nhìn giáo viên.
- **🖼️ Tải ảnh PNG** — xuất sơ đồ đang xem ra file ảnh.
- **📄 Tải PDF** — xuất sơ đồ đang xem ra PDF khổ A4 nằm ngang.
- **📊 Mở Google Sheet** — mở nhanh Sheet ở tab mới để chỉnh sửa.
- **⚙️** — đổi link Google Sheet ngay trên trình duyệt.

Nếu chưa cấu hình Sheet hoặc mạng lỗi, web tự hiển thị dữ liệu mẫu có sẵn trong `index.html`
(khối `FALLBACK`) để sơ đồ không bao giờ trắng trang.
