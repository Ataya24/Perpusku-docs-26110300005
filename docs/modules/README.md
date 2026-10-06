# Peta Pembagian Bagian (Modul) PerpusKu

Agar PerpusKu tidak rumit dan membingungkan, PerpusKu ini dibagi menjadi **tujuh modul (bagian kerja)** berdasarkan fungsi masing-masing. 

Prinsip penting yang diterapkan adalah: **setiap aturan hanya ditulis satu kali di bagian yang berhak mengaturnya**. Bagian lain yang membutuhkan aturan tersebut cukup merujuk ke bagian pemiliknya, tanpa membuat aturan baru yang bisa berujung saling bertentangan.

---

## 1. Daftar Tujuh Bagian PerpusKu

| Nama Bagian (Modul) | Tugas Utama yang Diurus |
|---|---|
| [**Autentikasi Akun**](autentikasi-akun.md) | Mengurus pendaftaran anggota baru, login semua pengguna, pembagian peran, dan memastikan apakah akun masih aktif atau sedang dibekukan. |
| [**Integrasi Akademik**](integrasi-akademik.md) | Menghubungkan PerpusKu dengan sistem kampus untuk memeriksa keabsahan NIM mahasiswa atau NIP dosen serta masa studinya. |
| [**Katalog Buku**](katalog-buku.md) | Menyimpan data buku, melayani pencarian buku, dan mengatur kapan stok buku di rak harus bertambah atau berkurang. |
| [**Peminjaman**](peminjaman.md) | Memeriksa syarat boleh pinjam, mencatat transaksi peminjaman mandiri, dan melayani perpanjangan masa pinjam. |
| [**Pengembalian dan Denda**](pengembalian-denda.md) | Mencatat buku yang kembali, menghitung denda keterlambatan secara otomatis, dan mencatat pembayaran tunai. |
| [**Reservasi**](reservasi.md) | Mengatur antrean pesanan buku yang sedang habis, menahan buku selama 2 hari saat buku kembali, dan membatalkan pesanan yang lewat waktu. |
| [**Laporan**](laporan.md) | Mengumpulkan data secara otomatis setiap awal bulan untuk membuat laporan rekapitulasi yang bisa diunduh oleh admin dalam format PDF. |

---

## 2. Siapa yang Mengatur Aturan Penting?

Berdasarkan dari raw document, aturan-aturan di bawah ini sering ditulis berulang di berbagai tempat dengan penjelasan yang berbeda-beda. Di dokumentasi ini, setiap aturan sudah ditempatkan di satu bagian resmi:

| Aturan Penting | Sebelumnya Muncul di Catatan Mentah | Sekarang Resmi Diatur di |
|---|---|---|
| **Syarat Keanggotaan Aktif** | `raw/01` §4, `raw/02` §3, `raw/03` FLOW 3, 4A, 6A | [Modul Autentikasi Akun](autentikasi-akun.md#aturan) |
| **Aturan Kapan Stok Berubah** | `raw/02` §5, `raw/03` FLOW 3, 5, 6B | [Modul Katalog Buku](katalog-buku.md#aturan) |
| **Tarif dan Rumus Hitung Denda** | `raw/01` §4, `raw/02` §6, `raw/03` FLOW 4A, 5 | [Modul Pengembalian dan Denda](pengembalian-denda.md#aturan-denda-definisi-tunggal) |
| **Penyimpanan Buku Pesanan (2 Hari)** | `raw/01` §4, `raw/03` FLOW 5, 6B, `raw/04` F-06 | [Modul Reservasi](reservasi.md#aturan) |
| **Masa Pinjam (7 Hari) & Kuota (3 Buku)** | `raw/01` §4, `raw/03` FLOW 3, 4A | [Modul Peminjaman](peminjaman.md#nilai-aturan) |

---

## 3. Alur Hubungan Antarbagian

### Siapa Memanggil Siapa?

Setiap bagian saling terhubung untuk menyelesaikan suatu proses. Tabel di bawah ini memperlihatkan siapa yang meminta bantuan dan apa yang diminta:

| Bagian Peminta | Bagian yang Dimintai Bantuan | Alasan / Keperluan |
|---|---|---|
| **Autentikasi Akun** | Integrasi Akademik | Memeriksa apakah calon anggota benar terdaftar di kampus saat registrasi. |
| **Peminjaman** | Autentikasi Akun | Memastikan akun anggota masih aktif sebelum mengizinkan pinjam atau perpanjang. |
| **Peminjaman** | Katalog Buku | Mengecek ketersediaan buku di rak dan mengurangi stoknya saat dipinjam. |
| **Peminjaman** | Reservasi | Mengecek apakah buku yang diambil adalah pesanan anggota yang sudah siap, dan mengecek antrean saat ada yang ingin memperpanjang pinjaman. |
| **Peminjaman** | Pengembalian dan Denda | Memeriksa apakah anggota punya denda yang belum dibayar saat mengajukan perpanjangan. |
| **Pengembalian dan Denda** | Peminjaman | Mencari data pinjaman lama untuk mencatat tanggal kembali buku. |
| **Pengembalian dan Denda** | Reservasi | Menanyakan apakah ada orang yang sedang mengantre untuk buku yang baru saja dikembalikan. |
| **Pengembalian dan Denda** | Katalog Buku | Meminta stok rak ditambah 1 jika buku yang kembali tidak ada yang mengantre. |
| **Reservasi** | Autentikasi Akun | Memastikan akun anggota aktif sebelum membuat pesanan antrean buku. |
| **Reservasi** | Katalog Buku | Mengecek stok buku dan memberi tahu katalog saat ada buku yang harus ditahan untuk pemesan. |
| **Katalog Buku** | Peminjaman & Reservasi | Memeriksa apakah buku masih dipakai sebelum pustakawan menghapus data buku dari katalog. |
| **Laporan** | Peminjaman, Pengembalian, & Katalog | Membaca data transaksi dan daftar buku untuk membuat ringkasan bulanan (hanya membaca, tidak mengubah data apa pun). |

---

### Tingkatan Susunan PerpusKu

Untuk memudahkan pemahaman, hubungan ketujuh bagian di atas dapat dibayangkan seperti tingkatan gedung:

1. **Tingkat Laporan (Paling Atas):** [Laporan](laporan.md) — bagian ini hanya membaca rangkuman dari bagian-bagian di bawahnya tanpa pernah mengubah data.
2. **Tingkat Pelayanan Sehari-hari:** [Peminjaman](peminjaman.md), [Pengembalian dan Denda](pengembalian-denda.md), dan [Reservasi](reservasi.md) — bagian yang melayani interaksi langsung dengan anggota dan pustakawan setiap hari.
3. **Tingkat Data Pokok:** [Autentikasi Akun](autentikasi-akun.md) dan [Katalog Buku](katalog-buku.md) — bagian penyedia data utama (data pengguna dan data buku) yang dibutuhkan oleh tingkat pelayanan.
4. **Tingkat Sumber Luar:** [Integrasi Akademik](integrasi-akademik.md) — pintu penghubung untuk membaca data mahasiswa/dosen dari sistem universitas.

---

## 4. Alasan Mengapa Dibagi Menjadi Modul-Modul Ini

Bagian-bagian ini dipisahkan berdasarkan data yang mereka kelola:
- Data akun dipisahkan dari data buku agar pengaturan pengguna tidak tercampur dengan koleksi fisik.
- Peminjaman dipisahkan dari pengembalian karena peminjaman dilakukan mandiri oleh anggota di awal, sedangkan pengembalian dilayani oleh pustakawan di akhir.
- Reservasi dipisahkan secara khusus karena memiliki aturan antrean dan waktu tunggu penahanan buku sendiri.
- Pembuatan laporan dipisahkan tersendiri karena tugasnya hanya membaca data secara berkala tiap awal bulan, sehingga tidak mengganggu proses transaksi sehari-hari.

---

## 5. Contoh Nyata Manfaat Pembagian Modul Ini

**Contoh Kasus:** Pihak kampus memutuskan untuk menaikkan tarif denda keterlambatan dari Rp1.000 menjadi Rp2.000 per hari.

- **Dengan dokumentasi modular yang rapi:**
  Kita **hanya perlu mengubah satu angka** di satu tempat, yaitu di halaman [Modul Pengembalian dan Denda](pengembalian-denda.md#aturan-denda-definisi-tunggal). Secara otomatis, bagian perpanjangan di Modul Peminjaman dan bagian rekapitulasi di Modul Laporan akan langsung mengikuti aturan baru tersebut karena mereka merujuk ke tempat yang sama.
- **Sebelum dirapikan (pada catatan mentah):**
  Perubahan tarif denda harus dicari dan diubah secara manual di tiga tempat terpisah (`raw/01`, `raw/03` FLOW 4A, dan `raw/03` FLOW 5). Jika salah satu terlewat, aturan perpustakaan akan saling bertentangan dan membingungkan petugas.