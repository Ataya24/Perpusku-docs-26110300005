# Glosarium Istilah PerpusKu

Glosarium ini merupakan kamus istilah resmi untuk seluruh dokumentasi sistem PerpusKu. Dokumen ini membakukan istilah-istilah yang sebelumnya digunakan secara bergantian dan tidak konsisten pada dokumen mentah (`raw/`), sehingga tidak menimbulkan kerancuan bagi pengembang sistem maupun pengelola perpustakaan.

---

## 1. Istilah Peran dan Pengguna

Untuk mengatasi inkonsistensi pada dokumen mentah (Issue 1), istilah terkait pengguna dibakukan sebagai berikut:

| Istilah Baku | Definisi | Istilah Lama di `raw/` | Cakupan Hak Akses |
|---|---|---|---|
| **Pengguna** (*User*) | Istilah umum yang memayungi setiap individu yang mengakses antarmuka sistem PerpusKu (baik Anggota, Pustakawan, maupun Admin). | *User*, *Pengguna* (`raw/02`, `raw/04`, `raw/05`) | Seluruh pengguna yang dapat membuka aplikasi. |
| **Calon Anggota** | Mahasiswa atau dosen yang sedang melakukan proses registrasi akun mandiri dan belum tersimpan di basis data. | *Calon anggota* (`raw/03` FLOW 1A) | Hanya halaman pendaftaran akun. |
| **Anggota** | Sivitas akademika (mahasiswa atau dosen) yang telah memiliki akun terdaftar dan aktif di PerpusKu. Istilah *Member* dianggap sinonim dan dibakukan menjadi *Anggota* (nama *member* hanya dipertahankan pada nama kolom basis data `id_member`). | *Anggota*, *Member* (`raw/01`, `raw/03`, `raw/05`) | Pencarian katalog, peminjaman mandiri, perpanjangan, reservasi buku, melihat profil diri. |
| **Peminjam** | Anggota yang sedang memiliki catatan transaksi peminjaman buku aktif yang belum dikembalikan. Digunakan khusus saat membahas konteks sirkulasi berjalan. | *Peminjam* (`raw/01`, `raw/03`, `raw/05`) | Konteks transaksi peminjaman dan perpanjangan. |
| **Pustakawan** | Petugas perpustakaan di meja layanan sirkulasi. Akun dibuat langsung oleh administrator infrastruktur. | *Pustakawan*, *Petugas* (`raw/01`, `raw/02`) | Memproses pengembalian, mencatat pembayaran denda, mengelola katalog buku, membatalkan reservasi kedaluwarsa. |
| **Admin** | Pengelola sistem perpustakaan kampus. Akun dibuat langsung di basis data. | *Admin*, *Pengelola sistem* (`raw/01`, `raw/02`) | Membekukan/mengaktifkan akun anggota, melihat dan mengunduh laporan bulanan. |

---

## 2. Istilah Sirkulasi dan Aturan Bisnis

| Istilah | Definisi |
|---|---|
| **Eksemplar** | Salinan fisik buku yang dimiliki perpustakaan. Satu judul buku dapat memiliki beberapa eksemplar fisik. |
| **Stok Total** (`stok_total`) | Jumlah keseluruhan eksemplar suatu buku yang tercatat dimiliki oleh perpustakaan. |
| **Stok Tersedia** (`stok_tersedia`) | Jumlah eksemplar buku yang sedang berada di rak dan bebas dipinjam secara langsung. Eksemplar yang sedang ditahan untuk antrean reservasi tidak dihitung dalam stok tersedia. |
| **Buku Ditahan** | Kondisi eksemplar buku fisik yang disimpan sementara di meja layanan khusus untuk pemesan terawal reservasi selama maksimal 2 hari kalender. |
| **Keanggotaan Aktif** | Syarat mutlak anggota untuk bertransaksi: masa berlaku akun (tanggal akhir studi/kontrak dari sistem akademik) belum kedaluwarsa dan akun tidak dalam status dibekukan. |
| **Masa Pinjam** | Durasi waktu yang diberikan kepada anggota untuk meminjam buku. Nilai sementara dokumentasi ditetapkan **7 hari kalender** sejak tanggal transaksi dibuat (berdasarkan `raw/01`). |
| **Batas Kuota Pinjam** | Jumlah maksimal buku yang boleh dipinjam secara bersamaan oleh satu orang anggota. Nilai sementara dokumentasi ditetapkan **maksimal 3 buku** (berdasarkan `raw/01`). |
| **Tanggal Jatuh Tempo** | Batas akhir tanggal pengembalian buku pinjaman tanpa dikenakan denda keterlambatan. |
| **Perpanjangan Manual** | Tindakan anggota memperpanjang masa pinjam buku sebesar +7 hari melalui aplikasi mandiri, maksimal 1 kali per peminjaman, dengan syarat buku tidak sedang direservasi anggota lain dan peminjam bebas dari denda. |
| **Perpanjangan Otomatis** | Fitur perpanjangan masa pinjam yang dijalankan sistem menjelang jatuh tempo (disebutkan pada `raw/03` FLOW 4B dan `raw/04` F-04, namun rincian algoritmanya masih menunggu klarifikasi lebih lanjut). |
| **Denda Keterlambatan** | Sanksi finansial sebesar Rp1.000 per hari per buku, dihitung mulai hari pertama setelah tanggal jatuh tempo terlewati hingga tanggal buku dikembalikan fisik. |
| **Denda Berjalan** | Akumulasi nilai denda keterlambatan hipotetis dari buku-buku lain milik anggota yang sudah lewat jatuh tempo namun belum dikembalikan. Digunakan sebagai syarat pencegah (*blocker*) perpanjangan pinjaman. |
| **Status Denda** | Status pembayaran kewajiban denda: `belum_lunas` (tercatat saat pengembalian terlambat) atau `lunas` (setelah pembayaran tunai diserahkan ke pustakawan). |
| **Reservasi Buku** | Pemesanan antrean untuk buku yang seluruh eksemplarnya sedang dipinjam (`stok_tersedia = 0`). Urutan penyerahan buku menggunakan prinsip *First-In, First-Out* (FIFO) berdasarkan `waktu_reservasi`. |
| **Status Reservasi** | Tahapan daur hidup reservasi: `menunggu` (dalam antrean), `siap_diambil` (buku telah kembali dan ditahan 2 hari), `selesai` (buku telah dipinjam oleh pemesan), atau `batal` (pemesan tidak mengambil buku hingga batas waktu 2 hari habis). |
| **Batas Ambil** | Batas waktu pengambilan buku bagi anggota yang reservasinya berstatus `siap_diambil`, yaitu tanggal pengembalian + 2 hari. |

---

## 3. Istilah Teknis Sistem

| Istilah | Definisi |
|---|---|
| **Kios Mandiri** | Perangkat komputer layar sentuh atau terminal stasioner di area perpustakaan yang digunakan anggota untuk memindai buku dan melakukan peminjaman mandiri. |
| **Data Akademik Kampus** | Sistem informasi universitas eksternal yang dibaca (secara *read-only*) oleh PerpusKu untuk memverifikasi validitas NIM mahasiswa atau NIP dosen serta tanggal berakhirnya masa studi/kontrak. |
| **Pseudocode** | Notasi algoritmik informal tingkat tinggi yang digunakan pada dokumen mentah `raw/03` untuk menjelaskan alur sistem tanpa terikat pada sintaks bahasa pemrograman tertentu. |
