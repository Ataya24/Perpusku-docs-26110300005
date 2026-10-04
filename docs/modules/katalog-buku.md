# Modul Katalog Buku

## Tanggung jawab

- Menyimpan dan menampilkan data buku.
- Menangani operasi tambah, ubah, hapus buku.
- Menjaga konsistensi `stok_total` dan `stok_tersedia`.

## Isi/data dan aturan

- Data buku: ISBN, judul, penulis, stok total, stok tersedia.
- Pencarian memakai judul, penulis, atau ISBN.
- Buku tidak boleh dihapus jika masih ada peminjaman berjalan atau reservasi aktif.
- Aturan stok saat pinjam/kembali/reservasi mengikuti modul transaksi terkait.

## Hubungan

- Dipakai oleh [Peminjaman](./peminjaman.md), [Pengembalian dan Denda](./pengembalian-denda.md), dan [Reservasi](./reservasi.md).
- Menjadi sumber agregasi untuk [Laporan](./laporan.md).

## Alasan pengelompokan

Seluruh aturan data koleksi dipusatkan pada satu modul agar perubahan data bibliografis dan stok tidak tersebar.

## Referensi sumber

- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/04-daftar-fitur.txt`
