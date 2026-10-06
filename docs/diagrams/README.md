# Gambar Alur Kerja dan Rancangan Sistem PerpusKu

Halaman ini menyajikan activity diagram dan diagram rancangan sistem use case dan sequence diagram untuk PerpusKu. Seluruh penjelasan ditulis dengan kalimat yang jelas agar mudah dipahami.

---

## 1. Activity Diagram

### 1.1 Pendaftaran Akun dan Peminjaman Buku Mandiri

Diagram ini memperlihatkan alur anggota perpustakaan, mulai dari pertama kali mendaftar hingga berhasil meminjam buku sendiri di perpustakaan.

![Activity Diagram Registrasi dan Peminjaman Buku](img/activity-registrasi-peminjaman.png)

*Berkas PlantUML:* [`activity-registrasi-peminjaman.puml`](activity-registrasi-peminjaman.puml)

**Penjelasan Alur:**
Proses diawali saat calon anggota mendaftar (identitasnya dicocokkan otomatis dengan data universitas). Saat ingin meminjam buku lewat ponsel atau kios mandiri, sistem akan memeriksa tiga syarat penting:
1. Apakah akun anggota masih aktif (belum habis masa berlakunya dan tidak sedang dibekukan)?
2. Apakah jumlah buku yang sedang dipinjam belum mencapai batas kuota (maksimal 3 buku)?
3. Apakah buku yang ingin dipinjam tersedia di rak, atau merupakan buku pesanan yang memang sudah siap diambil untuk anggota tersebut?

Jika semua syarat terpenuhi, sistem akan mencatat peminjaman selama 7 hari dan menampilkan bukti peminjaman. Jika ada syarat yang tidak terpenuhi, sistem akan menampilkan pesan pemberitahuan dan proses pinjam dihentikan.

---

### 1.2 Pengembalian Buku, Perhitungan Denda, dan Penanganan Antrean

Diagram ini memperlihatkan alur kerja di meja layanan saat buku fisik dikembalikan ke petugas perpustakaan.

![Activity Diagram Pengembalian dan Reservasi](img/activity-pengembalian-reservasi.png)

*Berkas PlantUML:* [`activity-pengembalian-reservasi.puml`](activity-pengembalian-reservasi.puml)

**Penjelasan Alur:**
Petugas memindai kode buku yang diserahkan peminjam. Jika pengembalian terlambat melewati tanggal jatuh tempo, sistem secara otomatis menghitung denda sebesar Rp1.000 per hari, mencatatnya, lalu petugas menerima pembayaran uang tunai langsung di meja layanan. 

Setelah denda diselesaikan, sistem memeriksa apakah ada anggota lain yang sedang mengantre memesan buku tersebut:
- **Jika ada antrean:** Buku langsung disimpan selama 2 hari khusus untuk pemesan nomor satu di antrean (stok rak tidak bertambah).
- **Jika tidak ada antrean:** Buku langsung dikembalikan ke rak koleksi dan stok buku yang siap dipinjam bertambah 1.

---

## 2. Unified Modeling Language (UML)

### 2.1 Peta Peran Pengguna dan Fitur (Use Case Diagram)

Diagram ini merangkum siapa saja yang berinteraksi dengan PerpusKu dan apa saja yang bisa mereka lakukan di dalam PerpusKu.

![Use Case Diagram PerpusKu](img/use-case.png)

*Berkas PlantUML:* [`use-case.puml`](use-case.puml)

**Penjelasan Rancangan:**
Sistem ini melayani tiga pengguna utama: **Anggota** (mahasiswa/dosen), **Pustakawan** (petugas meja layanan), dan **Admin** (pengelola sistem), serta terhubung dengan **Sistem Akademik Kampus** untuk memastikan keabsahan data anggota. 

Beberapa tindakan memiliki aturan yang mengikat: saat anggota ingin meminjam, memperpanjang, atau memesan antrean buku, sistem wajib memeriksa keaktifan akun anggota terlebih dahulu. Selain itu, pembayaran denda hanya akan aktif jika ada buku yang dikembalikan dalam kondisi telat.

---

### 2.2 Langkah Komunikasi Saat Meminjam Buku (Sequence Diagram: Peminjaman)

Diagram ini memperlihatkan bagaimana bagian-bagian di dalam aplikasi saling bertukar informasi saat melayani anggota yang meminjam buku sendiri.

![Sequence Diagram Peminjaman Buku](img/sequence-peminjaman.png)

*Berkas PlantUML:* [`sequence-peminjaman.puml`](sequence-peminjaman.puml)

**Penjelasan Langkah:**
Bagian Peminjaman bertindak sebagai koordinator utama. Bagian ini meminta verifikasi keaktifan akun ke bagian Autentikasi Akun, memastikan kuota pinjaman belum penuh, lalu berkoordinasi dengan bagian Reservasi dan bagian Katalog Buku. 

Jika buku yang dipinjam berasal dari pesanan yang sudah disiapkan, status pesanannya diselesaikan tanpa mengubah jumlah buku di rak. Namun jika peminjaman dilakukan secara biasa, jumlah stok buku di rak langsung dikurangi satu. Setelah semua beres, bukti peminjaman dan tanggal batas kembali ditampilkan kepada anggota.

---

### 2.3 Langkah Komunikasi Saat Mengembalikan Buku (Sequence Diagram: Pengembalian)

Diagram ini memperlihatkan urutan komunikasi antarbagian di dalam sistem saat petugas memproses pengembalian buku di meja sirkulasi.

![Sequence Diagram Pengembalian Buku](img/sequence-pengembalian.png)

*Berkas PlantUML:* [`sequence-pengembalian.puml`](sequence-pengembalian.puml)

**Penjelasan Langkah:**
Saat petugas memindai buku, bagian Pengembalian dan Denda mengambil data pinjaman dari bagian Peminjaman untuk mencatat tanggal kembali serta menghitung denda jika terlambat. Setelah pembayaran tunai diterima oleh petugas, bagian ini menghubungi bagian Reservasi untuk memeriksa antrean. 

Jika ada pemesan yang sedang menunggu, buku langsung disisihkan selama 2 hari untuk orang tersebut. Namun jika antrean kosong, bagian Katalog Buku akan menambahkan 1 stok buku ke rak agar bisa dipinjam oleh orang lain.

---

## 3. Tabel Peran Setiap Bagian dalam Diagram

Tabel berikut merangkum bagaimana ketujuh bagian (*modul*) sistem saling berbagi peran dalam diagram-diagram di atas:

| Nama Bagian (Modul) | Muncul di Activity Diagram Sebagai | Muncul di Sequence Diagram Sebagai | Tugas Utama yang Dijalankan |
|---|---|---|---|
| **Autentikasi Akun** | Jalur khusus *Autentikasi Akun* | Komponen `Auth` | Pendaftaran, login, dan memastikan akun anggota masih aktif. |
| **Integrasi Akademik** | Jalur khusus *Integrasi Akademik* | Penghubung data kampus | Memvalidasi NIM mahasiswa atau NIP dosen ke sistem universitas. |
| **Katalog Buku** | Jalur khusus *Katalog Buku* | Komponen `Catalog` | Mengelola data buku, pencarian, dan menambah/mengurangi stok buku. |
| **Peminjaman** | Jalur khusus *Peminjaman* | Komponen `Loan` | Melayani pinjam mandiri dan perpanjangan masa pinjam. |
| **Pengembalian dan Denda** | Jalur khusus *Pengembalian dan Denda* | Komponen `ReturnFine` | Mencatat buku kembali, menghitung denda, dan melunasi bayar tunai. |
| **Reservasi** | Jalur khusus *Reservasi* | Komponen `Resv` | Mengatur antrean pesanan buku dan menahan buku selama 2 hari. |
| **Laporan** | Cakupan fitur umum | Fitur laporan | Mengumpulkan rekap data bulanan otomatis untuk diunduh admin (PDF). |
