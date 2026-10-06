# Modul Autentikasi Akun

## Tanggung Jawab

Modul ini mengelola registrasi anggota, login semua pengguna, peran akun,
status akun, pembekuan atau pengaktifan kembali akun anggota, serta
pemeriksaan **keanggotaan aktif** yang dipakai modul lain.

## Isi Modul

### Data

Sumber: `raw/02-cara-kerja-teknis.txt` §2 (tabel AKUN).

| Data | Keterangan |
|---|---|
| `id_user` | Identitas unik akun |
| `nim_nip` | NIM untuk mahasiswa, NIP untuk dosen |
| `nama` | Nama pemilik akun |
| `kata_sandi` | Disimpan terenkripsi, tidak pernah berupa teks asli |
| `peran` | `anggota`, `pustakawan`, atau `admin` |
| `status` | `aktif` atau `dibekukan` |
| `masa_berlaku` | Tanggal akhir keanggotaan, hanya terisi untuk anggota |

> Tabel AKUN tidak memiliki kolom email. Lihat catatan goal notifikasi email
> pada dokumen fitur dan goal produk.

### Aturan

**Registrasi** (`raw/03` FLOW 1A)

1. Calon anggota mengisi NIM/NIP, nama, dan kata sandi.
2. NIM/NIP dicocokkan melalui [Modul Integrasi Akademik](integrasi-akademik.md).
   Jika tidak ditemukan, registrasi ditolak.
3. Jika NIM/NIP sudah memiliki akun, registrasi ditolak.
4. Akun baru disimpan dengan `peran = anggota`, `status = aktif`, dan
   `masa_berlaku` dari Modul Integrasi Akademik.

**Login dan hak akses** (`raw/02` §3, `raw/03` FLOW 1B)

- Semua pengguna login menggunakan NIM/NIP dan kata sandi.
- Menu yang tampil ditentukan oleh peran akun.
- Anggota hanya dapat melihat data miliknya sendiri.
- Akun pustakawan dan admin dibuat langsung di basis data oleh pengelola
  infrastruktur kampus, bukan melalui aplikasi.

**Pembekuan akun** (`raw/03` FLOW 1C)

- Admin dapat membekukan atau mengaktifkan kembali akun anggota.

**Keanggotaan aktif** (definisi tunggal, `raw/01` §4 dan `raw/02` §3)

Anggota dianggap **aktif** jika kedua syarat terpenuhi:

1. `masa_berlaku` belum lewat dari tanggal hari ini, dan
2. `status` akun bukan `dibekukan`.

Status kedaluwarsa tidak disimpan, tetapi dihitung setiap kali pemeriksaan
dilakukan. Modul lain **tidak mendefinisikan ulang** aturan ini, tetapi cukup
merujuk ke bagian ini.

## Hubungan dengan Modul Lain

- **Memanggil** [Modul Integrasi Akademik](integrasi-akademik.md) saat
  registrasi.
- **Dipanggil oleh** [Modul Peminjaman](peminjaman.md) dan
  [Modul Reservasi](reservasi.md) untuk pemeriksaan keanggotaan aktif.
- **Menyediakan peran** untuk membatasi akses ke
  [Modul Katalog Buku](katalog-buku.md),
  [Modul Pengembalian dan Denda](pengembalian-denda.md), dan
  [Modul Laporan](laporan.md).

## Alasan Pengelompokan

Registrasi, login, peran, dan status akun sama-sama menentukan siapa yang boleh
mengakses sistem. Definisi keanggotaan aktif ditempatkan di modul ini karena
datanya (`status` dan `masa_berlaku`) disimpan pada akun. Dengan begitu,
peminjaman, perpanjangan, dan reservasi memakai pemeriksaan yang sama tanpa
versi yang berbeda-beda seperti pada `raw/03` (FLOW 3, 4A, dan 6A menuliskannya
dengan kalimat yang berbeda).