# Dokumentasi Sistem PerpusKu

Selamat datang di repositori dokumentasi resmi **PerpusKu**, sistem peminjaman buku perpustakaan kampus.

Repositori ini merapikan tumpukan catatan mentah (*raw data*) yang sebelumnya tercecer menjadi susunan dokumentasi yang jelas, rapi, dan mudah dipahami. Seluruh aturan dan cara kerja sistem diatur agar konsisten, tidak tumpang tindih, dan dapat dipahami oleh siapa saja tanpa harus membaca kode programnya.

---

## 1. Mengenal PerpusKu

**PerpusKu** adalah aplikasi web yang digunakan untuk mengelola peminjaman buku di perpustakaan pusat kampus. Sistem ini dibuat untuk menggantikan pencatatan manual di buku besar yang sebelumnya sering menimbulkan masalah, seperti salah menghitung denda atau petugas kesulitan melacak siapa yang sedang meminjam buku.

Dengan PerpusKu:
- **Mahasiswa dan dosen** bisa mencari koleksi buku dari laptop atau ponsel, meminjam buku sendiri di perpustakaan cukup dengan memindai kode buku, melihat daftar pinjaman, memperpanjang masa pinjam, atau memesan antrean buku jika sedang habis.
- **Petugas perpustakaan (pustakawan)** terbantu dalam memproses pengembalian buku, melihat hitungan denda otomatis, menerima pembayaran tunai di meja layanan, dan mengelola stok buku.
- **Pengelola sistem (admin)** dapat memantau jalannya perpustakaan melalui laporan bulanan yang rapi (dalam bentuk PDF) serta mengelola akun anggota.

---

## 2. Peta Dokumen dan Isi Repositori

Dokumentasi ini disusun ke dalam beberapa bagian agar pembaca bisa langsung menuju halaman yang dibutuhkan:

```
perpusku/
├── README.md                      # Halaman utama dokumentasi (file ini)
├── identitas.md                   # Data diri mahasiswa dan status pengerjaan tugas
├── SOAL.md                        # Panduan tugas awal
├── raw/                           # Catatan mentah asli sebelum dirapikan
└── docs/
    ├── glosarium.md               # Kamus istilah resmi agar tidak salah paham
    ├── produk/                    # Penjelasan umum produk dan aturan perpustakaan
    │   ├── ringkasan.md           # Latar belakang, cara pakai, dan cara kerja umum
    │   ├── pengguna-dan-aturan.md # Siapa saja penggunanya dan aturan peminjaman buku
    │   └── fitur-dan-goal.md      # Daftar fitur yang sudah jadi dan sasaran produk
    ├── modules/                   # Penjelasan rinci cara kerja sistem per modul
    │   ├── README.md              # Ringkasan pembagian modul dan hubungannya
    │   ├── autentikasi-akun.md    # Cara pendaftaran, login, dan syarat keaktifan akun
    │   ├── integrasi-akademik.md  # Pengecekan data mahasiswa/dosen ke sistem kampus
    │   ├── katalog-buku.md        # Pengelolaan data buku dan aturan perubahan stok
    │   ├── peminjaman.md          # Aturan peminjaman mandiri dan perpanjangan waktu
    │   ├── pengembalian-denda.md  # Alur pengembalian, hitungan denda, dan bayar tunai
    │   ├── reservasi.md           # Aturan antrean buku dan penahanan buku 2 hari
    │   └── laporan.md             # Pembuatan rekap bulanan otomatis dan unduh PDF
    └── diagrams/                  # Gambar alur dan rancangan sistem (PlantUML & PNG)
        ├── README.md              # Penjelasan seluruh gambar diagram
        ├── activity-registrasi-peminjaman.puml  # Diagram alur: pendaftaran & pinjam buku
        ├── activity-pengembalian-reservasi.puml # Diagram alur: kembali buku, denda, & antrean
        ├── use-case.puml                        # Diagram peran pengguna dan fiturnya
        ├── sequence-peminjaman.puml             # Diagram urutan kerja saat meminjam buku
        ├── sequence-pengembalian.puml           # Diagram urutan kerja saat mengembalikan buku
        └── img/                                 # Kumpulan gambar diagram siap lihat (.png)
```

---

## 3. Panduan Membaca Dokumen

### A. Untuk Pihak Perpustakaan dan Pembaca Umum
Bagi Anda yang ingin memahami aturan perpustakaan dan cara kerja aplikasi secara umum:
- [**Ringkasan Produk**](docs/produk/ringkasan.md): Latar belakang perpustakaan, cara anggota memakai aplikasi, dan gambaran umum sistem.
- [**Pengguna dan Aturan Operasional**](docs/produk/pengguna-dan-aturan.md): Panduan lengkap tentang siapa saja penggunanya, batas pinjam 3 buku, masa pinjam 7 hari, denda Rp1.000/hari, dan aturan antrean buku.
- [**Fitur dan Goal Produk**](docs/produk/fitur-dan-goal.md): Daftar lengkap fitur yang sudah berfungsi dan sasaran apa saja yang sudah tercapai.
- [**Glosarium Istilah**](docs/glosarium.md): Kamus kata-kata penting seperti arti *Anggota*, *Peminjam*, *Buku Ditahan*, *Jatuh Tempo*, hingga *Denda Berjalan*.

### B. Untuk Pengembang dan Pembaca Teknis
Bagi Anda yang ingin mengetahui bagaimana sistem bekerja di balik layar:
-  [**Peta Pembagian Modul**](docs/modules/README.md): Gambaran bagaimana sistem dipecah menjadi 7 bagian mandiri, siapa yang memanggil siapa, dan aturan perubahan data.
-  **Detail Modul:**
  - [Autentikasi Akun](docs/modules/autentikasi-akun.md) | [Integrasi Akademik](docs/modules/integrasi-akademik.md) | [Katalog Buku](docs/modules/katalog-buku.md)
  - [Peminjaman](docs/modules/peminjaman.md) | [Pengembalian dan Denda](docs/modules/pengembalian-denda.md) | [Reservasi](docs/modules/reservasi.md) | [Laporan](docs/modules/laporan.md)
-  [**Diagram Alur dan UML**](docs/diagrams/README.md): Gambar visual cara kerja sistem lengkap dengan penjelasan langkah demi langkah.

---

## 4. Hasil Pemeriksaan Catatan Mentah (Penyelesaian Masalah)

Saat membaca catatan mentah pertama kali, ditemukan 5 hal yang tidak konsisten atau membingungkan. Masalah tersebut telah diselesaikan dalam dokumentasi ini:

1. **Sebutan Pengguna yang Campur Aduk:** Kata *anggota*, *member*, *peminjam*, dan *user* sebelumnya dipakai bergantian tanpa penjelasan. Semuanya kini dibakukan lewat [Glosarium](docs/glosarium.md).
2. **Perpanjangan Otomatis yang Kurang Jelas:** Perpanjangan manual dijelaskan lengkap, sedangkan perpanjangan otomatis dicatat sebagai fitur yang membutuhkan kejelasan teknis lebih lanjut.
3. **Sasaran Notifikasi Email Belum Punya Data Pendukung:** Goal notifikasi email sempat dicatat selesai di bahan mentah, tetapi tabel data pengguna belum memiliki kolom alamat email dan fiturnya belum tersedia.
4. **Bayar Denda Online vs Bayar Tunai:** Sasaran sempat menyebutkan bayar online, namun kenyataan alur operasional di perpustakaan seluruhnya memakai pembayaran tunai langsung di meja petugas.
5. **Perbedaan Masa Pinjam dan Kuota:** Terdapat perbedaan antara aturan (7 hari & 3 buku) dengan alur simulasi (14 hari & 5 buku). Dokumentasi ini memakai aturan 7 hari dan maksimal 3 buku sebagai nilai sementara yang konsisten dengan tambahan perpanjangan 7 hari.

---

## 5. Informasi Mahasiswa

Data mahasiswa pengelola repositori ini tercantum pada berkas [identitas.md](identitas.md).
