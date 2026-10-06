# Glosarium Istilah PerpusKu

Glosarium ini adalah kamus yang berisi istilah-istilah untuk memahami seluruh dokumentasi PerpusKu. Tujuannya agar pembaca—baik mahasiswa, petugas perpustakaan, maupun pengembang aplikasi—memiliki pemahaman yang sama dan tidak bingung dengan istilah-istilah yang sebelumnya dipakai campur aduk di catatan mentah (`raw/`).

---

## 1. Istilah Pengguna dan Peran

Di catatan mentah, sebutan untuk pengguna sering berganti-ganti (Issue 1). Berikut istilah resmi yang digunakan:

| Istilah Baku | Arti Sederhana | Sebutan Lama di Bahan Mentah | Hak Akses Utama |
|---|---|---|---|
| **Pengguna** | Sebutan umum untuk siapa saja yang membuka dan memakai aplikasi PerpusKu. | *User*, *Pengguna* (`raw/02`, `raw/04`, `raw/05`) | Semua orang yang login ke aplikasi. |
| **Calon Anggota** | Mahasiswa atau dosen yang baru mau mendaftar dan belum memiliki akun. | *Calon anggota* (`raw/03` FLOW 1A) | Hanya bisa membuka halaman pendaftaran. |
| **Anggota** | Mahasiswa atau dosen yang sudah resmi terdaftar dan akunnya aktif. Kata *member* punya arti yang sama, tetapi di dokumentasi resmi diseragamkan menjadi *anggota*. | *Anggota*, *Member* (`raw/01`, `raw/03`, `raw/05`) | Bisa cari buku, pinjam mandiri, perpanjang waktu pinjam, dan pesan antrean buku. |
| **Peminjam** | Anggota yang saat ini sedang membawa/meminjam buku perpustakaan. Istilah ini dipakai saat membicarakan transaksi pinjam-meminjam yang sedang berjalan. | *Peminjam* (`raw/01`, `raw/03`, `raw/05`) | Terikat dengan batas waktu pinjam dan denda jika telat. |
| **Pustakawan** | Petugas perpustakaan di meja layanan. Akunnya dibuatkan langsung oleh pengelola sistem kampus. | *Pustakawan*, *Petugas* (`raw/01`, `raw/02`) | Melayani pengembalian buku, menerima uang denda tunai, mencatat data buku baru, dan membatalkan pesanan buku yang lewat waktu. |
| **Admin** | Pengelola sistem perpustakaan. Akunnya juga dibuatkan langsung oleh pengelola kampus. | *Admin*, *Pengelola sistem* (`raw/01`, `raw/02`) | Berhak membekukan/mengaktifkan akun anggota dan mengunduh laporan rekap bulanan (PDF). |

---

## 2. Istilah Aturan Pinjam dan Sirkulasi Buku

| Istilah | Penjelasan Mudah |
|---|---|
| **Eksemplar** | Jumlah fisik buku yang ada. Misalnya, perpustakaan punya 5 buku fisik dengan judul yang sama, berarti ada 5 eksemplar. |
| **Stok Total** (`stok_total`) | Jumlah seluruh eksemplar buku yang dimiliki perpustakaan (baik yang ada di rak maupun yang sedang dipinjam orang). |
| **Stok Tersedia** (`stok_tersedia`) | Jumlah buku yang saat ini ada di rak dan boleh langsung diambil untuk dipinjam. Buku yang sedang disimpan khusus untuk pemesan antrean tidak dihitung di sini. |
| **Buku Ditahan** | Buku yang disimpan sementara di meja petugas selama 2 hari khusus untuk orang yang sudah antre memesan (*reservasi*). |
| **Keanggotaan Aktif** | Syarat utama bagi anggota untuk bisa meminjam atau memesan buku: masa berlaku akunnya belum habis dan akunnya tidak sedang dibekukan oleh admin. |
| **Masa Pinjam** | Jangka waktu peminjaman buku. Saat ini disepakati **7 hari** terhitung sejak hari peminjaman. |
| **Batas Kuota Pinjam** | Jumlah maksimal buku yang boleh dipinjam bersamaan oleh satu anggota, yaitu **maksimal 3 buku**. |
| **Tanggal Jatuh Tempo** | Batas hari terakhir pengembalian buku agar tidak terkena denda keterlambatan. |
| **Perpanjangan Manual** | Pengajuan tambah waktu pinjam (+7 hari) yang dilakukan sendiri oleh anggota lewat menu aplikasi. Maksimal hanya boleh 1 kali, dan hanya bisa dilakukan jika buku tidak sedang ditunggu orang lain serta anggota tidak punya tunggakan denda. |
| **Perpanjangan Otomatis** | Fitur perpanjangan otomatis dari sistem menjelang batas waktu habis (fitur ini sempat disebut di bahan mentah, tetapi cara kerjanya masih butuh kejelasan teknis lebih lanjut). |
| **Denda Keterlambatan** | Biaya denda sebesar **Rp1.000 per hari untuk tiap buku**, mulai dihitung sehari setelah tanggal jatuh tempo terlewati sampai buku diserahkan ke meja petugas. |
| **Denda Berjalan** | Perhitungan denda dari buku-buku lain milik anggota yang sudah lewat jatuh tempo tetapi belum dikembalikan. Denda ini membuat anggota tidak bisa memperpanjang pinjaman buku lainnya. |
| **Status Denda** | Catatan denda: `belum_lunas` (tercatat otomatis saat mengembalikan telat) atau `lunas` (setelah anggota membayar tunai ke pustakawan). |
| **Reservasi Buku** | Antrean pemesanan buku untuk buku yang semua fisiknya sedang dipinjam orang lain. Siapa yang memesan lebih dulu akan dilayani lebih dulu. |
| **Perjalanan Reservasi** | Tahapan antrean buku: `menunggu` (masih dalam antrean), `siap_diambil` (buku sudah ada dan disimpan 2 hari di meja petugas), `selesai` (buku sudah diambil oleh pemesan), atau `batal` (pemesan tidak mengambil buku sampai batas 2 hari habis). |
| **Batas Ambil** | Batas waktu 2 hari bagi pemesan untuk mengambil buku yang sudah siap di meja layanan. |

---

## 3. Istilah Teknis dan Pendukung

| Istilah | Penjelasan Mudah |
|---|---|
| **Kios Layanan Mandiri** | Komputer layar sentuh yang ada di ruangan perpustakaan untuk anggota memindai dan meminjam buku sendiri. |
| **Data Akademik Kampus** | Data induk milik kampus yang dibaca oleh PerpusKu untuk mengecek apakah NIM mahasiswa atau NIP dosen benar-benar terdaftar dan masih aktif kuliah/bekerja. |
| **Alur Pseudocode** | Catatan langkah-langkah logika kerja sistem yang ditulis seperti bahasa sehari-hari agar alurnya mudah dibaca sebelum dijadikan program komputer. |
