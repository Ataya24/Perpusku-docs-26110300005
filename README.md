# PerpusKu - Dokumentasi Produk

PerpusKu adalah sistem peminjaman buku perpustakaan kampus yang sudah berjalan. Repository ini berisi dokumentasi terstruktur berbasis sumber mentah pada folder `raw/`.

## Ringkasan cepat

- Platform: aplikasi web perpustakaan kampus.
- Aktor utama: anggota, pustakawan, admin.
- Proses inti: registrasi/login, pencarian buku, peminjaman, perpanjangan, pengembalian + denda, reservasi, laporan bulanan.
- Fokus dokumentasi: konsistensi aturan bisnis dan pemetaan modul.

## Daftar isi dokumentasi

### 1) Dokumentasi produk

- [Ringkasan Produk](docs/produk/ringkasan.md)
- [Pengguna dan Aturan](docs/produk/pengguna-dan-aturan.md)
- [Fitur dan Goal](docs/produk/fitur-dan-goal.md)

### 2) Dokumentasi modul

- [Ringkasan dan peta modul](docs/modules/README.md)
- [Modul Autentikasi Akun](docs/modules/autentikasi-akun.md)
- [Modul Integrasi Akademik](docs/modules/integrasi-akademik.md)
- [Modul Katalog Buku](docs/modules/katalog-buku.md)
- [Modul Peminjaman](docs/modules/peminjaman.md)
- [Modul Perpanjangan](docs/modules/perpanjangan.md)
- [Modul Pengembalian dan Denda](docs/modules/pengembalian-denda.md)
- [Modul Reservasi](docs/modules/reservasi.md)
- [Modul Laporan](docs/modules/laporan.md)
- [Modul Notifikasi](docs/modules/notifikasi.md)

### 3) Diagram

- [Index diagram + pasangan `.puml` dan target `.png`](docs/diagrams/README.md)
- [Activity: Registrasi dan Peminjaman (`.puml`)](docs/diagrams/activity-registrasi-peminjaman.puml)
- [Activity: Pengembalian dan Reservasi (`.puml`)](docs/diagrams/activity-pengembalian-reservasi.puml)
- [Sequence: Peminjaman (`.puml`)](docs/diagrams/sequence-peminjaman.puml)
- [Sequence: Pengembalian (`.puml`)](docs/diagrams/sequence-pengembalian.puml)
- [Use case (`.puml`)](docs/diagrams/use-case.puml)

### 4) Glosarium

- [Glosarium istilah](docs/glosarium.md)

## Catatan keputusan isu dokumentasi (#8-#13)

- [#8](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/8): istilah umum dipakai **anggota**; **peminjam** bersifat kontekstual; `id_member` dipakai saat membahas nama field sumber.
- [#9](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/9): aturan utama masa pinjam **7 hari**; angka 14 hari di flow dicatat sebagai inkonsistensi sumber.
- [#10](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/10): kuota utama **3 buku**; angka 5 buku di flow dicatat sebagai inkonsistensi sumber.
- [#11](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/11): pembayaran denda didokumentasikan **tunai** sesuai alur operasional saat ini; goal pembayaran online dicatat sebagai kebutuhan klarifikasi.
- [#12](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/12): perpanjangan otomatis tetap didokumentasikan sebagai fitur, tetapi pemicu/pengecualian/notifikasi masih belum rinci.
- [#13](https://github.com/Ataya24/perpusku-docs-26110300005-/issues/13): notifikasi email dicatat sebagai goal/fitur yang memerlukan spesifikasi jadwal dan kondisi pengiriman.

## Sumber mentah (tidak diubah)

- [raw/01-deskripsi-produk.txt](raw/01-deskripsi-produk.txt)
- [raw/02-cara-kerja-teknis.txt](raw/02-cara-kerja-teknis.txt)
- [raw/03-flow-aplikasi.txt](raw/03-flow-aplikasi.txt)
- [raw/04-daftar-fitur.txt](raw/04-daftar-fitur.txt)
- [raw/05-goal.txt](raw/05-goal.txt)

## Keterbatasan render diagram

File PNG diagram belum dirender di environment agent ini. Folder `docs/diagrams/img/` disiapkan dengan `.gitkeep`, dan `docs/diagrams/README.md` sudah mendokumentasikan pasangan file `.puml` ke target `.png` beserta referensi gambar relatif.
