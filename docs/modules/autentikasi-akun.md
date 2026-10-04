# Modul Autentikasi Akun

## Tanggung jawab

- Registrasi anggota baru.
- Login semua peran (anggota, pustakawan, admin).
- Pengelolaan status akun anggota (aktif/dibekukan).

## Isi/data dan aturan

- Data akun: `nim_nip`, nama, kata sandi terenkripsi, peran, status, masa berlaku.
- Registrasi anggota wajib valid terhadap data akademik dan menolak akun duplikat.
- Login menggunakan kombinasi `nim_nip` dan kata sandi.
- Status aktif anggota ditentukan dari masa berlaku dan status pembekuan.

## Hubungan

- Memakai [Integrasi Akademik](./integrasi-akademik.md) untuk validasi NIM/NIP.
- Menjadi prasyarat akses untuk [Peminjaman](./peminjaman.md), [Perpanjangan](./perpanjangan.md), dan [Reservasi](./reservasi.md).

## Alasan pengelompokan

Semua aturan identitas, autentikasi, dan status akun disatukan agar pengecekan akses konsisten di seluruh transaksi.

## Referensi sumber

- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
