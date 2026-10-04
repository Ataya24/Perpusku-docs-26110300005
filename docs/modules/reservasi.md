# Modul Reservasi

## Tanggung jawab

- Mengelola antrean pemesanan buku saat stok habis.
- Menetapkan status reservasi dan batas ambil.
- Menangani pembatalan reservasi kedaluwarsa.

## Isi/data dan aturan

- Reservasi hanya boleh dibuat jika `stok_tersedia` = 0.
- Anggota tidak boleh memiliki duplikasi reservasi menunggu untuk buku yang sama.
- Urutan antrean berdasarkan waktu reservasi (`waktu_reservasi`).
- Saat buku kembali: antrean terdepan menjadi `siap_diambil` dengan `batas_ambil` +2 hari.
- Jika lewat batas ambil: reservasi dibatalkan, lalu dialihkan ke antrean berikutnya atau stok dikembalikan.

## Hubungan

- Bergantung pada status anggota dari [Autentikasi Akun](./autentikasi-akun.md).
- Bergantung pada data buku dari [Katalog Buku](./katalog-buku.md).
- Beririsan proses dengan [Peminjaman](./peminjaman.md) dan [Pengembalian dan Denda](./pengembalian-denda.md).
- Menjadi salah satu sumber event untuk [Notifikasi](./notifikasi.md).

## Alasan pengelompokan

Aturan antrean dan status reservasi dipusatkan agar kebijakan fair queue tidak tersebar ke banyak modul.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/04-daftar-fitur.txt`
