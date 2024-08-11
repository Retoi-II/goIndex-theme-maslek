<!-- # GoIndex-theme-maslek -->
# Go-Index (Google Drive Index)


demo: [Maslek DDL](https://test.maslek.workers.dev/0:/)


# Instruksi Instalasi

## Inisialisasi Cloudflare Workers

1. Siapkan akun cloudflare dan buka [Dashboard Cloudflare](https://dash.cloudflare.com/).
2. Buka dropdown Workers & Pages lalu pilih Overview > Create Worker.
3. Buat subdomain level 2 untuk situs yang ingin dibuat (subdomain level 1 bisa di-adjust di halaman workers), klik deploy.
4. Continue to project > pilih tab Metrics > Edit Code.

## Inisialisasi Google Drive API

1. Enable [Google Drive API](https://console.cloud.google.com/marketplace/product/google/drive.googleapis.com?q=search&referrer=search&authuser=4&supportedpurview=project).
2. Create Credential.
    - Credential Type:
        - Select an API: Google Drive API.
        - What data will you be accessing: User Data.
    - OAuth Client ID 
        - Application type: Web Application.
        - Authorized redirect URIs: `https://{subdomainlv2}.{subdomain}.workers.dev`, kalau ingin modifikasi subdomain maka kembali ke halaman overview > change subdomain.
3. Create > Done.
4. Buka Tab Credential > klik pada App Name.
5. Buka OAuth consent screen (lihat di bawah App Name).
6. Pada bagian Testing, klik Publish App.
7. Buka link ini di browser, isi dengan Client ID dan Redirect URI.
```bash
https://accounts.google.com/o/oauth2/v2/auth?client_id=YOUR_CLIENT_ID&redirect_uri=YOUR_REDIRECT_URI&response_type=code&scope=https://www.googleapis.com/auth/drive&access_type=offline&prompt=consent
```
8. Sign in dengan akun google yang digunakan, izinkan API.
9. Kalau tampil halaman tidak ditemukan itu normal, kita akan fokus ke url untuk mengambil Refresh Token, ini contohnya:
```bash
https://ddl.lexsz.workers.dev/?code=4/0AcvDMr...u3g&scope=https://www.googleapis.com/auth/drive
```
10. Simpan token, yaitu `bash4/0AcvDMr...u3g` di notepad atau clipboard.

## Deploy Aplikasi di Cloudflare Workers

1. Buka editor kode Cloudflare Workers, lalu masukkan kode [index.js](https://github.com/5MayRain/goIndex-theme-nexmoe/blob/master/dist/index.js).
2. Beberapa identifier yang perlu diperhatikan:
    - `siteName` : nama situs.
    - `siteIcon` : favicon situs.
    - `client_id` : diambil dari tab credential GD API.
    - `client_secret` : diambil dari tab credential GD API.
    - `refresh_token` : kode yang sudah disimpan tadi.
    - `roots` : folder yang mau di-index, default: root.
3. Kalau ingin memodifikasi situs lebih dalam lagi maka direkomendasikan menggunakan file dalam repositori ini karena sudah berbahasa indonesia dan siapkan CDN tentunya.
4. Bagi yang ingin modifikasi, perhatikan fungsi ```themeConfig``` pada baris 72.
    - `url` : dipakai untuk mengambil resource situs, CDN digunakan menyimpan situs modifikasi dan simpan url dalam identifier.
    - `theme` : memilih tema, "light" dan "dark".
    - `avatar` : foto profil di kiri atas halaman.
    - `bimg` : background image.
5. Untuk modifikasi situs buka folder `dist/themes/` lalu pilih "light" atau "dark" dan modifikasi pada file `app.js`. Jangan lupa untuk mengkonversinya menjadi `app.min.js` setelah selesai melakukan modifikasi.
6. Happy modding, bisa digunakan juga untuk semua template yang tersedia.

# Credit

original repository: [5MayRain/goIndex-theme-nexmoe](https://github.com/5MayRain/goIndex-theme-nexmoe/tree/master)

...
