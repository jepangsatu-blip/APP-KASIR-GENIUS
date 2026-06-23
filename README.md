# KasirKu — Sistem Kasir & Service HP (PWA)

Aplikasi kasir digital offline-first untuk UMKM, bisa diinstall sebagai PWA (Progressive Web App) di HP maupun laptop.

## 📁 Isi Folder
```
index.html       -> Halaman utama aplikasi
manifest.json     -> Konfigurasi PWA (nama, ikon, warna tema)
sw.js              -> Service Worker untuk mode offline
icon-192.png      -> Ikon aplikasi 192x192
icon-512.png      -> Ikon aplikasi 512x512
```
Semua file **wajib berada di folder yang sama** (jangan dipisah ke subfolder), karena saling memanggil dengan path relatif (`./`).

## 🚀 Cara Upload & Deploy ke GitHub Pages

1. Buat repository baru di GitHub (boleh publik), misal: `kasirku`.
2. Upload ke-5 file di atas ke root repository tersebut (drag & drop lewat web GitHub, atau via git push).
3. Masuk ke **Settings → Pages** pada repository.
4. Di bagian **Build and deployment**:
   - Source: `Deploy from a branch`
   - Branch: `main` (atau `master`), folder `/ (root)`
5. Klik **Save**, tunggu 1–2 menit.
6. Aplikasi akan aktif di:
   ```
   https://<username-github-anda>.github.io/kasirku/
   ```
7. Buka link tersebut di HP → menu browser → **"Tambahkan ke Layar Utama" / "Install App"** untuk memasangnya seperti aplikasi native.

## ✅ Yang Sudah Disesuaikan
- `index.html` sudah dihubungkan ke `manifest.json` dan ikon (`<link rel="manifest">`, `<link rel="icon">`, `apple-touch-icon`).
- Service worker bawaan (inline/Blob) yang lama **diganti** agar memanggil file `sw.js` asli — sebelumnya ada dua service worker yang tidak nyambung satu sama lain.
- Semua path file memakai format relatif (`./`), jadi aman dipakai di subfolder GitHub Pages (`username.github.io/nama-repo/`) maupun custom domain.
- Meta tag tambahan untuk tampilan PWA di iOS/Android (`theme-color`, `apple-mobile-web-app-capable`, dll).

## ℹ️ Catatan tentang Fitur Google Sheets Sync
Fitur sinkronisasi ke Google Sheets memakai OAuth dan akan otomatis mengarah ke alamat domain tempat aplikasi dibuka — jadi tidak perlu diubah manual di kode. Namun jika Anda ingin mengaktifkan fitur ini:
1. Buat **OAuth Client ID** di [Google Cloud Console](https://console.cloud.google.com/apis/credentials).
2. Pada **Authorized JavaScript origins** dan **Authorized redirect URIs**, tambahkan alamat GitHub Pages Anda, contoh:
   ```
   https://<username-github-anda>.github.io
   ```
3. Masukkan Client ID tersebut di menu **Admin & Settings** pada aplikasi.

Data transaksi & katalog tetap tersimpan secara lokal (localStorage) di browser meskipun fitur Google Sheets tidak diaktifkan.
