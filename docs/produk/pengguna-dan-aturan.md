# Pengguna dan Aturan Produk

## Pengguna

| Pengguna | Peran utama |
|---|---|
| Anggota | Registrasi, login, cari buku, pinjam, perpanjang, reservasi, lihat pinjaman sendiri |
| Pustakawan | Proses pengembalian, kelola denda, kelola katalog, tindak lanjut reservasi |
| Admin | Bekukan/aktifkan akun anggota, lihat dan unduh laporan bulanan |

## Aturan operasional utama

### Status keanggotaan

- Anggota harus **aktif** (masa berlaku belum habis dan tidak dibekukan admin) untuk meminjam, memperpanjang, dan reservasi.

### Masa pinjam

- Keputusan dokumentasi utama: **7 hari** sejak tanggal pinjam.
- Ditemukan inkonsistensi sumber: flow peminjaman menulis jatuh tempo `+14 hari`.
- Status: perlu klarifikasi lanjutan, tetapi dokumentasi ini memakai 7 hari sebagai aturan utama.

### Kuota pinjam

- Keputusan dokumentasi utama: maksimal **3 buku** per anggota.
- Ditemukan inkonsistensi sumber: flow peminjaman menulis batas kuota `5 buku`.
- Status: perlu klarifikasi lanjutan, tetapi dokumentasi ini memakai 3 buku sebagai aturan utama.

### Perpanjangan

- Perpanjangan manual maksimal 1 kali, menambah 7 hari.
- Syarat manual: akun aktif, tidak melewati batas perpanjangan, tidak ada antrean reservasi untuk buku tersebut, dan tidak memiliki denda belum lunas.
- Perpanjangan otomatis disebut tersedia di sumber, tetapi pemicu detail, pengecualian, dan notifikasi belum dirinci.

### Denda

- Denda keterlambatan: Rp1.000/hari/buku.
- Denda dihitung saat pengembalian terlambat.
- Pembayaran denda didokumentasikan sebagai **tunai** melalui pustakawan.

### Pembayaran denda

- Keputusan dokumentasi saat ini: **tunai di meja pustakawan** (sesuai deskripsi produk, teknis, dan flow).
- Konflik sumber: goal menyebut pembayaran denda online.
- Status: keputusan final kanal pembayaran masih butuh klarifikasi pemangku kepentingan.

### Reservasi

- Reservasi hanya untuk buku tanpa stok tersedia.
- Antrean berdasarkan urutan waktu reservasi.
- Buku yang kembali dapat ditahan 2 hari untuk antrean terdepan (`siap_diambil`).

### Notifikasi email

- Notifikasi email sebelum jatuh tempo disebut sebagai goal/fitur.
- Spesifikasi jadwal, kondisi pemicu, dan isi pesan belum dirinci di sumber.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/05-goal.txt`
