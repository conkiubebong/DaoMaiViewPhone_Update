# DaoMaiViewPhone_Update

Kênh cập nhật của **Dao Mai View Phone** (bản native `DaoMaiView.exe`). App đọc `latest.json` ở nhánh
`main` khi mở, có bản mới thì tải gói từ mục **Releases** của repo này và tự thay thế bằng `update.exe`.

- `latest.json` — bản mới nhất: `version`, `build`, `url` (link asset trong Releases), `sha256`, `size`, `notes`, `min_build`.
- Gói nằm ở [Releases](https://github.com/conkiubebong/DaoMaiViewPhone_Update/releases), tag `v<phiên bản>`:
  - `DaoMaiView-<ver>.zip` — Windows: `DaoMaiView.exe`, `update.exe`, `daomai.apk`, `daomai-adb\` (adb DaoMai + 2 DLL), (`*.dll` FFmpeg khi là gói đầy đủ).
  - `DaoMaiView-<ver>-linux-x86_64.tar.xz` — Linux (từ 1.0.4; 1.0.5 kèm adb DaoMai 6.3.0): `DaoMaiView`, 4 lib FFmpeg,
    `daomai.apk`, `daomai-adb/adb`, `run.sh`. Giải nén rồi `sh native/run.sh`; cần glibc ≥ 2.31, X11/Wayland, GL.
    Bản Linux chưa tự cập nhật (tải tay).
  - `SHA256SUMS-v<ver>.txt`.

Phát hành từ repo nguồn: `tools\release_native.ps1 -Build N -Notes "..." [-WithDlls] -Push` (xem `docs/UPDATE.md`).
