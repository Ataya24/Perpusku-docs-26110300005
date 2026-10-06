# Modul Laporan

## Tanggung Jawab

Modul ini menyusun rekap kegiatan perpustakaan setiap bulan dan menyediakan
laporan untuk dilihat atau diunduh oleh admin.

## Isi Modul

### Data Rekap

Sumber: `raw/02-cara-kerja-teknis.txt` §7 dan `raw/03-flow-aplikasi.txt`
FLOW 8.

| Isi rekap | Sumber data |
|---|---|
| Jumlah peminjaman bulan sebelumnya | [Modul Peminjaman](peminjaman.md) |
| 10 buku yang paling sering dipinjam | [Modul Peminjaman](peminjaman.md) dan [Modul Katalog Buku](katalog-buku.md) |
| Total denda yang tercatat pada bulan tersebut | [Modul Pengembalian dan Denda](pengembalian-denda.md) |

### Aturan

**Penyusunan rekap** (terjadwal)

1. Pekerjaan terjadwal berjalan setiap tanggal 1 pukul 01:00.
2. Hitung jumlah peminjaman bulan sebelumnya.
3. Tentukan 10 buku yang paling sering dipinjam.
4. Jumlahkan denda yang tercatat pada bulan tersebut.
5. Simpan hasil rekap di basis data.

**Melihat laporan** (pelaku: admin)

1. Admin membuka halaman Laporan dan memilih bulan.
2. Sistem menampilkan rekap bulan tersebut.
3. Jika admin menekan "Unduh", sistem memberikan file PDF.

## Hubungan dengan Modul Lain

- **Membaca** data dari [Modul Peminjaman](peminjaman.md),
  [Modul Pengembalian dan Denda](pengembalian-denda.md), dan
  [Modul Katalog Buku](katalog-buku.md). Modul ini tidak mengubah data modul
  lain.
- Akses dibatasi untuk admin melalui
  [Modul Autentikasi Akun](autentikasi-akun.md).

## Alasan Pengelompokan

Penyusunan rekap berjalan terjadwal dan dipakai oleh admin, berbeda dari
transaksi harian anggota dan pustakawan. Modul ini hanya membaca data, sehingga
aturan periode laporan dan format PDF tidak bercampur dengan aturan transaksi.