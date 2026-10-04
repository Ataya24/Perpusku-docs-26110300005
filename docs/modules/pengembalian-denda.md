# Modul Pengembalian dan Denda

## Tanggung jawab

- Memproses pengembalian buku.
- Menghitung keterlambatan dan mencatat denda.
- Mencatat pelunasan denda oleh pustakawan.

## Isi/data dan aturan

- Saat pengembalian: cari transaksi aktif, isi tanggal kembali, hitung hari terlambat.
- Tarif denda: Rp1.000/hari/buku.
- Denda dicatat berstatus `belum_lunas`, lalu diubah jadi `lunas` setelah pembayaran.
- Keputusan dokumentasi saat ini: pembayaran denda dilakukan **tunai** di meja pustakawan.
- Konflik sumber: goal produk menyebut opsi pembayaran online; dicatat sebagai kebutuhan klarifikasi.

## Hubungan

- Mengakhiri transaksi dari [Peminjaman](./peminjaman.md).
- Memperbarui ketersediaan/penahanan stok bersama [Katalog Buku](./katalog-buku.md) dan [Reservasi](./reservasi.md).
- Status denda dipakai [Perpanjangan](./perpanjangan.md) untuk validasi.

## Alasan pengelompokan

Pengembalian dan denda digabung karena keduanya terjadi pada momen transaksi yang sama dan berbagi data keterlambatan serta status pelunasan.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/05-goal.txt`
