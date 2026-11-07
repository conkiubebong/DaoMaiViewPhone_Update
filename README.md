# DaoMaiViewPhone_Update

Kênh cập nhật của **Dao Mai View Phone** (bản native `DaoMaiView.exe`). App đọc `latest.json` ở nhánh
`main` khi mở, có bản mới thì tải gói trong `releases/<phiên bản>/` và tự thay thế bằng `update.exe`.

- `latest.json` — bản mới nhất: `version`, `build`, `url`, `sha256`, `size`, `notes`, `min_build`.
- `releases/<ver>/DaoMaiView-<ver>.zip` — `DaoMaiView.exe`, `update.exe`, `daomai.apk` (và `*.dll` FFmpeg khi là gói đầy đủ).
- `releases/<ver>/release.json` — bản sao mô tả của phiên bản đó.
- `releases/<ver>/DaoMaiView-<ver>-linux-x86_64.tar.xz` — bản Linux (từ 1.0.4; 1.0.5 kèm adb DaoMai 6.3.0): `DaoMaiView`, 4 lib FFmpeg,
  `daomai.apk`, `daomai-adb/adb`, `run.sh`. Giải nén rồi `sh native/run.sh`; cần glibc ≥ 2.31, X11/Wayland,
  GL. Bản Linux chưa tự cập nhật (tải tay).

Phát hành từ repo nguồn: `tools\release_native.ps1 -Build N -Notes "..." [-WithDlls] -Push` (xem `docs/UPDATE.md`).
