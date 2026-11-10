# Dao Mai View Phone

**[Tiếng Việt](#tiếng-việt)** · **[English](#english)**

Tải bản mới nhất / Latest download: [Releases](https://github.com/conkiubebong/DaoMaiViewPhone_Update/releases)

---

## Tiếng Việt

Ứng dụng desktop (Windows, Linux) chiếu và điều khiển hàng chục đến hàng trăm điện thoại Android cắm USB, Wi-Fi
hoặc qua máy tính khác (Đa PC). Mỗi điện thoại một luồng H.264 riêng qua adb; máy tính giải mã bằng FFmpeg (ưu
tiên GPU).

### Cài đặt và cập nhật

- **Windows 10/11**: tải `DaoMaiView-<phiên bản>.zip`, giải nén ra một thư mục, chạy `DaoMaiView.exe`. Lần đầu
  điện thoại phải bật *Gỡ lỗi USB* và bấm *Cho phép* khi máy hỏi.
- **Linux x86_64** (glibc ≥ 2.31, X11 / Wayland): giải nén `DaoMaiView-<phiên bản>-linux-x86_64.tar.xz`, chạy
  `sh native/run.sh`.
- **Tự cập nhật** (Windows): app tự kiểm bản mới khi mở, tải nền, kiểm **chữ ký số** và sha256, rồi thay file và mở
  lại. File giống hệt bản cũ không bị ghi lại; nếu adb không đổi thì adb server **không bị tắt** nên điện thoại
  không rớt kết nối. Tải lỗi (mạng / CDN) → nút *Mở trang tải* để tải tay ở Releases.
- Chỉ chạy **một phiên** mỗi người dùng: mở lại khi đang chạy sẽ đưa cửa sổ cũ lên trước.

### Thao tác chuột và bàn phím

Màn lớn: bấm đúp một ô. Màn nhỏ: bật *Điều khiển màn nhỏ* để thao tác thẳng trên ô.

| Thao tác | Màn lớn | Màn nhỏ (bật điều khiển) |
|---|---|---|
| Chuột trái: chạm / kéo | ✓ | ✓ (cả các máy đang chọn) |
| Chuột phải | Back | Back (Ctrl + chuột phải = menu) |
| Lăn chuột | Vuốt lên / xuống tại con trỏ | Vuốt lên / xuống (lăn ở khe giữa các ô để cuộn lưới) |
| **Ctrl + lăn chuột** | Zoom to / nhỏ (chụm 2 ngón) | Zoom to / nhỏ |
| **Giữ Ctrl** | Ghim một ngón tại con trỏ tới khi nhả Ctrl | Như màn lớn |
| **Giữ Ctrl + kéo** | Ngón thứ hai → chụm / xoay thật | Như màn lớn |
| Ctrl + C / Ctrl + X | Sao chép / cắt chữ đang chọn trên máy về PC | Gửi tới máy chạm gần nhất |
| Ctrl + V | Dán clipboard của PC vào máy | Như màn lớn |
| Ctrl + A | Chọn hết trên máy | Máy đang trỏ chuột |
| Ctrl + Z / Ctrl + Y | Hoàn tác / làm lại | ✓ |
| Gõ phím | Chữ (có dấu), Enter, Backspace, mũi tên, Home/End, PgUp/PgDn | — |

- Lăn thường: mỗi nấc ≈ 5 % chiều cao màn; ngừng lăn 150 ms thì nhả ngón.
- Khi không ghim: Ctrl + click vẫn là chọn nhiều ô. Kính lúp tự ẩn khi giữ Ctrl.

### Đa PC — xem và điều khiển điện thoại của máy tính khác

Mỗi PC chạy adb DaoMai riêng (kèm sẵn trong gói). Một PC có hai vai:

- **Node** (mặc định): điện thoại cắm ở PC này. Tab *Đa PC* hiện `IP:cổng` để PC khác kết nối tới.
- **Server**: nhập (hoặc *Quét LAN*) địa chỉ các Node. Điện thoại của Node hiện trong lưới **như cắm trực tiếp**:
  xem video, chạm, gõ, cài APK, truyền file, chạy thao tác đều được.

Cách chạy bên trong:

1. adb của Server giữ danh sách Node (`server.txt`), hỏi mỗi Node danh sách máy định kỳ và gộp vào danh sách của
   mình (máy của Node có `transport_id` riêng, không trùng máy cắm tại chỗ).
2. Mỗi lệnh / luồng video tới máy của Node: app → adb Server → kết nối TCP tới adb Node → điện thoại. Video vẫn mã
   hoá trên điện thoại, chỉ đi qua 2 chặng mạng; Server không giải mã lại.
3. **Chia sẻ** (trên Node): chia sẻ tất cả, hoặc chỉ một số máy, hoặc từng máy cho riêng một IP Server. Bộ lọc áp
   cho mọi lệnh, không chỉ lúc liệt kê.
4. **Quyền xem** (trên Node): mỗi điện thoại chỉ nên có một bộ mã hoá. *Tự nhường*: Server đang xem máy nào thì
   Node tắt video máy đó; *Luôn xem*; *Tắt xem*. Server báo "đang xem" cho Node mỗi ~10 s.
5. Đổi chế độ / danh sách áp dụng ngay, không khởi động lại adb. Node rớt mạng thì máy của nó tạm xám, có lại thì
   tự hiện lại.
6. **Cổng COM** (Control Box) của Node dùng được từ Server khi IP Server có trong `allow.txt` của Node.

Mở Node ra Internet (WAN):
- Chuyển tiếp cổng adb của Node trên router.
- **Bắt buộc nên** tạo `allow.txt` (mỗi dòng một IP Server) trong thư mục cấu hình adb của Node
  (`%LOCALAPPDATA%\DaoMaiViewPhone\adb\`, cạnh `server.txt`). Có file này thì mọi IP khác bị từ chối.
- Lệnh quản trị (đổi danh sách Node, đổi chia sẻ, tắt server, cổng COM, cài driver…) **chỉ chạy từ chính máy đó**,
  không nhận từ mạng (adb DaoMai ≥ 6.6.0).
- An toàn nhất: nối các PC qua VPN (WireGuard, Tailscale…) thay vì mở cổng.

### Chức năng khác

- **Lưới**: số thứ tự, tên, serial, IP; thẻ / nhóm; tìm, lọc; xoay ô; kính lúp; tắt màn hình điện thoại nhưng vẫn
  chiếu; tự đặt độ phân giải & DPI; bàn phím DaoMaiIME tự cài.
- **Hiệu năng**: mẫu *Nhiều máy / Cân bằng / Mượt nhất*; *Stream Siêu Cao* (mã hoá đúng cỡ ô, màn lớn có bộ mã hoá
  riêng); *Video theo nhu cầu* (tắt luồng máy không ai xem); giải mã GPU (d3d11va / vaapi) hoặc CPU.
- **File / APK / văn bản**: cài APK hàng loạt (.apk/.xapk/.apkm/.apks, OBB); nhập, phân phối, xuất file; phân phối văn
  bản; clipboard nhiều máy; cụm từ nhanh; ảnh nền có số.
- **Tự động hoá**: ghi và chạy lại thao tác; vuốt tự động; console shell nhiều máy; quản lý ứng dụng; proxy.
- **Menu chuột phải với máy đang ở Recovery**: *Khởi động lại vào System*, *Khởi động lại vào Download*,
  *Format data (TWRP)*, *Wipe data* (có hỏi xác nhận).
- **Hộp Thiết bị**: trạng thái adb từng máy, khởi động lại theo chế độ, nút *Khởi động lại adb server* (chỉ adb của
  app) và *Diệt adb server* (diệt mọi adb rồi khởi động lại).
- **Tài khoản**: Free tối đa 40 máy; VIP đăng nhập tài khoản kích hoạt (mỗi máy tính một key), chạy offline tới hết hạn.
- **7 ngôn ngữ**: Tiếng Việt, English, 中文, 日本語, 한국어, ไทย, Português.

### Ổn định khi nhiều máy

- App mở cửa sổ và nạp xong thư viện **trước**, rồi mới khởi động adb và kết nối máy.
- Kết nối xếp hàng (4 máy một lúc), cài APK 2 máy một lúc, khởi động video 4 máy một lúc, lệnh shell ngắn tối đa 8
  cùng lúc — adb server không bị dồn nghẽn; máy lỗi được thử lại thưa dần (tới 60 s).
- Ô *Không khởi tạo được*: bấm vào ô để thử lại ngay (tự thử lại sau 60 s).
- Lỗi cục bộ (một máy, một khung vẽ) không làm sập cả app.

### Nhật ký lỗi

Mỗi lần mở app ghi một file `%LOCALAPPDATA%\DaoMaiViewPhone\logs\DaoMaiView-<ngày-giờ>.log` (giữ 20 file mới nhất;
Linux: `~/.local/share/DaoMaiViewPhone/logs/`). Lần chạy trước thoát bất thường thì log mới có dòng cảnh báo kèm
tên log cũ. Gửi file này khi báo lỗi.

### Gói tải

- `DaoMaiView-<ver>.zip` — Windows: `DaoMaiView.exe`, `update.exe`, `daomai-adb\`, DLL FFmpeg. Giải nén đè lên bản cũ.
- `DaoMaiView-<ver>-linux-x86_64.tar.xz` — Linux.
- `SHA256SUMS-v<ver>.txt`. `latest.json` ở nhánh `main` có chữ ký Ed25519; app bỏ qua bản không có chữ ký hợp lệ.

---

## English

A desktop app (Windows, Linux) that mirrors and controls tens to hundreds of Android phones over USB, Wi-Fi, or
through other computers (Multi-PC). Each phone streams its own H.264 over adb; the PC decodes with FFmpeg (GPU when
available).

### Install and update

- **Windows 10/11**: download `DaoMaiView-<version>.zip`, extract to a folder, run `DaoMaiView.exe`. On first
  connect, enable *USB debugging* on the phone and tap *Allow*.
- **Linux x86_64** (glibc ≥ 2.31, X11 / Wayland): extract `DaoMaiView-<version>-linux-x86_64.tar.xz` and run
  `sh native/run.sh`.
- **Auto-update** (Windows): checks on start, downloads in the background, verifies the **digital signature** and
  sha256, replaces files and restarts. Unchanged files are not rewritten; if adb did not change, the adb server
  **keeps running**, so phones stay connected. If the download fails, *Open download page* takes you to Releases.
- **Single instance** per user: launching again brings the running window to the front.

### Mouse and keyboard

Large view: double-click a tile. Small tiles: turn on *Small-screen control* to act directly on tiles.

| Action | Large view | Small tile (control on) |
|---|---|---|
| Left mouse: tap / drag | ✓ | ✓ (also on selected phones) |
| Right mouse | Back | Back (Ctrl + right-click = menu) |
| Mouse wheel | Swipe up / down at the cursor | Swipe up / down (wheel in the gaps to scroll the grid) |
| **Ctrl + wheel** | Zoom in / out (two-finger pinch) | Zoom in / out |
| **Hold Ctrl** | Pins one finger at the cursor until Ctrl is released | Same |
| **Hold Ctrl + drag** | Second finger → real pinch / rotate | Same |
| Ctrl + C / Ctrl + X | Copy / cut the phone's selection to the PC | Goes to the last touched phone |
| Ctrl + V | Paste the PC clipboard into the phone | Same |
| Ctrl + A | Select all on the phone | Phone under the cursor |
| Ctrl + Z / Ctrl + Y | Undo / redo | ✓ |
| Typing | Text (incl. accents), Enter, Backspace, arrows, Home/End, PgUp/PgDn | — |

- Wheel: one notch ≈ 5 % of the screen height; the finger lifts 150 ms after you stop.
- Without a pin, Ctrl + click still multi-selects tiles. The magnifier hides while Ctrl is held.

### Multi-PC — view and control phones attached to other computers

Every PC runs its own DaoMai adb (bundled). A PC has one of two roles:

- **Node** (default): phones are plugged into this PC. The *Multi-PC* tab shows `IP:port` for other PCs.
- **Server**: enter (or *Scan LAN* for) Node addresses. Node phones appear in the grid **as if plugged in locally**:
  video, touch, typing, APK install, file transfer and macros all work.

How it works:

1. The Server's adb keeps the Node list (`server.txt`), polls each Node for its phones and merges them into its own
   list (Node phones get their own `transport_id`, never clashing with local phones).
2. Every command / video stream to a Node phone goes app → Server adb → TCP to the Node adb → phone. Video is still
   encoded on the phone and only crosses two network hops; the Server does not re-encode.
3. **Sharing** (on the Node): share all phones, a subset, or a phone with one specific Server IP. The filter applies
   to every command, not only to listing.
4. **Viewing policy** (on the Node): ideally one encoder per phone. *Yield*: when a Server is watching a phone, the
   Node stops its own video for it; *Always view*; *View off*. Servers report "watching" to Nodes about every 10 s.
5. Mode / list changes apply immediately without restarting adb. If a Node drops, its phones turn grey and come back
   automatically.
6. A Node's **COM port** (Control Box) can be used from a Server when the Server IP is listed in the Node's `allow.txt`.

Exposing a Node to the Internet (WAN):
- Port-forward the Node's adb port on the router.
- **Strongly recommended**: create `allow.txt` (one Server IP per line) in the Node's adb config folder
  (`%LOCALAPPDATA%\DaoMaiViewPhone\adb\`, next to `server.txt`). With this file, every other IP is rejected.
- Admin commands (change Node list, change sharing, kill the server, COM ports, driver install…) **only run from the
  machine itself**, never from the network (DaoMai adb ≥ 6.6.0).
- Safest: connect the PCs over a VPN (WireGuard, Tailscale…) instead of opening ports.

### Other features

- **Grid**: number, name, serial, IP; tags / groups; search, filter; rotate tiles; magnifier; screen-off while
  mirroring; automatic resolution & DPI; DaoMaiIME keyboard auto-installed.
- **Performance**: presets *Many phones / Balanced / Smoothest*; *Ultra stream* (encode at tile size, separate
  encoder for the large view); *On-demand video*; GPU (d3d11va / vaapi) or CPU decoding.
- **Files / APK / text**: bulk APK install (.apk/.xapk/.apkm/.apks, OBB); import, distribute, export files; text
  distribution; multi-phone clipboard; quick phrases; numbered wallpapers.
- **Automation**: record and replay; auto-swipe; multi-phone shell console; app management; proxies.
- **Right-click menu for phones in Recovery**: *Reboot to System*, *Reboot to Download*, *Format data (TWRP)*,
  *Wipe data* (with confirmation).
- **Devices dialog**: adb state per phone, reboot modes, *Restart adb server* (the app's own adb only) and
  *Kill adb server* (kills every adb, then restarts).
- **Accounts**: Free up to 40 phones; VIP signs in to an activation account (one key per computer), works offline
  until expiry.
- **7 languages**: Tiếng Việt, English, 中文, 日本語, 한국어, ไทย, Português.

### Stability with many phones

- The window opens and libraries load **first**; adb and phone connections start afterwards.
- Connections are queued (4 phones at a time), APK installs 2 at a time, video start-up 4 at a time, at most 8 short
  shell commands at once, so the adb server never gets flooded; failing phones are retried with backoff (up to 60 s).
- A *Could not initialize* tile: click it to retry now (it also retries after 60 s).
- A local error (one phone, one frame) no longer crashes the whole app.

### Logs

Each launch writes `%LOCALAPPDATA%\DaoMaiViewPhone\logs\DaoMaiView-<date-time>.log` (newest 20 kept; Linux:
`~/.local/share/DaoMaiViewPhone/logs/`). If the previous run ended abnormally, the new log starts with a warning
naming the old log. Attach it when reporting a bug.

### Downloads

- `DaoMaiView-<ver>.zip` — Windows: `DaoMaiView.exe`, `update.exe`, `daomai-adb\`, FFmpeg DLLs. Extract over the old copy.
- `DaoMaiView-<ver>-linux-x86_64.tar.xz` — Linux.
- `SHA256SUMS-v<ver>.txt`. `latest.json` on `main` is Ed25519-signed; the app ignores updates without a valid signature.
