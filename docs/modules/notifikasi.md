# Modul Notifikasi

## Tanggung jawab

- Mendokumentasikan kebutuhan notifikasi kepada anggota terkait jatuh tempo dan perubahan status layanan.

## Isi/data dan aturan

- Notifikasi email sebelum jatuh tempo disebut sebagai goal produk.

### Kebutuhan notifikasi yang sudah jelas

- Kanal notifikasi yang disebut: email.
- Penerima utama: anggota/peminjam yang memiliki pinjaman aktif.
- Tujuan utama: pengingat sebelum jatuh tempo.

### Kebutuhan notifikasi yang belum terspesifikasi

- kapan pengiriman dilakukan (mis. H-1, H-2, atau multi-tahap),
- kondisi pemicu selain jatuh tempo,
- aturan idempoten agar email tidak terkirim ganda,
- template isi pesan untuk tiap kondisi,
- aturan fallback jika email gagal terkirim.

### Kaitan langsung dengan isu

- Isu [#13](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/13): notifikasi email tetap dicatat sebagai goal/fitur, namun detail jadwal dan kondisi pengiriman masih perlu klarifikasi.

## Hubungan

- Membaca data jadwal dari [Peminjaman](./peminjaman.md) dan [Perpanjangan](./perpanjangan.md).
- Dapat terpicu dari status [Reservasi](./reservasi.md).
- Harus menghormati data akun dari [Autentikasi Akun](./autentikasi-akun.md).

## Alasan pengelompokan

Walau detail implementasi belum lengkap, kebutuhan komunikasi lintas proses perlu dipisahkan agar daftar gap spesifikasi jelas dan dapat ditindaklanjuti.

## Referensi sumber

- `../../raw/04-daftar-fitur.txt`
- `../../raw/05-goal.txt`
- `../../raw/03-flow-aplikasi.txt`
