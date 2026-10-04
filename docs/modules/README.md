# Ringkasan Modul PerpusKu

Dokumentasi ini memecah PerpusKu menjadi modul fungsional agar aturan tidak ditulis berulang dan alur antarbagian mudah ditelusuri.

## Daftar modul

1. [Autentikasi Akun](./autentikasi-akun.md)
2. [Integrasi Akademik](./integrasi-akademik.md)
3. [Katalog Buku](./katalog-buku.md)
4. [Peminjaman](./peminjaman.md)
5. [Perpanjangan](./perpanjangan.md)
6. [Pengembalian dan Denda](./pengembalian-denda.md)
7. [Reservasi](./reservasi.md)
8. [Laporan](./laporan.md)
9. [Notifikasi](./notifikasi.md)

## Peta hubungan antar modul

- **Autentikasi Akun** memakai **Integrasi Akademik** saat registrasi anggota.
- **Peminjaman**, **Perpanjangan**, dan **Reservasi** bergantung pada status akun dari **Autentikasi Akun**.
- **Peminjaman**, **Pengembalian dan Denda**, **Reservasi**, serta **Katalog Buku** berbagi aturan stok buku.
- **Perpanjangan** memakai data dari **Peminjaman**, **Reservasi**, dan status denda dari **Pengembalian dan Denda**.
- **Laporan** mengambil rekap dari transaksi pada modul operasional.
- **Notifikasi** membaca jadwal/peristiwa dari **Peminjaman**, **Perpanjangan**, dan **Reservasi** (detail trigger masih perlu spesifikasi).

## Pemetaan isu dokumentasi ke modul

| Isu | Keputusan saat ini | Modul utama |
|---|---|---|
| [#8](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/8) istilah anggota/member/peminjam | Istilah baku: **anggota**; **peminjam** kontekstual; `id_member` hanya untuk nama field sumber | [Peminjaman](./peminjaman.md), [Autentikasi Akun](./autentikasi-akun.md), [Glosarium](../glosarium.md) |
| [#9](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/9) masa pinjam 7 vs 14 | Acuan dokumentasi 7 hari; 14 hari dicatat sebagai inkonsistensi sumber | [Peminjaman](./peminjaman.md), [Perpanjangan](./perpanjangan.md) |
| [#10](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/10) kuota 3 vs 5 buku | Acuan dokumentasi 3 buku; 5 buku dicatat sebagai inkonsistensi sumber | [Peminjaman](./peminjaman.md) |
| [#11](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/11) denda tunai vs online | Operasional saat ini: tunai; online dicatat sebagai target/konflik sumber | [Pengembalian dan Denda](./pengembalian-denda.md) |
| [#12](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/12) perpanjangan otomatis | Fitur ada, detail pemicu/pengecualian/notifikasi belum rinci | [Perpanjangan](./perpanjangan.md), [Notifikasi](./notifikasi.md) |
| [#13](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/13) notifikasi email | Goal tersedia, jadwal dan kondisi pengiriman belum terspesifikasi | [Notifikasi](./notifikasi.md) |

## Contoh dampak perubahan modul

Jika aturan status keanggotaan aktif pada modul **Autentikasi Akun** diubah, maka validasi di modul **Peminjaman**, **Perpanjangan**, dan **Reservasi** ikut berubah. Dampaknya langsung ke izin transaksi dan potensi penolakan layanan anggota.

## Referensi sumber

- `../../raw/02-cara-kerja-teknis.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/05-goal.txt`
