# Ringkasan Modul PerpusKu

Dokumentasi ini memecah PerpusKu menjadi modul fungsional agar aturan tidak ditulis berulang dan alur antarbagian mudah ditelusuri.

## Daftar modul

1. [Autentikasi Akun](./autentikasi-akun.md)
2. [Integrasi Akademik](./integrasi-akademik.md)
3. [Katalog Buku](./katalog-buku.md)
4. [Peminjaman](./peminjaman.md)
5. [Perpanjangan](./perpanjangan.md)
6. [Pengembalian dan Denda](./pengembalian-denda.md)
7. [Reservasi](./reservasi.md)
8. [Laporan](./laporan.md)
9. [Notifikasi](./notifikasi.md)

## Peta hubungan antar modul

- **Autentikasi Akun** memakai **Integrasi Akademik** saat registrasi anggota.
- **Peminjaman**, **Perpanjangan**, dan **Reservasi** bergantung pada status akun dari **Autentikasi Akun**.
- **Peminjaman**, **Pengembalian dan Denda**, **Reservasi**, serta **Katalog Buku** berbagi aturan stok buku.
- **Perpanjangan** memakai data dari **Peminjaman**, **Reservasi**, dan status denda dari **Pengembalian dan Denda**.
- **Laporan** mengambil rekap dari transaksi pada modul operasional.
- **Notifikasi** membaca jadwal/peristiwa dari **Peminjaman**, **Perpanjangan**, dan **Reservasi** (detail trigger masih perlu spesifikasi).

## Contoh dampak perubahan modul

Jika aturan status keanggotaan aktif pada modul **Autentikasi Akun** diubah, maka validasi di modul **Peminjaman**, **Perpanjangan**, dan **Reservasi** ikut berubah. Dampaknya langsung ke izin transaksi dan potensi penolakan layanan anggota.

## Referensi sumber

- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
