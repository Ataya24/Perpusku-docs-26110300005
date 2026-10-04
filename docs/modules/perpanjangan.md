# Modul Perpanjangan

## Tanggung jawab

- Memproses perpanjangan manual peminjaman.
- Mendokumentasikan perpanjangan otomatis sebagai kemampuan sistem.

## Isi/data dan aturan

- Perpanjangan manual maksimal 1 kali per transaksi, menambah 7 hari.
- Syarat manual: akun aktif, belum mencapai batas perpanjangan, buku tidak sedang ditunggu anggota lain, dan tidak ada denda belum lunas.

### Perpanjangan otomatis (status spesifikasi)

- Sumber menyebut perpanjangan otomatis tersedia menjelang jatuh tempo.
- Aturan rinci yang **belum tersedia**:
  - pemicu waktu tepatnya,
  - kondisi pengecualian final (antrean reservasi, denda, akun nonaktif),
  - mekanisme notifikasi kepada anggota,
  - jejak audit kapan perpanjangan otomatis dieksekusi.

### Kaitan langsung dengan isu

- Isu [#12](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/12): modul ini menandai bahwa perpanjangan otomatis adalah fitur yang ada di sumber, tetapi spesifikasi operasionalnya belum lengkap.

## Hubungan

- Memakai data transaksi dari [Peminjaman](./peminjaman.md).
- Memakai status antrean dari [Reservasi](./reservasi.md).
- Memakai status denda dari [Pengembalian dan Denda](./pengembalian-denda.md).
- Terhubung dengan [Notifikasi](./notifikasi.md) untuk kebutuhan komunikasi perubahan jatuh tempo.

## Alasan pengelompokan

Aturan perpanjangan dipisahkan dari peminjaman agar syarat, batas, dan pengecualian dapat dipelihara tanpa menduplikasi logika transaksi awal.

## Referensi sumber

- `../../raw/01-deskripsi-produk.txt`
- `../../raw/03-flow-aplikasi.txt`
- `../../raw/04-daftar-fitur.txt`
