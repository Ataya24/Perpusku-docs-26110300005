# Modul Peminjaman

## Tanggung jawab

- Memproses transaksi pinjam buku oleh anggota.
- Menetapkan tanggal pinjam dan jatuh tempo.
- Mencatat relasi pinjam terhadap anggota dan buku.

## Isi/data dan aturan

- Data peminjaman: `id_peminjaman`, `id_member` (nama field sumber), `id_buku`, tanggal pinjam, tanggal jatuh tempo, jumlah perpanjangan.
- Syarat peminjaman: anggota aktif, kuota belum penuh, stok tersedia atau ada reservasi `siap_diambil` milik anggota.

### Aturan operasional yang dipakai dokumentasi

- Masa pinjam acuan: **7 hari**.
- Kuota acuan: **maksimal 3 buku**.
- Jika peminjaman berasal dari reservasi `siap_diambil`, status reservasi diubah menjadi `selesai`.

### Inkonsistensi sumber yang dicatat

- Flow mentah menulis jatuh tempo `+14 hari`.
- Flow mentah menulis batas kuota `5 buku`.
- Dokumen ini tetap memakai 7 hari dan 3 buku sebagai keputusan kerja, sambil menandai kebutuhan klarifikasi lanjutan.

### Kaitan langsung dengan isu

- Isu [#8](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/8): konsolidasi istilah anggota/peminjam.
- Isu [#9](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/9): keputusan masa pinjam 7 hari.
- Isu [#10](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/10): keputusan kuota 3 buku.

## Hubungan

- Bergantung pada [Autentikasi Akun](./autentikasi-akun.md) untuk status anggota.
- Membaca/menulis stok melalui [Katalog Buku](./katalog-buku.md).
- Berinteraksi dengan [Reservasi](./reservasi.md) saat peminjaman dari antrean siap ambil.
- Menjadi dasar proses [Perpanjangan](./perpanjangan.md) dan [Pengembalian dan Denda](./pengembalian-denda.md).
- Menjadi salah satu sumber event pada [Notifikasi](./notifikasi.md) (pengingat jatuh tempo).

## Alasan pengelompokan

Seluruh aturan pembentukan transaksi pinjam diletakkan di satu modul agar definisi jatuh tempo, kuota, dan validasi awal tidak berulang.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/04-daftar-fitur.txt`
