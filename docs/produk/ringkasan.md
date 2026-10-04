# Ringkasan Produk PerpusKu

PerpusKu adalah sistem peminjaman buku perpustakaan kampus berbasis web. Sistem ini menggantikan pencatatan manual di buku besar agar pelacakan peminjaman, perhitungan denda, dan pengelolaan layanan perpustakaan lebih akurat.

## Tujuan utama

- Memudahkan anggota mencari buku dan meminjam secara mandiri.
- Menjaga konsistensi aturan peminjaman, perpanjangan, dan pengembalian.
- Membantu pustakawan mengelola katalog, denda, dan reservasi.
- Menyediakan laporan bulanan untuk admin.

## Aktor sistem

- **Anggota**: mahasiswa/dosen yang memiliki akun aktif.
- **Peminjam**: anggota yang sedang memiliki transaksi peminjaman aktif.
- **Pustakawan**: petugas layanan pengembalian, denda, katalog, reservasi.
- **Admin**: pengelola akun anggota dan konsumen laporan bulanan.

## Cakupan fungsi

1. Registrasi, login, pembekuan/aktivasi akun.
2. Pencarian katalog buku.
3. Peminjaman buku.
4. Perpanjangan manual dan otomatis.
5. Pengembalian buku dan perhitungan denda.
6. Reservasi buku.
7. Pengelolaan katalog buku.
8. Laporan bulanan.
9. Notifikasi email (goal, masih perlu spesifikasi rinci).

## Catatan keputusan dokumentasi

- Istilah umum yang dipakai adalah **anggota**.
- Istilah **peminjam** dipakai khusus untuk anggota yang sedang meminjam.
- Nama field **`id_member`** dipertahankan hanya saat merujuk struktur data sumber.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/04-daftar-fitur.txt`
- `../../raw/05-goal.txt`
