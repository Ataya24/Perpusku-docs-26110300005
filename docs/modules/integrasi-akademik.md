# Modul Integrasi Akademik

## Tanggung jawab

- Menyediakan validasi akademik saat registrasi anggota.
- Menyediakan masa berlaku keanggotaan dari data akademik kampus.

## Isi/data dan aturan

- Data referensi akademik dibaca tanpa diubah oleh PerpusKu.
- Registrasi ditolak jika NIM/NIP tidak ditemukan di sumber akademik.
- Masa berlaku akun anggota mengikuti tanggal akhir studi/kontrak dari data akademik.

## Hubungan

- Dipanggil oleh [Autentikasi Akun](./autentikasi-akun.md) saat registrasi.
- Nilai masa berlaku dipakai lintas modul saat cek keanggotaan aktif.

## Alasan pengelompokan

Integrasi eksternal dipisahkan agar perubahan sumber data kampus tidak mencampur logika akun internal PerpusKu.

## Referensi sumber

- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
