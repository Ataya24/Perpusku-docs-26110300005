# Peta Modul PerpusKu

Dokumentasi PerpusKu dibagi menjadi tujuh modul berdasarkan tanggung jawab
utama masing-masing. Setiap aturan didefinisikan **satu kali** di modul
pemiliknya. Modul lain cukup merujuk ke sana dan tidak menulis ulang aturannya.

## Daftar Modul

| Modul | Tanggung jawab utama |
|---|---|
| [Autentikasi Akun](autentikasi-akun.md) | Registrasi, login, peran, status akun, dan definisi keanggotaan aktif |
| [Integrasi Akademik](integrasi-akademik.md) | Pembacaan NIM/NIP dan masa berlaku dari data akademik kampus |
| [Katalog Buku](katalog-buku.md) | Data buku, pencarian, dan seluruh aturan perubahan stok |
| [Peminjaman](peminjaman.md) | Peminjaman dan perpanjangan |
| [Pengembalian dan Denda](pengembalian-denda.md) | Pengembalian, rumus denda, dan pembayaran |
| [Reservasi](reservasi.md) | Antrean, penahanan buku, dan status reservasi |
| [Laporan](laporan.md) | Rekap bulanan dan unduhan PDF |

## Pemilik Aturan

Aturan berikut muncul berulang di dokumen mentah. Di dokumentasi ini,
masing-masing hanya didefinisikan di satu modul.

| Aturan | Muncul di dokumen mentah | Didefinisikan di |
|---|---|---|
| Keanggotaan aktif | `raw/01` §4, `raw/02` §3, `raw/03` FLOW 3, 4A, 6A | [Autentikasi Akun](autentikasi-akun.md#aturan) |
| Perubahan stok | `raw/02` §5, `raw/03` FLOW 3, 5, 6B | [Katalog Buku](katalog-buku.md#aturan) |
| Tarif dan rumus denda | `raw/01` §4, `raw/02` §6, `raw/03` FLOW 4A, 5 | [Pengembalian dan Denda](pengembalian-denda.md#aturan-denda-definisi-tunggal) |
| Menahan buku untuk antrean (2 hari) | `raw/01` §4, `raw/03` FLOW 5, 6B, `raw/04` F-06 | [Reservasi](reservasi.md#aturan) |
| Masa pinjam, kuota, dan batas perpanjangan | `raw/01` §4, `raw/03` FLOW 3, 4A | [Peminjaman](peminjaman.md#nilai-aturan) |

## Hubungan Antar Modul

### Siapa Memanggil Siapa

| Pemanggil | Dipanggil | Untuk apa |
|---|---|---|
| Autentikasi Akun | Integrasi Akademik | Mencocokkan NIM/NIP dan mengambil masa berlaku saat registrasi |
| Peminjaman | Autentikasi Akun | Memeriksa keanggotaan aktif |
| Peminjaman | Katalog Buku | Membaca dan mengubah stok |
| Peminjaman | Reservasi | Memeriksa reservasi `siap_diambil`, menyelesaikannya, dan memeriksa antrean saat perpanjangan |
| Peminjaman | Pengembalian dan Denda | Memeriksa denda saat perpanjangan |
| Pengembalian dan Denda | Peminjaman | Mencari transaksi berjalan dan mengisi tanggal kembali |
| Pengembalian dan Denda | Reservasi | Menahan buku jika ada antrean |
| Pengembalian dan Denda | Katalog Buku | Mengubah stok |
| Reservasi | Autentikasi Akun | Memeriksa keanggotaan aktif |
| Reservasi | Katalog Buku | Membaca dan mengubah stok |
| Katalog Buku | Peminjaman, Reservasi | Memeriksa transaksi aktif sebelum buku dihapus |
| Laporan | Peminjaman, Pengembalian dan Denda, Katalog Buku | Membaca data untuk rekap (tanpa mengubah) |

Peran dari Modul Autentikasi Akun juga membatasi akses ke Katalog Buku
(pustakawan), Pengembalian dan Denda (pustakawan), dan Laporan (admin).

### Lapisan Modul

1. **Lapisan pelaporan:** Laporan (hanya membaca data dari lapisan transaksi
   dan data dasar).
2. **Lapisan transaksi:** Peminjaman, Pengembalian dan Denda, Reservasi
   (saling memanggil sesuai tabel di atas).
3. **Lapisan data dasar:** Autentikasi Akun dan Katalog Buku (dipanggil oleh
   lapisan transaksi).
4. **Lapisan sumber eksternal:** Integrasi Akademik (hanya dipanggil oleh
   Autentikasi Akun).

Modul di lapisan bawah tidak bergantung pada aturan modul di lapisan atas,
kecuali Katalog Buku yang memeriksa transaksi aktif sebelum buku dihapus.

## Alasan Pengelompokan

Modul dipisahkan berdasarkan data dan aturan yang berubah bersama. Setiap modul
memiliki satu tabel utama dari `raw/02` §2: AKUN (Autentikasi Akun), BUKU
(Katalog Buku), PEMINJAMAN (Peminjaman), DENDA (Pengembalian dan Denda), dan
RESERVASI (Reservasi). Integrasi Akademik dipisah karena membaca sistem di luar
PerpusKu. Laporan dipisah karena hanya membaca data dan berjalan terjadwal.

## Dampak Perubahan Modul

**Contoh:** perpustakaan menaikkan tarif denda dari Rp1.000 menjadi Rp2.000 per
hari.

- Yang diubah hanya satu baris di
  [Pengembalian dan Denda](pengembalian-denda.md#aturan-denda-definisi-tunggal).
- Perpanjangan di [Peminjaman](peminjaman.md) ikut memakai tarif baru untuk
  denda berjalan, karena hanya merujuk ke aturan tersebut.
- [Laporan](laporan.md) otomatis menjumlahkan denda dengan nilai baru.

Di dokumen mentah, perubahan yang sama harus dilakukan di tiga tempat
(`raw/01` §4, `raw/03` FLOW 4A, dan FLOW 5). Jika salah satu terlewat,
dokumentasi akan saling bertentangan.