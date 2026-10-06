# Fitur dan Goal Produk PerpusKu

Dokumen ini memetakan seluruh daftar fitur yang telah selesai dibangun beserta tujuan (*goals*) produk yang ingin dicapai oleh PerpusKu, dilengkapi dengan analisis kritis keselarasan data.

---

## 1. Daftar Fitur yang Berjalan di Produk

Berdasarkan `raw/04-daftar-fitur.txt`, seluruh fitur di bawah ini telah selesai dibangun dan telah beroperasi penuh di lingkungan produksi:

| Kode | Nama Fitur | Sasaran Pengguna | Modul Penanggung Jawab | Deskripsi Fungsional |
|:---:|---|---|---|---|
| **F-01** | Registrasi, Login, dan Pembekuan Akun | Anggota, Admin, Pustakawan | [Autentikasi Akun](../modules/autentikasi-akun.md) & [Integrasi Akademik](../modules/integrasi-akademik.md) | Anggota mendaftar mandiri memakai NIM/NIP yang divalidasi ke data akademik kampus. Login menggunakan NIM/NIP dan kata sandi terenkripsi. Admin dapat membekukan dan mengaktifkan akun. |
| **F-02** | Pencarian Katalog | Semua Pengguna | [Katalog Buku](../modules/katalog-buku.md) | Pencarian fleksibel berdasarkan judul buku, penulis, atau ISBN. Menampilkan informasi detail dan jumlah stok eksemplar yang tersedia di rak. |
| **F-03** | Peminjaman Buku Mandiri | Anggota | [Peminjaman](../modules/peminjaman.md) | Layanan mandiri dengan memindai kode buku di kios atau ponsel. Sistem memeriksa keaktifan anggota, batas kuota pinjam, dan stok tersedia. |
| **F-04** | Perpanjangan Peminjaman | Anggota | [Peminjaman](../modules/peminjaman.md) | Masa pinjam dapat diperpanjang manual melalui menu aplikasi (maksimal 1x, +7 hari) maupun otomatis menjelang jatuh tempo. |
| **F-05** | Pengembalian Buku dan Denda | Pustakawan | [Pengembalian dan Denda](../modules/pengembalian-denda.md) | Pemindaian buku yang kembali di meja sirkulasi. Sistem menghitung denda otomatis (Rp1.000/hari) dan pustakawan mencatat pelunasan tunai di tempat. |
| **F-06** | Reservasi Buku | Anggota, Pustakawan | [Reservasi](../modules/reservasi.md) | Anggota dapat memesan buku yang sedang habis dipinjam dan memantau antrean. Buku yang kembali ditahan 2 hari untuk pemesan pertama. Pustakawan dapat membatalkan reservasi kedaluwarsa. |
| **F-07** | Pengelolaan Katalog | Pustakawan | [Katalog Buku](../modules/katalog-buku.md) | Pustakawan dapat menambah judul buku baru, memperbarui informasi dan stok, serta menghapus data buku (selama tidak ada peminjaman atau reservasi aktif). |
| **F-08** | Laporan Bulanan Terjadwal | Admin | [Laporan](../modules/laporan.md) | Pekerjaan otomatis menyusun statistik setiap tanggal 1 (total pinjam, 10 buku terpopuler, total denda). Admin dapat melihat dan mengunduh berkas PDF. |

---

## 2. Matriks Pencapaian Goal Produk

Berdasarkan `raw/05-goal.txt`, berikut adalah sasaran produk yang telah ditetapkan beserta status ketercapaiannya:

| Kode Goal | Pernyataan Sasaran Produk | Status Sumber | Fitur Terkait | Catatan Status dan Validasi |
|:---:|---|:---:|:---:|---|
| **G-01** | Anggota dapat mencari buku dan melihat ketersediaannya tanpa bantuan petugas. | ✅ Tercapai | F-02 | Berjalan penuh melalui katalog pencarian mandiri di browser web. |
| **G-02** | Member dapat meminjam buku secara mandiri tanpa antre di meja layanan. | ✅ Tercapai | F-03 | Berjalan penuh via pemindaian kode buku di ponsel pintar atau kios mandiri. |
| **G-03** | Peminjam dapat memperpanjang pinjaman tanpa harus datang ke perpustakaan. | ✅ Tercapai | F-04 | Berjalan penuh via halaman web Peminjaman Saya. |
| **G-04** | Denda keterlambatan terhitung otomatis dan akurat. | ✅ Tercapai | F-05 | Berjalan penuh dengan rumus: `(tgl_kembali - tgl_jatuh_tempo) * Rp1.000`. |
| **G-05** | Antrean reservasi berjalan adil sesuai urutan pemesanan. | ✅ Tercapai | F-06 | Berjalan penuh dengan skema antrean FIFO berdasarkan `waktu_reservasi`. |
| **G-06** | Pustakawan dapat mengelola katalog buku tanpa bantuan tim teknis. | ✅ Tercapai | F-07 | Berjalan penuh melalui antarmuka web khusus pustakawan. |
| **G-07** | Admin menerima laporan bulanan tanpa perlu menyusunnya manual. | ✅ Tercapai | F-08 | Berjalan penuh via scheduler otomatis setiap tanggal 1 pukul 01:00 dan ekspor PDF. |
| **G-08** | User menerima notifikasi email sebelum buku jatuh tempo. | ✅ Tercapai | *Belum ada* | **Isu Temuan (Issue 3):** Dinyatakan tercapai pada sumber, namun tidak ada fitur maupun data pendukung email pada sistem saat ini. |
| **G-09** | Anggota dapat membayar denda secara online. | ✅ Tercapai | *Belum ada* | **Isu Temuan (Issue 4):** Dinyatakan tercapai pada sumber, namun mekanisme operasional riil berjalan secara tunai di meja pustakawan. |

---

## 3. Analisis Kritis Kesenjangan Dokumen Mentah

Sebagai bagian dari proses *Computational Thinking* (Abstraksi dan Evaluasi Kritis), dokumentasi PerpusKu mengidentifikasi beberapa perbedaan penting antara pernyataan dokumen mentah dengan kenyataan teknis sistem:

### 3.1 Isu Notifikasi Email (Goal G-08)
- **Kondisi Sumber:** Dokumen `raw/05-goal.txt` menandai G-08 dengan centang hijau [✅] (sudah tercapai).
- **Fakta Teknis:** Pada dokumen arsitektur data `raw/02` §2, tabel `AKUN` sama sekali **tidak memiliki kolom penyimpanan alamat email**. Selain itu, pada daftar fitur `raw/04` tidak tercantum modul pengirim email ataupun mekanisme notifikasi terjadwal.
- **Keputusan Dokumentasi:** G-08 tetap dicatat sebagai goal yang dinyatakan oleh pembuat dokumen, tetapi diberi catatan resmi bahwa implementasi teknis dan basis datanya belum tersedia dan memerlukan penambahan skema tabel.

### 3.2 Isu Pembayaran Denda Online (Goal G-09)
- **Kondisi Sumber:** Dokumen `raw/05-goal.txt` menandai G-09 dengan centang hijau [✅] (anggota dapat membayar denda secara online).
- **Fakta Teknis:** Seluruh dokumen operasional lainnya (`raw/01` §4, `raw/02` §6, `raw/03` FLOW 5, dan `raw/04` F-05) secara seragam menegaskan bahwa **pembayaran denda dilakukan secara tunai di meja pustakawan**. Tabel `DENDA` pun tidak memiliki kolom metode pembayaran (*payment gateway*, transfer, dsb.).
- **Keputusan Dokumentasi:** Mekanisme pembayaran denda yang didokumentasikan sebagai operasional aktif adalah **pembayaran tunai di meja sirkulasi**. Goal G-09 dicatat sebagai aspirasi fitur masa depan yang belum terealisasi.

### 3.3 Isu Kejelasan Perpanjangan Otomatis (Fitur F-04)
- **Kondisi Sumber:** Dokumen `raw/03` FLOW 4B dan `raw/04` F-04 menyebutkan bahwa peminjaman diperpanjang otomatis menjelang tanggal jatuh tempo.
- **Kekosongan Logika:** Tidak ada penjelasan mengenai jadwal *cron job* eksekusinya, apakah sistem memotong jatah perpanjangan manual, dan bagaimana notifikasi kegagalan jika buku sedang ditunggu pemesan reservasi.
- **Keputusan Dokumentasi:** Menguraikan fitur perpanjangan manual sebagai fitur utama yang telah memiliki aturan validasi lengkap, serta mencatat perpanjangan otomatis sebagai bagian yang memerlukan klarifikasi algoritma lebih lanjut.
