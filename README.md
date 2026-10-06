# Dokumentasi Sistem PerpusKu

Selamat datang di repositori dokumentasi resmi **PerpusKu**, sistem manajemen sirkulasi peminjaman buku perpustakaan kampus terintegrasi.

Repositori ini telah direstrukturisasi secara menyeluruh menggunakan pendekatan ***Computational Thinking*** (Dekomposisi, Pengenalan Pola, Abstraksi, dan Perancangan Algoritma) untuk mengubah catatan mentah (*raw data*) menjadi dokumentasi yang modular, terstandarisasi, dan bebas dari duplikasi logika (*single source of truth*).

---

## 1. Tentang PerpusKu

**PerpusKu** adalah sistem peminjaman buku perpustakaan kampus berbasis web yang telah beroperasi penuh (*production*) di perpustakaan pusat. Sistem ini menggantikan sistem pencatatan manual buku besar konvensional yang sebelumnya rawan kesalahan kalkulasi denda dan hilangnya pelacakan koleksi buku. 

Melalui PerpusKu, anggota perpustakaan (mahasiswa dan dosen) dapat melakukan peminjaman buku secara mandiri (*self-service*) melalui pemindaian kode di kios perpustakaan maupun ponsel pintar, memantau masa pinjam, serta melakukan reservasi buku yang sedang habis tanpa antre di meja layanan.

---

## 2. Peta Navigasi Dokumentasi

Dokumentasi PerpusKu disusun dengan struktur folder modular dan terarah sesuai kebutuhan pembaca:

```
perpusku/
├── README.md                      # Pintu masuk utama dokumentasi (file ini)
├── identitas.md                   # Identitas mahasiswa dan status pengerjaan
├── SOAL.md                        # Panduan tugas dan ketentuan pengerjaan
├── raw/                           # Arsip data dan catatan mentah asli (sumber primer)
└── docs/
    ├── glosarium.md               # Kamus istilah baku resmi PerpusKu
    ├── produk/                    # Dokumentasi tingkat tinggi (level bisnis & pengguna)
    │   ├── ringkasan.md           # Latar belakang, cara pemakaian, dan arsitektur produk
    │   ├── pengguna-dan-aturan.md # Peran pengguna dan tata tertib/aturan sirkulasi
    │   └── fitur-dan-goal.md      # Matriks ketercapaian fitur F-01..F-08 dan goal G-01..G-09
    ├── modules/                   # Spesifikasi teknis modular (level arsitektur & developer)
    │   ├── README.md              # Peta keterhubungan modul, matriks caller-callee, dan lapisan sistem
    │   ├── autentikasi-akun.md    # Registrasi, login, peran, dan definisi keanggotaan aktif
    │   ├── integrasi-akademik.md  # Pembacaan data sivitas akademika kampus
    │   ├── katalog-buku.md        # Data koleksi buku, pencarian, dan seluruh aturan perubahan stok
    │   ├── peminjaman.md          # Validasi peminjaman mandiri dan perpanjangan masa pinjam
    │   ├── pengembalian-denda.md  # Sirkulasi pengembalian, rumus denda, dan pembayaran tunai
    │   ├── reservasi.md           # Antrean pemesanan FIFO, penahanan 2 hari, dan status reservasi
    │   └── laporan.md             # Rekapitulasi statistik bulanan otomatis dan ekspor PDF
    └── diagrams/                  # Pemodelan visual sistem (PlantUML dan render gambar)
        ├── README.md              # Dokumentasi seluruh diagram dan penjelasan deskriptif
        ├── activity-registrasi-peminjaman.puml  # Activity diagram registrasi & pinjam
        ├── activity-pengembalian-reservasi.puml # Activity diagram kembali, denda, & reservasi
        ├── use-case.puml                        # UML use case diagram
        ├── sequence-peminjaman.puml             # UML sequence diagram peminjaman mandiri
        ├── sequence-pengembalian.puml           # UML sequence diagram pengembalian & alokasi
        └── img/                                 # Direktori gambar hasil render (.png)
```

---

## 3. Ringkasan Dokumen Utama

### A. Untuk Pihak Perpustakaan & Pengguna Umum
- 📖 [**Ringkasan Produk**](docs/produk/ringkasan.md): Memahami latar belakang transformasi perpustakaan, cara akses mandiri di kios, serta gambaran keamanan sistem.
- 📋 [**Pengguna dan Aturan Operasional**](docs/produk/pengguna-dan-aturan.md): Membaca kebijakan resmi masa pinjam (7 hari), kuota pinjam (maksimal 3 buku), sanksi denda keterlambatan (Rp1.000/hari), serta tata cara reservasi buku.
- 🎯 [**Fitur dan Goal Produk**](docs/produk/fitur-dan-goal.md): Memantau status implementasi 8 fitur utama dan ketercapaian 9 sasaran produk.
- 📚 [**Glosarium Istilah**](docs/glosarium.md): Daftar definisi baku untuk istilah *Anggota*, *Pustakawan*, *Admin*, *Stok Tersedia vs Ditahan*, *Jatuh Tempo*, hingga *Denda Berjalan*.

### B. Untuk Pengembang Sistem & Arsitek Perangkat Lunak
- 🗺️ [**Peta Arsitektur Modul**](docs/modules/README.md): Mempelajari pembagian 7 modul independen, lapisan sistem (*layered architecture*), kepemilikan tunggal aturan bisnis, serta analisis dampak perubahan.
- ⚙️ **Rincian Modul Spesifik:**
  - [Autentikasi Akun](docs/modules/autentikasi-akun.md) | [Integrasi Akademik](docs/modules/integrasi-akademik.md) | [Katalog Buku](docs/modules/katalog-buku.md)
  - [Peminjaman](docs/modules/peminjaman.md) | [Pengembalian dan Denda](docs/modules/pengembalian-denda.md) | [Reservasi](docs/modules/reservasi.md) | [Laporan](docs/modules/laporan.md)
- 📊 [**Diagram Alur dan UML**](docs/diagrams/README.md): Mempelajari visualisasi pemodelan *activity diagram* (berbasis swimlane modul), *use case diagram*, dan *sequence diagram* interaksi antarmodul.

---

## 4. Penanganan Temuan Kritis (GitHub Issues)

Dalam proses penyusunan dokumentasi ini, 5 masalah inkonsistensi data mentah telah dianalisis dan diselesaikan secara transparan:

1. **Inkonsistensi Istilah Pengguna:** Dibakukan secara terpusat pada [Glosarium](docs/glosarium.md), menghilangkan kerancuan tumpang tindih antara *anggota*, *member*, *peminjam*, dan *user*.
2. **Kekosongan Aturan Perpanjangan Otomatis:** Perpanjangan manual didokumentasikan lengkap dengan validasi denda berjalan, sementara perpanjangan otomatis dicatat sebagai fitur yang membutuhkan konfirmasi teknis lebih lanjut.
3. **Ketiadaan Fitur Notifikasi Email (Goal G-08):** Goal tetap dicatat, namun secara kritis dijelaskan bahwa tabel `AKUN` belum memiliki kolom email dan fitur pengirimnya belum ada.
4. **Kontradiksi Pembayaran Denda Online vs Tunai (Goal G-09):** Pembayaran operasional riil dibakukan secara tunai di meja pustakawan sesuai seluruh dokumen alur dan ketiadaan skema pembayaran elektronik.
5. **Perbedaan Masa Pinjam (7 vs 14 hari) dan Kuota (3 vs 5 buku):** Digunakan nilai `raw/01` (7 hari dan 3 buku) sebagai nilai sementara yang konsisten dengan aturan durasi perpanjangan +7 hari.

---

## 5. Informasi Mahasiswa

Identitas pengerjaan dan informasi repositori tercatat pada berkas [identitas.md](identitas.md).
