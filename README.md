# Dao Mai View Phone

Ứng dụng desktop (Windows, Linux) chiếu và điều khiển hàng chục đến hàng trăm điện thoại Android
cắm USB hoặc kết nối Wi-Fi vào máy tính. Mỗi điện thoại một luồng H.264 riêng qua adb, máy tính
giải mã bằng FFmpeg (ưu tiên GPU). Tải bản mới nhất ở
[Releases](https://github.com/conkiubebong/DaoMaiViewPhone_Update/releases).

## Tính năng

### Xem và điều khiển
- **Lưới thẻ máy trực tiếp**: mỗi điện thoại một ô video; hiện số thứ tự, tên, serial, IP; xoay ô; tìm kiếm, lọc theo thẻ; kính lúp.
- **Màn lớn**: bấm đúp ô để mở; chạm / kéo / gõ phím trực tiếp; cố định cạnh lưới hoặc thả nổi; nghe âm thanh máy đang phóng to (Windows, Android 11+).
- **Điều khiển ngay trên ô nhỏ** không cần mở màn lớn.
- **Đồng bộ thao tác**: chọn nhiều máy (Ctrl / Shift / kéo khung), thao tác trên một máy lặp lên tất cả.
- **Bảng chức năng**: Đa nhiệm, Home, Back, Thông báo, Cài đặt nhanh, Nguồn, Âm lượng, Màn trước / sau, vuốt 4 hướng, xoay, chụp màn hình, gửi văn bản; mở nhanh Cài đặt / Wi-Fi / Bàn phím / Ngôn ngữ / Trợ năng; tự sắp xếp nút Hiện / Ẩn.
- **Tay cầm ảo**: gán phím / chuột thành chạm, vuốt, giữ, chụm 2 ngón.
- Tắt màn hình điện thoại nhưng vẫn chiếu; tự tắt khi kết nối; hiện vị trí chạm; tự đặt độ phân giải & DPI.
- **Bàn phím DaoMaiIME** tự cài, đặt khi kết nối, trả bàn phím cũ khi ngắt.

### Hiệu năng
- Ba mẫu: **Nhiều máy (tiết kiệm)** · **Cân bằng** · **Mượt nhất**.
- **Stream Siêu Cao**: điện thoại mã hoá đúng cỡ ô đang hiện; màn lớn có bộ mã hoá riêng theo độ phân giải / bitrate / FPS.
- **Video theo nhu cầu** (tắt luồng máy không ai xem), chỉ giải mã ô đang hiện, làm mới ô ngoài khung theo chu kỳ.
- Bộ giải mã Tự động / Phần cứng (d3d11va, vaapi) / Phần mềm; bộ mã hoá phần cứng hoặc OMX.google.h264; thống kê video từng máy.

### File, APK, văn bản
- **Cài APK hàng loạt**: .apk / .xapk / .apkm / .apks, split + OBB, nhiều máy song song, cài lại mục lỗi.
- **Nhập file**, **Phân phối file** (mỗi máy 1–100 file theo số thứ tự, quay vòng), **Xem / xuất file trên máy** (duyệt thư mục, xuất giữ cấu trúc, xoá, tạo thư mục).
- **Phân phối văn bản** theo dấu phân cách / regex; **Clipboard nhiều máy**; **Cụm từ nhanh** theo nhóm; **Ảnh nền số** (mỗi máy một ảnh có số thứ tự).
- **Truyền file chạy nền** có tiến độ, dừng, thử lại, chờ máy online lại; dùng `push-daomai` / `pull-daomai` (LZ4) với adb DaoMai.

### Tự động hoá
- **Ghi thao tác** (chạm, vuốt, phím, chữ) → **Chạy thao tác**: tốc độ, giờ bắt đầu, số vòng, nghỉ giữa vòng, lệch giữa máy; chạy ngay trên máy (đẩy .sh).
- **Vuốt tự động** 4 hướng, lặp, nghỉ ngẫu nhiên.
- **Console lệnh** shell / Automation API nhiều máy: lệnh có sẵn (tắt máy, âm lượng, Wi-Fi, DPI, độ phân giải, pin, app), tìm phần tử theo text, bấm, chạm toạ độ; lệnh yêu thích, lịch sử, log theo máy.
- **Danh sách tác vụ**, dừng từng cái hoặc tất cả.
- **Ứng dụng**: tìm, mở, dừng, xoá dữ liệu, gỡ, ghim, xuất APK trên nhiều máy.
- **Proxy**: một proxy cho nhóm, phân phối mỗi máy một proxy, bypass theo danh sách.

### Quản lý máy
- **Thẻ / nhóm thiết bị**: tạo, thêm bớt, thu gọn, sắp xếp, lọc; sao lưu / khôi phục ra file.
- Đổi số thứ tự, đổi tên, sao chép serial, khởi động lại nhiều máy, xoá máy mất kết nối; hộp **Thiết bị** có tìm và phân trang.

### Mạng, Wi-Fi, nhiều máy tính
- **Mạng / OTG**: quét dải IP, cổng ADB 5555, quét tất cả, tự quét theo chu kỳ.
- **Đa PC** (adb DaoMai Multi-Server ≥ 6.3.0 kèm sẵn): **Node** (mặc định) cho máy khác trong LAN xem điện thoại cắm ở máy này, hiện `IP:5037` để sao chép; **Server** nhập hoặc **Quét LAN** các PC Node, điện thoại của chúng hiện trong lưới như cắm trực tiếp. Đổi chế độ áp dụng ngay, không khởi động lại adb.

### Tài khoản, giấy phép, cập nhật
- **Free**: dùng ngay, tối đa 40 máy. **VIP**: đăng nhập tài khoản kích hoạt, giấy phép gắn máy, chạy offline tới hết hạn.
- **Tự cập nhật** (Windows): kiểm tra bản mới khi mở, tải, kiểm sha256, thay file và chạy lại.
- **7 ngôn ngữ**: Tiếng Việt, English, 中文, 日本語, 한국어, ไทย, Português.
- **Đồng bộ cài đặt** sao lưu / khôi phục ra JSON; phím tắt tuỳ chỉnh.

### Nền tảng
- **Windows 10/11**: `DaoMaiView.exe`, giải mã d3d11va, âm thanh, tự cập nhật.
- **Linux x86_64** (glibc ≥ 2.31, X11 / Wayland, OpenGL): giải mã vaapi; chưa có âm thanh và tự cập nhật.

## Gói tải (Releases, tag `v<phiên bản>`)

- `DaoMaiView-<ver>.zip` — Windows: `DaoMaiView.exe`, `update.exe`, `daomai.apk`, `daomai-adb\` (adb DaoMai + 2 DLL), (`*.dll` FFmpeg khi là gói đầy đủ). Giải nén đè lên bản cũ.
- `DaoMaiView-<ver>-linux-x86_64.tar.xz` — Linux: `DaoMaiView`, 4 lib FFmpeg, `daomai.apk`, `daomai-adb/adb`, `run.sh`. Giải nén rồi `sh native/run.sh`.
- `SHA256SUMS-v<ver>.txt`.

## Kênh cập nhật

App đọc `latest.json` ở nhánh `main` (`version`, `build`, `url` = asset trong Releases, `sha256`, `size`, `notes`, `min_build`), có bản mới thì tải và tự thay thế bằng `update.exe`. Phát hành từ repo nguồn: `tools\release_native.ps1 -Build N -Notes "..." [-WithDlls] -Push`.
