# Modul Integrasi Akademik

## Tanggung Jawab

Modul ini membaca data akademik kampus untuk memvalidasi identitas calon
anggota dan menentukan masa berlaku keanggotaannya.

## Isi Modul

### Data

| Data | Keterangan |
|---|---|
| NIM | Nomor induk mahasiswa |
| NIP | Nomor induk dosen |
| Tanggal akhir studi/kontrak | Menjadi `masa_berlaku` pada akun anggota |

### Aturan

Sumber: `raw/02-cara-kerja-teknis.txt` §1 dan `raw/03-flow-aplikasi.txt`
FLOW 1A.

- Data akademik hanya **dibaca**, tidak pernah diubah oleh PerpusKu.
- Modul mengembalikan dua hasil: apakah NIM/NIP ditemukan, dan tanggal akhir
  studi/kontrak pemiliknya.
- Keputusan menerima atau menolak registrasi berada di
  [Modul Autentikasi Akun](autentikasi-akun.md).

## Hubungan dengan Modul Lain

- **Dipanggil oleh** [Modul Autentikasi Akun](autentikasi-akun.md) saat
  registrasi.
- Tidak dipanggil langsung oleh modul lain. Masa berlaku yang dihasilkan
  disimpan di akun, lalu dipakai modul lain melalui pemeriksaan keanggotaan
  aktif di Modul Autentikasi Akun.

## Alasan Pengelompokan

Data akademik adalah sistem milik kampus di luar PerpusKu. Memisahkannya
membuat cara membaca sumber eksternal ini terkumpul di satu tempat. Jika
sistem akademik kampus berganti, hanya modul ini yang perlu disesuaikan.