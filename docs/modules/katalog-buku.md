# Modul Katalog Buku

## Tanggung Jawab

Modul ini mengelola data buku, pencarian katalog, dan **seluruh aturan
perubahan stok**.

## Isi Modul

### Data

Sumber: `raw/02-cara-kerja-teknis.txt` §2 (tabel BUKU).

| Data | Keterangan |
|---|---|
| `id_buku` | Identitas unik buku |
| `isbn` | Nomor ISBN |
| `judul` | Judul buku |
| `penulis` | Nama penulis |
| `stok_total` | Jumlah eksemplar yang dimiliki perpustakaan |
| `stok_tersedia` | Jumlah eksemplar di rak yang boleh dipinjam. Buku yang sedang ditahan untuk reservasi tidak dihitung. |

### Aturan

**Pencarian** (`raw/02` §4, `raw/03` FLOW 2)

- Kata kunci dicocokkan dengan judul, penulis, atau ISBN.
- Hasil pencarian menampilkan `stok_tersedia` setiap buku.
- Pengguna dapat memilih satu buku untuk melihat detailnya.

**Perubahan stok** (definisi tunggal, `raw/02` §5)

| Kejadian | Perubahan `stok_tersedia` | Dipicu oleh |
|---|---|---|
| Buku dipinjam tanpa reservasi | Berkurang 1 | [Peminjaman](peminjaman.md) |
| Buku diambil oleh pemesan reservasi | Tidak berubah (buku sudah tidak dihitung saat ditahan) | [Peminjaman](peminjaman.md) |
| Buku dikembalikan, tidak ada antrean | Bertambah 1 | [Pengembalian dan Denda](pengembalian-denda.md) |
| Buku dikembalikan, ada antrean | Tidak berubah (buku ditahan) | [Pengembalian dan Denda](pengembalian-denda.md) |
| Reservasi dibatalkan, tidak ada antrean berikutnya | Bertambah 1 | [Reservasi](reservasi.md) |
| Reservasi dibatalkan, ada antrean berikutnya | Tidak berubah (buku ditahan untuk pemesan berikutnya) | [Reservasi](reservasi.md) |

Modul lain tidak menghitung stok sendiri. Mereka hanya melaporkan kejadian,
lalu modul ini menerapkan perubahan sesuai tabel di atas.

**Pengelolaan katalog oleh pustakawan** (`raw/03` FLOW 7)

1. **Tambah buku:** pustakawan mengisi ISBN, judul, penulis, dan `stok_total`.
   `stok_tersedia` awal sama dengan `stok_total`.
2. **Ubah buku:** jika `stok_total` diubah, `stok_tersedia` disesuaikan dengan
   selisih perubahannya.
3. **Hapus buku:** ditolak jika buku masih memiliki peminjaman berjalan atau
   reservasi aktif (definisi reservasi aktif ada di
   [Modul Reservasi](reservasi.md)).

## Hubungan dengan Modul Lain

- **Dipanggil oleh** [Modul Peminjaman](peminjaman.md),
  [Modul Pengembalian dan Denda](pengembalian-denda.md), dan
  [Modul Reservasi](reservasi.md) untuk membaca dan mengubah stok.
- **Memanggil** [Modul Peminjaman](peminjaman.md) dan
  [Modul Reservasi](reservasi.md) saat penghapusan buku untuk memeriksa
  transaksi yang masih berjalan.
- **Dibaca oleh** [Modul Laporan](laporan.md) untuk data judul buku.
- Akses pengelolaan dibatasi untuk pustakawan melalui
  [Modul Autentikasi Akun](autentikasi-akun.md).

## Alasan Pengelompokan

Data buku, pencarian, dan stok selalu berubah bersama. Di dokumen mentah,
aturan stok muncul di `raw/02` §5 serta di FLOW 3, 5, dan 6B pada `raw/03`.
Semua aturan itu dikumpulkan di satu tabel di modul ini agar modul transaksi
tidak menyalin perhitungan stok.