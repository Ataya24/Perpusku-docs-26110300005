# Dokumentasi Sistem PerpusKu

**PerpusKu** adalah aplikasi web manajemen sirkulasi perpustakaan kampus yang menggantikan sistem pencatatan manual buku besar. Sistem ini mengintegrasikan layanan peminjaman mandiri (*self-service*), reservasi antrean buku, perhitungan denda otomatis, dan penyusunan laporan bulanan.

Repositori ini memuat dokumentasi terstruktur hasil analisis dan modularisasi dari dokumen mentah (`raw/`) menggunakan pendekatan *Computational Thinking*.

---

## 1. Navigasi Dokumentasi

Dokumentasi sistem dikelompokkan ke dalam tiga bagian utama:

### Dokumentasi Tentang PerpusKu 
* [**Ringkasan Produk**](docs/produk/ringkasan.md) — Latar belakang, alur pemakaian umum, arsitektur dasar, dan keamanan data.
* [**Pengguna dan Aturan Operasional**](docs/produk/pengguna-dan-aturan.md) — Peran pengguna, kebijakan masa pinjam (7 hari), kuota (maksimal 3 buku), denda, dan aturan reservasi.
* [**Fitur dan Goal Produk**](docs/produk/fitur-dan-goal.md) — Matriks implementasi fitur (F-01 s.d. F-08) dan ketercapaian target sistem (G-01 s.d. G-09).
* [**Glosarium Istilah**](docs/glosarium.md) — Standarisasi istilah sistem (*Anggota*, *Peminjam*, *Stok Tersedia*, *Buku Ditahan*, dsb.).

###  Arsitektur & Modul
* [**Peta Modul (README)**](docs/modules/README.md) — Pembagian 7 modul independen, diagram pemanggilan antarmodul, dan arsitektur sistem.
* **Detail Modul:** [Autentikasi Akun](docs/modules/autentikasi-akun.md) | [Integrasi Akademik](docs/modules/integrasi-akademik.md) | [Katalog Buku](docs/modules/katalog-buku.md) | [Peminjaman](docs/modules/peminjaman.md) | [Pengembalian dan Denda](docs/modules/pengembalian-denda.md) | [Reservasi](docs/modules/reservasi.md) | [Laporan](docs/modules/laporan.md)

### Diagram Alur & Pemodelan UML
* [**Dokumentasi Diagram (README)**](docs/diagrams/README.md) — Penjelasan naratif untuk seluruh pemodelan visual sistem.
* **Activity Diagram:** [Registrasi & Peminjaman](docs/diagrams/activity-registrasi-peminjaman.puml) | [Pengembalian & Reservasi](docs/diagrams/activity-pengembalian-reservasi.puml)
* **UML Diagram:** [Use Case Diagram](docs/diagrams/use-case.puml) | [Sequence Peminjaman](docs/diagrams/sequence-peminjaman.puml) | [Sequence Pengembalian](docs/diagrams/sequence-pengembalian.puml)

---

## 2. Struktur Repositori

```
perpusku/
├── README.md                      # Dokumentasi utama (file ini)
├── identitas.md                   # Identitas mahasiswa dan status pengerjaan
├── SOAL.md                        # Panduan tugas
├── raw/                           # Dokumen teks mentah asli
└── docs/
    ├── glosarium.md               # Kamus istilah resmi
    ├── produk/                    # Dokumentasi bisnis & aturan operasional
    ├── modules/                   # Spesifikasi teknis 7 modul sistem
    └── diagrams/                  # Berkas PlantUML (.puml) dan gambar render (.png)
```

---

## 3. Resolusi Masalah (GitHub Issues)

Lima inkonsistensi utama pada dokumen mentah diselesaikan dengan keputusan berikut:

| Masalah | Temuan Dokumen Mentah | Keputusan Dokumentasi |
|---|---|---|
| **Istilah Pengguna** | *Anggota*, *member*, *peminjam*, dan *user* dipakai tanpa definisi baku. | Dibakukan di [Glosarium](docs/glosarium.md): *Anggota* untuk peran resmi, *peminjam* untuk transaksi aktif. |
| **Perpanjangan Otomatis** | Disebutkan di `raw/03` FLOW 4B tetapi tidak memiliki parameter validasi teknis. | Perpanjangan manual didokumentasikan penuh; perpanjangan otomatis dicatat butuh konfirmasi lanjutan. |
| **Goal Notifikasi Email (G-08)** | Ditandai tercapai pada `raw/05`, namun tabel `AKUN` tidak memiliki kolom alamat email. | Tetap dicatat sebagai target sistem, dengan catatan skema basis data belum mendukung. |
| **Goal Bayar Online (G-09)** | Ditandai tercapai pada `raw/05`, tetapi semua alur operasional menyatakan tunai di meja. | Prosedur resmi dibakukan tunai di meja sirkulasi; pembayaran online dicatat belum diimplementasikan. |
| **Masa Pinjam & Kuota** | Konflik antara `raw/01` (7 hari, 3 buku) dan `raw/03` (14 hari, 5 buku). | Menggunakan aturan `raw/01` (7 hari, 3 buku) sebagai nilai acuan sementara yang konsisten dengan perpanjangan +7 hari. |

---

## 4. Informasi Mahasiswa

Data mahasiswa pengembang repositori ini tercantum pada [identitas.md](identitas.md).
