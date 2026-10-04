# Modul Laporan

## Tanggung jawab

- Menyusun rekap bulanan secara terjadwal.
- Menyajikan laporan untuk admin dan unduh PDF.

## Isi/data dan aturan

- Proses terjadwal setiap tanggal 1 pukul 01:00.
- Rekap mencakup: jumlah peminjaman bulanan, 10 buku paling sering dipinjam, total denda tercatat.
- Hasil rekap disimpan, lalu dapat dipilih berdasarkan bulan oleh admin.

## Hubungan

- Mengambil agregasi data dari [Peminjaman](./peminjaman.md), [Katalog Buku](./katalog-buku.md), dan [Pengembalian dan Denda](./pengembalian-denda.md).
- Akses antarmuka dibatasi ke peran admin melalui [Autentikasi Akun](./autentikasi-akun.md).

## Alasan pengelompokan

Fungsi pelaporan dipisahkan dari transaksi harian karena bersifat analitik, terjadwal, dan ditujukan khusus untuk kebutuhan manajerial.

## Referensi sumber

- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/04-daftar-fitur.txt`
