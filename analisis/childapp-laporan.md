# Analisis statis childapp.apk

Laporan ini merangkum pemeriksaan statis pada 15 November 2026 untuk membantu pembacaan kode dan penilaian risiko. APK tidak dijalankan dan tidak disertakan dalam repository.

## Identitas

- Sampel: `childapp.apk` dari `Testing_Dropper.apk`.
- SHA-256: `b2ce0457168e3e52df647e5d1eb7f444dbbb5241eb376febab1622261849faee`.
- Paket: `com.whh.premium`; label Testing; versi 3.0.0.0.
- Minimum SDK 21; target SDK 29. Target SDK bukan jaminan kompatibilitas dengan versi Android baru.
- Byte sampel cocok dengan Testing.apk pada proyek Eagle yang diperiksa. Kesamaan dengan source CraxsRAT 7.4 atau integrasi dengan MDMesh belum dibuktikan.

## Temuan utama

1. APK memuat alur inisialisasi, layanan latar belakang, komunikasi dan penerimaan permintaan. Keberadaan kode tidak membuktikan setiap jalur berjalan di perangkat.
2. Jalur pengambilan gambar layar menggunakan MediaProjection dan memerlukan persetujuan sistem yang sesuai. Bagian lain dari alur antarmuka dan jalur cadangan memiliki hubungan dengan Accessibility; hasil tanpa Accessibility belum dibuktikan menyeluruh.
3. Kode terkait Accessibility mencakup pembacaan struktur antarmuka, gestur dan navigasi. Perilaku menghalangi penghapusan yang diamati pengguna tidak membuktikan instalasi sebagai aplikasi sistem atau bertahan setelah factory reset.
4. Deklarasi izin untuk akses data atau sensor tidak membuktikan izin diberikan atau operasi berhasil.
5. Pengiriman, pemuatan, dan keberhasilan plugin saat aplikasi berjalan belum dibuktikan. Tidak ada perintah atau payload yang dijalankan pada pemeriksaan ini.

## Delapan plugin lokal yang diperiksa

| Kelompok | Fungsi yang terlihat secara statis | Batas |
| --- | --- | --- |
| Aplikasi | Informasi dan daftar aplikasi. | Dibatasi visibilitas paket Android. |
| Panggilan | Pembacaan riwayat dan cabang perubahan. | Izin tulis log panggilan tidak ditemukan di manifest child. |
| Kontak | Pembacaan dan cabang perubahan kontak. | Izin tulis kontak tidak ditemukan di manifest child. |
| Berkas | Pengelolaan dan transfer berkas. | Dibatasi izin dan sandbox; ada risiko kehilangan data pada sebagian jalur. |
| Informasi perangkat | Informasi perangkat dan status tertentu. | Hasil bergantung pada izin, API dan versi Android. |
| Mikrofon | Pengolahan audio. | Memerlukan izin dan dukungan lingkungan. |
| SMS | Pembacaan pesan. | Memerlukan izin; tidak membuktikan fungsi kirim atau hapus pada plugin ini. |
| Terminal | Pemanggilan proses. | Berjalan dalam batas hak aplikasi; tidak membuktikan root. |

Tidak ditemukan ketergantungan langsung pada Accessibility dalam pemeriksaan statis kedelapan plugin lokal. Hal itu tidak membuktikan seluruh APK bekerja tanpa Accessibility.

## Batas cakupan dan risiko

Pemeriksaan ini tidak membuktikan persistensi setelah factory reset, keberhasilan pengambilan data, kemampuan pada setiap versi Android, atau operasi semua fitur pada perangkat nyata. Izin sensitif, akses latar belakang, privasi data, dan pengelolaan berkas merupakan risiko yang memerlukan penilaian lebih lanjut.

Identitas server, token, kredensial, dan kode atau berkas sampel yang dapat dijalankan tidak dipublikasikan di sini. Data ini merupakan ringkasan defensif, bukan instruksi pengoperasian.

## Hubungan dengan source MDMesh

Repository ini adalah fork MDMesh. Branch `vps-v0.4.0` menunjuk ke commit `b81d83f505704ad5bf45fc94ecfffa1a92952a73`, sama dengan source MDMesh pada VPS saat diverifikasi 17 November 2026. Child APK tidak dibuktikan sebagai bagian dari MDMesh.
