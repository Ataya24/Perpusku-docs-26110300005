# Modul Peminjaman

## Tanggung Jawab

Modul ini mengelola pemeriksaan kelayakan peminjaman, pencatatan transaksi
peminjaman, dan perpanjangan masa pinjam.

## Isi Modul

### Data

Sumber: `raw/02-cara-kerja-teknis.txt` §2 (tabel PEMINJAMAN).

| Data | Keterangan |
|---|---|
| `id_peminjaman` | Identitas unik transaksi |
| `id_member` | Anggota yang meminjam |
| `id_buku` | Buku yang dipinjam |
| `tanggal_pinjam` | Tanggal transaksi dibuat |
| `tanggal_jatuh_tempo` | Batas pengembalian |
| `jumlah_perpanjangan` | Dimulai dari 0 |
| `tanggal_kembali` | Kosong selama buku belum dikembalikan |

### Nilai Aturan

| Aturan | Nilai yang dipakai | Catatan |
|---|---|---|
| Masa pinjam | 7 hari | `raw/01` §4. `raw/03` FLOW 3 menulis 14 hari. |
| Kuota pinjam | 3 buku sekaligus | `raw/01` §4. `raw/03` FLOW 3 menulis 5 buku. |
| Batas perpanjangan | 1 kali per peminjaman | `raw/01` §4 dan `raw/03` FLOW 4A |
| Tambahan masa pinjam | 7 hari | `raw/01` §4 dan `raw/03` FLOW 4A |

> [!IMPORTANT]
> Nilai masa pinjam dan kuota adalah **nilai sementara**. `raw/01` dipilih
> karena merupakan dokumen aturan penggunaan produk, dan tambahan perpanjangan
> 7 hari sejalan dengan masa pinjam 7 hari. Nilai pada `raw/03` dicatat sebagai
> perbedaan yang perlu dikonfirmasi ke pembuat dokumen.

### Aturan Peminjaman

Sumber: `raw/03` FLOW 3. Pelaku: anggota.

1. Anggota memindai kode buku di kios layanan mandiri atau ponsel.
2. Periksa **keanggotaan aktif** sesuai
   [Modul Autentikasi Akun](autentikasi-akun.md#aturan). Jika tidak aktif,
   tampilkan "Keanggotaan tidak aktif" dan berhenti.
3. Periksa kuota. Jika anggota sudah mencapai kuota, berhenti.
4. Periksa ketersediaan: `stok_tersedia` lebih dari 0 menurut
   [Modul Katalog Buku](katalog-buku.md), **atau** anggota memiliki reservasi
   `siap_diambil` untuk buku ini menurut [Modul Reservasi](reservasi.md).
   Jika tidak memenuhi, tampilkan "Buku sedang habis", tawarkan reservasi, lalu
   berhenti.
5. Catat peminjaman dengan `tanggal_pinjam` hari ini, `tanggal_jatuh_tempo`
   sesuai masa pinjam, dan `jumlah_perpanjangan = 0`.
6. Laporkan kejadian ke modul terkait:
   - jika berasal dari reservasi, Modul Reservasi menyelesaikan reservasi
     tersebut;
   - perubahan stok diterapkan oleh Modul Katalog Buku sesuai
     [tabel perubahan stok](katalog-buku.md#aturan).
7. Tampilkan bukti peminjaman beserta tanggal jatuh tempo.

### Aturan Perpanjangan Manual

Sumber: `raw/01` §4 dan `raw/03` FLOW 4A. Pelaku: anggota.

1. Anggota membuka halaman Peminjaman Saya dan memilih peminjaman yang sedang
   berjalan.
2. Periksa **keanggotaan aktif** sesuai
   [Modul Autentikasi Akun](autentikasi-akun.md#aturan).
3. Jika `jumlah_perpanjangan` sudah mencapai batas, tolak.
4. Jika ada reservasi `menunggu` untuk buku ini menurut
   [Modul Reservasi](reservasi.md), tolak.
5. Periksa denda melalui
   [Modul Pengembalian dan Denda](pengembalian-denda.md). Perpanjangan ditolak
   jika:
   - anggota memiliki denda berstatus `belum_lunas`, atau
   - anggota memiliki **denda berjalan**, yaitu buku lain yang sudah lewat jatuh
     tempo tetapi belum dikembalikan. Besarnya dihitung dengan tarif yang sama
     seperti di Modul Pengembalian dan Denda.
6. Tambahkan 7 hari pada `tanggal_jatuh_tempo` dan tambah
   `jumlah_perpanjangan` sebanyak 1.
7. Tampilkan tanggal jatuh tempo baru.

> [!NOTE]
> Pemeriksaan denda berjalan (langkah 5 butir kedua) hanya ada di `raw/03`.
> `raw/01` hanya menyebut "anggota tidak memiliki denda". Dokumentasi mengikuti
> flow karena lebih rinci dan tidak bertentangan dengan `raw/01`.

### Perpanjangan Otomatis

Sumber: `raw/03` FLOW 4B dan `raw/04` F-04.

Sumber hanya menyatakan bahwa peminjaman diperpanjang otomatis menjelang jatuh
tempo, satu kali per peminjaman, dan tanggal baru tampil di halaman Peminjaman
Saya. Hal berikut **belum dijelaskan** dan perlu dikonfirmasi:

- kapan tepatnya proses otomatis berjalan;
- apakah perpanjangan otomatis memakai jatah 1 kali perpanjangan yang sama;
- apakah syarat keanggotaan aktif, antrean reservasi, dan denda tetap
  diperiksa;
- apa yang terjadi jika proses gagal dan apakah anggota diberi tahu.

Dokumentasi tidak menambahkan aturan yang tidak ada di sumber.

## Hubungan dengan Modul Lain

- **Memanggil** [Modul Autentikasi Akun](autentikasi-akun.md) untuk
  pemeriksaan keanggotaan aktif.
- **Memanggil** [Modul Katalog Buku](katalog-buku.md) untuk membaca dan
  mengubah stok.
- **Memanggil** [Modul Reservasi](reservasi.md) untuk memeriksa reservasi
  `siap_diambil`, menyelesaikannya, dan memeriksa antrean saat perpanjangan.
- **Memanggil** [Modul Pengembalian dan Denda](pengembalian-denda.md) untuk
  memeriksa denda saat perpanjangan.
- **Dibaca oleh** [Modul Pengembalian dan Denda](pengembalian-denda.md) dan
  [Modul Laporan](laporan.md).

## Alasan Pengelompokan

Peminjaman dan perpanjangan sama-sama mengubah masa pinjam anggota dan disimpan
di tabel PEMINJAMAN. Pengembalian dipisahkan karena pelakunya pustakawan dan
terjadi di akhir transaksi. Pemeriksaan keanggotaan, stok, antrean, dan denda
tidak didefinisikan di sini, tetapi dirujuk ke modul pemiliknya.