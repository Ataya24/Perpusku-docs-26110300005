# Ringkasan Produk PerpusKu

## 1. Latar Belakang dan Tujuan

Sebelum sistem **PerpusKu** diimplementasikan, seluruh transaksi sirkulasi perpustakaan kampus dicatat secara manual di buku besar fisik. Metode manual ini menimbulkan berbagai kendala operasional yang merugikan:

- Perhitungan denda keterlambatan sering mengalami salah hitung dan kelalaian pencatatan.
- Petugas perpustakaan kesulitan melacak lokasi fisik dan pemegang buku yang sedang dipinjam.
- Terjadinya antrean panjang di meja layanan karena mahasiswa harus menunggu pencatatan manual.

Saat ini, sistem PerpusKu telah **berjalan penuh (operasional)** di perpustakaan pusat kampus. Seluruh pencatatan sirkulasi, status buku, antrean pemesanan, dan kalkulasi denda kini diproses secara terpusat melalui satu sistem digital terpadu.

---

## 2. Cara Pemakaian Produk Secara Umum

PerpusKu dirancang sebagai aplikasi web responsif yang fleksibel dan dapat diakses dari berbagai perangkat:

1. **Layanan Mandiri bagi Anggota:**
   - Anggota (mahasiswa dan dosen) dapat mencari ketersediaan koleksi buku melalui katalog web dari perangkat pribadi (laptop atau ponsel pintar).
   - Di perpustakaan, anggota melakukan peminjaman buku secara mandiri tanpa harus antre di meja layanan, cukup dengan memindai kode barcode/QR pada buku fisik menggunakan kamera ponsel atau melalui terminal **Kios Layanan Mandiri**.
   - Anggota dapat memantau daftar pinjaman berjalan, melakukan perpanjangan pinjaman, serta memesan buku yang sedang habis langsung dari antarmuka web.
2. **Layanan Sirkulasi bagi Pustakawan:**
   - Pengembalian buku fisik diproses oleh pustakawan di meja sirkulasi dengan memindai kode buku.
   - Pustakawan memverifikasi perhitungan denda otomatis, menerima pembayaran tunai di meja, mengelola stok katalog buku, serta membatalkan reservasi yang tidak diambil sesuai batas waktu.
3. **Pengelolaan bagi Administrator:**
   - Admin memantau kinerja operasional perpustakaan melalui laporan statistik bulanan terunduh (format PDF) serta mengelola status pembekuan akun anggota yang bermasalah.

---

## 3. Arsitektur Sistem Tingkat Tinggi

Secara konseptual, sistem PerpusKu bekerja melalui model arsitektur tiga lapis (*three-tier architecture*):

```
[ Browser Pengguna ]  ──(HTTP/Web)──>  [ Server Aplikasi ]  ──(SQL)──>  [ Basis Data PerpusKu ]
(Ponsel, Kios, Laptop)                   (Logika Bisnis & Aturan)        (Tabel Akun, Buku, Pinjam,
                                                     │                    Denda, Reservasi)
                                                     ▼
                                          [ Sistem Akademik Kampus ]
                                             (Hanya Membaca Data)
```

- **Lapis Antarmuka (Browser Pengguna):** Menampilkan antarmuka interaktif, formulir input, pemindai kode buku, dan navigasi menu sesuai dengan peran pengguna yang telah masuk (*login*).
- **Lapis Logika Bisnis (Server Aplikasi):** Memproses dan mengeksekusi semua aturan bisnis (validasi kuota pinjam, pengecekan denda, penghitungan denda keterlambatan, penahanan buku reservasi, serta kompilasi laporan bulanan).
- **Lapis Penyimpanan (Basis Data):** Menyimpan seluruh data secara terstruktur dan persisten pada lima tabel inti: `AKUN`, `BUKU`, `PEMINJAMAN`, `DENDA`, dan `RESERVASI`.
- **Integrasi Eksternal (Sistem Akademik):** Server aplikasi membaca data akademik universitas secara aman (*read-only*) untuk mencocokkan NIM/NIP calon anggota dan menarik tanggal masa berlaku keanggotaan.

---

## 4. Keamanan dan Pemeliharaan Data

- **Keamanan Kata Sandi:** Seluruh kata sandi pengguna disimpan dalam bentuk terenkripsi satu arah (*hashed*) di basis data dan tidak pernah disimpan atau ditampilkan dalam bentuk teks asli.
- **Pencadangan Otomatis (*Backup*):** Seluruh basis data PerpusKu dicadangkan (*backup*) secara otomatis setiap malam hari oleh tim pengelola infrastruktur kampus untuk menjamin integritas data dari potensi kegagalan sistem.

---

## 5. Navigasi Dokumentasi Lanjutan

Untuk mendalami aspek sistem lainnya, silakan merujuk ke dokumen berikut:
- [Panduan Pengguna dan Aturan Operasional](pengguna-dan-aturan.md)
- [Matriks Fitur dan Goal Produk](fitur-dan-goal.md)
- [Peta Arsitektur dan Modul Teknis](../modules/README.md)
- [Visualisasi Diagram Alur dan UML](../diagrams/README.md)
- [Glosarium Istilah Resmi](../glosarium.md)
