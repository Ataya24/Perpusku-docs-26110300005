# Modul Peminjaman

## Tanggung jawab

- Memproses transaksi pinjam buku oleh anggota.
- Menetapkan tanggal pinjam dan jatuh tempo.
- Mencatat relasi pinjam terhadap anggota dan buku.

## Isi/data dan aturan

- Data peminjaman: `id_peminjaman`, `id_member` (nama field sumber), `id_buku`, tanggal pinjam, tanggal jatuh tempo, jumlah perpanjangan.
- Syarat peminjaman: anggota aktif, kuota belum penuh, stok tersedia atau ada reservasi `siap_diambil` milik anggota.
- Aturan dokumentasi utama:
  - masa pinjam 7 hari,
  - kuota maksimal 3 buku.
- Inkonstistensi sumber yang dicatat:
  - flow mentah menulis jatuh tempo +14 hari,
  - flow mentah menulis kuota 5 buku.

## Hubungan

- Bergantung pada [Autentikasi Akun](./autentikasi-akun.md) untuk status anggota.
- Membaca/menulis stok melalui [Katalog Buku](./katalog-buku.md).
- Berinteraksi dengan [Reservasi](./reservasi.md) saat peminjaman dari antrean siap ambil.
- Menjadi dasar proses [Perpanjangan](./perpanjangan.md) dan [Pengembalian dan Denda](./pengembalian-denda.md).

## Alasan pengelompokan

Seluruh aturan pembentukan transaksi pinjam diletakkan di satu modul agar definisi jatuh tempo, kuota, dan validasi awal tidak berulang.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
