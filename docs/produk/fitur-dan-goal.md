# Fitur dan Goal Produk

## Daftar fitur implementasi

| Kode | Fitur | Pengguna utama | Ringkasan |
|---|---|---|---|
| F-01 | Registrasi, login, pembekuan akun | Anggota, pustakawan, admin | Registrasi anggota berbasis validasi NIM/NIP; admin dapat membekukan/mengaktifkan akun |
| F-02 | Pencarian katalog | Semua pengguna login | Cari berdasar judul, penulis, ISBN dengan informasi stok tersedia |
| F-03 | Peminjaman buku | Anggota | Peminjaman mandiri setelah cek status keanggotaan, kuota, dan ketersediaan |
| F-04 | Perpanjangan peminjaman | Anggota | Perpanjangan manual dan otomatis |
| F-05 | Pengembalian dan denda | Pustakawan | Hitung denda otomatis saat terlambat dan tandai lunas setelah pembayaran |
| F-06 | Reservasi buku | Anggota, pustakawan | Antrean reservasi dan penahanan buku 2 hari untuk antrean pertama |
| F-07 | Pengelolaan katalog | Pustakawan | Tambah, ubah, hapus buku dengan aturan konsistensi stok |
| F-08 | Laporan bulanan | Admin | Rekap bulanan dan unduh PDF |

## Goal produk

| Kode | Goal | Status sumber | Catatan dokumentasi |
|---|---|---|---|
| G-01 | Anggota bisa mencari buku mandiri | ✅ | Selaras dengan fitur F-02 |
| G-02 | Anggota meminjam mandiri | ✅ | Selaras dengan fitur F-03 |
| G-03 | Peminjam dapat memperpanjang tanpa hadir fisik | ✅ | Selaras, namun aturan otomatis belum rinci |
| G-04 | Denda otomatis dan akurat | ✅ | Selaras dengan F-05 |
| G-05 | Antrean reservasi adil | ✅ | Selaras dengan F-06 |
| G-06 | Pustakawan kelola katalog mandiri | ✅ | Selaras dengan F-07 |
| G-07 | Admin mendapat laporan bulanan | ✅ | Selaras dengan F-08 |
| G-08 | Notifikasi email sebelum jatuh tempo | ✅ | Perlu spesifikasi jadwal/kondisi pengiriman |
| G-09 | Pembayaran denda online | ✅ | Bertentangan dengan aturan operasional tunai saat ini |

## Konsolidasi keputusan dari isu dokumentasi

- Istilah baku: **anggota**; **peminjam** bersifat kontekstual.
- Masa pinjam acuan: **7 hari**; angka 14 hari dicatat sebagai inkonsistensi sumber.
- Kuota pinjam acuan: **3 buku**; angka 5 buku dicatat sebagai inkonsistensi sumber.
- Pembayaran denda terdokumentasi saat ini: **tunai**, sedangkan opsi online dicatat sebagai target yang perlu klarifikasi.
- Perpanjangan otomatis dan notifikasi email dianggap tersedia sebagai kemampuan, tetapi aturan rinci belum lengkap.

## Referensi sumber

- `../../raw/04-daftar-fitur.txt`
- `../../raw/05-goal.txt`
- `../../raw/01-deskripsi-produk.txt`
- `../../raw/03-flow-aplikasi.txt`
