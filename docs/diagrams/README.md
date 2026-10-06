# Diagram Alur dan UML PerpusKu

Halaman ini menjelaskan alur kerja (*activity diagram*) dan diagram UML (*use case* serta *sequence diagram*) untuk sistem PerpusKu dengan bahasa yang lebih sederhana dan mudah dipahami. Seluruh diagram ini dibuat berdasarkan pembagian modul yang sudah disusun sebelumnya.

---

## 1. Diagram Alur Kerja (Activity Diagram)

### 1.1 Daftar Akun Baru dan Peminjaman Buku Mandiri
Diagram ini memperlihatkan proses dari awal seseorang mendaftar sebagai anggota perpustakaan hingga cara mereka meminjam buku sendiri lewat ponsel atau mesin di perpustakaan.

![Activity Diagram Registrasi dan Peminjaman Buku](img/activity-registrasi-peminjaman.png)

*File PlantUML:* [`activity-registrasi-peminjaman.puml`](activity-registrasi-peminjaman.puml)

**Penjelasan Singkat:**
Proses dimulai saat anggota baru mendaftar (datanya otomatis dicek dengan data kampus), lalu dilanjutkan dengan proses peminjaman buku. Sebelum buku bisa dipinjam, sistem akan mengecek tiga hal:
1. Apakah keanggotaan masih aktif?
2. Apakah jumlah buku yang dipinjam belum melewati batas maksimal (maksimal 3 buku)?
3. Apakah buku yang dicari benar-benar tersedia di rak atau sudah dipesan sebelumnya? 

Jika semua syarat terpenuhi, peminjaman akan dicatat untuk durasi 7 hari. Jika ada syarat yang gagal, proses otomatis dihentikan.

---

### 1.2 Pengembalian Buku, Perhitungan Denda, dan Pengaturan Antrean
Diagram ini memperlihatkan apa yang terjadi saat buku dikembalikan ke meja petugas perpustakaan.

![Activity Diagram Pengembalian dan Reservasi](img/activity-pengembalian-reservasi.png)

*File PlantUML:* [`activity-pengembalian-reservasi.puml`](activity-pengembalian-reservasi.puml)

**Penjelasan Singkat:**
Petugas memindai kode buku yang dikembalikan. Jika telat mengembalikan, sistem otomatis menghitung denda sebesar Rp1.000 per hari, lalu petugas menerima pembayaran tunainya. 

Setelah itu, sistem mengecek apakah ada orang lain yang sedang mengantre (*reservasi*) untuk meminjam buku tersebut:
* **Jika ada yang mengantre:** Buku langsung disimpan selama 2 hari khusus untuk orang pertama di antrean tersebut.
* **Jika tidak ada yang mengantre:** Buku langsung dikembalikan ke rak dan stok buku bertambah 1.

---

## 2. Diagram UML

### 2.1 Peta Fitur Sistem (Use Case Diagram)
Diagram ini menggambarkan batasan sistem PerpusKu, siapa saja yang menggunakannya, dan apa saja hal yang bisa mereka lakukan.

![Use Case Diagram PerpusKu](img/use-case.png)

*File PlantUML:* [`use-case.puml`](use-case.puml)

**Penjelasan Singkat:**
Sistem ini digunakan oleh tiga pengguna utama: **Anggota**, **Pustakawan**, dan **Admin**, serta dibantu oleh **Sistem Akademik Kampus**. 

Beberapa fitur penting saling terikat, contohnya: saat anggota ingin meminjam, memperpanjang, atau memesan buku, sistem wajib mengecek status keanggotaannya terlebih dahulu. Selain itu, fitur bayar denda hanya akan muncul jika anggota terlambat mengembalikan buku.

---

### 2.2 Urutan Proses Peminjaman Buku Mandiri (Sequence Diagram: Peminjaman)
Diagram ini memperlihatkan bagaimana bagian-bagian dalam sistem saling mengirim pesan dan bekerja sama saat anggota meminjam buku.

![Sequence Diagram Peminjaman Buku](img/sequence-peminjaman.png)

*File PlantUML:* [`sequence-peminjaman.puml`](sequence-peminjaman.puml)

**Penjelasan Singkat:**
Bagian Peminjaman bertindak sebagai pengatur utama. Ia akan bertanya ke bagian Akun untuk memastikan status keanggotaan aktif, mengecek batas kuota pinjaman, lalu memeriksa ketersediaan buku. 

Di sini ada dua kemungkinan: kalau buku itu ternyata pesanan (*reservasi*) yang siap diambil, status reservasinya diubah jadi selesai tanpa mengganggu stok rak. Tapi kalau itu peminjaman biasa, sistem langsung mengurangi stok buku yang ada di katalog.

---

### 2.3 Urutan Proses Pengembalian dan Pembayaran Denda (Sequence Diagram: Pengembalian)
Diagram ini menunjukkan proses komunikasi antar-bagian di dalam sistem saat pustakawan melayani pengembalian buku di meja layanan.

![Sequence Diagram Pengembalian Buku](img/sequence-pengembalian.png)

*File PlantUML:* [`sequence-pengembalian.puml`](sequence-pengembalian.puml)

**Penjelasan Singkat:**
Saat petugas memindai buku, bagian Pengembalian mengambil data peminjaman asli, mencatat tanggal kembali, dan menghitung denda jika terlambat. Setelah denda dibayar tunai, sistem mengecek daftar antrean: apakah ada orang yang menunggu buku tersebut? Jika ada, buku ditahan selama 2 hari untuk orang itu; jika tidak ada, stok buku di katalog langsung ditambah kembali.

---

## 3. Tabel Ringkasan Hubungan Modul dan Diagram

Tabel berikut merangkum bagaimana setiap bagian (*modul*) sistem ikut berperan di dalam berbagai diagram di atas:

| Nama Modul | Peran di Activity Diagram | Peran di Sequence Diagram | Fitur Utama yang Dikerjakan |
|---|---|---|---|
| **Autentikasi Akun** | Jalur/Kolom khusus | Berperan sebagai `Auth` | Login, daftar akun, cek keaktifan anggota |
| **Integrasi Akademik** | Jalur/Kolom khusus | Terhubung lewat bagian Akun | Validasi data kampus bersama Sistem Akademik |
| **Katalog Buku** | Jalur/Kolom khusus | Berperan sebagai `Catalog` | Cari buku, kelola data buku, update stok |
| **Peminjaman** | Jalur/Kolom khusus | Berperan sebagai `Loan` | Peminjaman mandiri, perpanjangan waktu pinjam |
| **Pengembalian dan Denda**| Jalur/Kolom khusus | Berperan sebagai `ReturnFine` | Proses kembali buku, pembayaran denda tunai |
| **Reservasi** | Jalur/Kolom khusus | Berperan sebagai `Resv` | Pesan buku, atur antrean dan alokasi buku |
| **Laporan** | Disebutkan dalam ruang lingkup umum | Disebutkan di fitur umum | Melihat dan mengunduh laporan bulanan (PDF) |
