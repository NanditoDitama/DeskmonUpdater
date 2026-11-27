# Deskmon Updater

Repository resmi untuk distribusi installer dan pembaruan otomatis (*auto-updater*) aplikasi **Deskmon** lintas platform (**Windows**, **macOS**, dan **Linux**).

## Struktur Repository

- **`version.json`** (branch `main`) — Manifest versi terbaru yang dicek otomatis oleh aplikasi Deskmon saat dibuka:
  ```text
  https://raw.githubusercontent.com/NanditoDitama/DeskmonUpdater/main/version.json
  ```
- **[GitHub Releases](https://github.com/NanditoDitama/DeskmonUpdater/releases)** — Penyimpanan file installer awal dan arsip pembaruan per OS:
  - **Windows**: `Deskmon-Setup-<version>.exe` (installer) & `Deskmon-<version>-win64.zip` (auto-update)
  - **macOS**: `Deskmon-<version>-macos.dmg` (installer) & `Deskmon-<version>-macos.zip` (auto-update)
  - **Linux**: `Deskmon-<version>-amd64.deb` (installer) & `Deskmon-<version>-linux-x64.tar.gz` (auto-update)

## Format `version.json`

```json
{
  "version": "2.0.1.0",
  "releaseNotes": "- Perbaikan bug dan peningkatan stabilitas\n- Peningkatan fitur auto-updater",
  "releasePageUrl": "https://github.com/NanditoDitama/DeskmonUpdater/releases",
  "platforms": {
    "windows-x64": {
      "url": "https://github.com/NanditoDitama/DeskmonUpdater/releases/download/v2.0.1.0/Deskmon-2.0.1.0-win64.zip",
      "sha256": "<sha256-win64-zip>",
      "type": "zip"
    },
    "macos-universal": {
      "url": "https://github.com/NanditoDitama/DeskmonUpdater/releases/download/v2.0.1.0/Deskmon-2.0.1.0-macos.zip",
      "sha256": "<sha256-macos-zip>",
      "type": "zip"
    },
    "linux-x64": {
      "url": "https://github.com/NanditoDitama/DeskmonUpdater/releases/download/v2.0.1.0/Deskmon-2.0.1.0-linux-x64.tar.gz",
      "sha256": "<sha256-linux-tar-gz>",
      "type": "tar.gz"
    }
  }
}
```

> Platform yang belum tersedia pada suatu rilis boleh tidak dicantumkan sementara di `platforms`; aplikasi akan otomatis menampilkan tautan halaman Releases untuk OS tersebut.

## Alur Rilis Update Baru

1. Naikkan nomor versi di `CMakeLists.txt` pada repository utama aplikasi Deskmon.
2. Build paket rilis sesuai OS:
   - **Windows**: jalankan `package_installer.bat`
   - **macOS**: jalankan `bash installer/package_mac.sh`
   - **Linux**: jalankan `bash installer/package_linux.sh`
3. Buat **Release** baru di repository ini dengan tag `v<version>`, lalu unggah file `.zip` / `.tar.gz` (dan installer `.exe` / `.dmg` / `.deb`) pada bagian **Attach binaries**.
4. Perbarui file **`version.json`** di branch `main` dengan versi, `releaseNotes`, URL aset Release, dan checksum `sha256` yang sesuai.# DeskmonUpdater
