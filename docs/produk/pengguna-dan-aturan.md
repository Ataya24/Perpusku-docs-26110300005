# Pengguna dan Aturan Operasional PerpusKu

Dokumen ini memuat panduan lengkap mengenai peran pengguna sistem PerpusKu serta seluruh aturan bisnis dan operasional perpustakaan kampus.

---

## 1. Peran dan Hak Pengguna

Sistem PerpusKu membagi pengguna ke dalam tiga peran (*roles*) dengan tanggung jawab dan batasan hak akses yang tegas:

```
                  ┌───────────────────────────────┐
                  │       PENGGUNA SISTEM         │
                  └───────────────┬───────────────┘
          ┌───────────────────────┼───────────────────────┐
          ▼                       ▼                       ▼
   [   ANGGOTA   ]         [  PUSTAKAWAN  ]        [     ADMIN    ]
  Mahasiswa & Dosen       Petugas Meja Sirkulasi   Pengelola Sistem
  - Registrasi mandiri    - Proses pengembalian    - Bekukan/aktifkan akun
  - Cari katalog buku     - Hitung & terima denda  - Unduh rekap bulanan
  - Pinjam mandiri        - Kelola data buku         (format PDF)
  - Perpanjang pinjam     - Batal reservasi lewat
  - Antre reservasi
```

### 1.1 Anggota (Mahasiswa dan Dosen)
- **Registrasi:** Mendaftar mandiri secara online menggunakan Nomor Induk Mahasiswa (NIM) atau Nomor Induk Pegawai (NIP). Data dicocokkan otomatis dengan data akademik universitas.
- **Aktivitas:** Mencari koleksi buku di katalog, melakukan peminjaman mandiri via pemindaian kode di kios/ponsel, memantau daftar pinjaman pribadi, memperpanjang masa pinjam, dan melakukan reservasi buku yang sedang habis.
- **Batasan Akses:** Anggota hanya dapat melihat dan mengelola data transaksi miliknya sendiri (*private scope*).

### 1.2 Pustakawan
- **Pembuatan Akun:** Akun dibuat dan dikonfigurasi langsung di basis data oleh administrator infrastruktur kampus.
- **Aktivitas:** Memproses penerimaan pengembalian buku fisik dengan pemindai barcode, memverifikasi besaran denda keterlambatan, menerima pembayaran denda tunai dan menandai status lunas, menambah/mengubah data koleksi katalog buku, serta membatalkan alokasi buku reservasi yang tidak diambil hingga lewat batas waktu.

### 1.3 Admin (Pengelola Sistem)
- **Pembuatan Akun:** Akun dibuat langsung di basis data oleh pengelola infrastruktur kampus.
- **Aktivitas:** Mengawasi kepatuhan pengguna dengan membekukan atau mengaktifkan kembali akun anggota yang bermasalah, serta mengakses dan mengunduh laporan rekapitulasi operasional bulanan perpustakaan dalam format PDF.

---

## 2. Kebijakan Keanggotaan Aktif

Agar dapat melakukan peminjaman mandiri, perpanjangan, maupun reservasi, seorang anggota wajib berstatus **Keanggotaan Aktif**. 

Status keanggotaan aktif ditentukan oleh dua kriteria kumulatif:
1. **Masa Berlaku Belum Habis:** Tanggal hari ini belum melewati batas `masa_berlaku` yang diperoleh dari data akademik (tanggal kelulusan mahasiswa atau masa kontrak dosen).
2. **Akun Tidak Dibekukan:** Kolom `status` akun bernilai `aktif` (tidak sedang dibekukan oleh Admin).

---

## 3. Kebijakan Peminjaman Buku

| Ketentuan | Nilai Aturan Baku | Catatan Dokumentasi |
|---|---|---|
| **Masa Pinjam Standar** | **7 hari kalender** | Berdasarkan aturan resmi `raw/01` §4. Perbedaan nilai 14 hari pada pseudocode `raw/03` FLOW 3 dicatat sebagai isu klarifikasi. |
| **Batas Kuota Pinjam** | **Maksimal 3 buku sekaligus** | Berdasarkan aturan resmi `raw/01` §4. Nilai 5 buku pada pesan validasi `raw/03` FLOW 3 dicatat sebagai isu klarifikasi. |
| **Metode Peminjaman** | Mandiri (*Self-service*) | Menggunakan pemindaian kode buku via kios perpustakaan atau ponsel anggota. |
| **Syarat Peminjaman** | Koleksi tersedia di rak / ada reservasi siap diambil | Kuota masih tersedia, akun aktif, serta tidak ada tunggakan denda. |

---

## 4. Kebijakan Perpanjangan Masa Pinjam

### 4.1 Perpanjangan Manual Mandiri
Anggota dapat mengajukan perpanjangan masa pinjam secara mandiri melalui menu **Peminjaman Saya** pada aplikasi web dengan ketentuan:
- **Batas Maksimal:** Maksimal **1 kali** per transaksi peminjaman.
- **Durasi Tambahan:** Menambah masa pinjam sebanyak **+7 hari kalender** dari tanggal jatuh tempo sebelumnya.
- **Kondisi Pencegah (*Blockers*):** Perpanjangan otomatis **DITOLAK** jika:
  1. Keanggotaan anggota sudah tidak aktif atau akun dibekukan.
  2. Batas perpanjangan telah tercapai (`jumlah_perpanjangan = 1`).
  3. Buku yang bersangkutan sedang berada dalam status antrean reservasi (`menunggu`) oleh anggota lain.
  4. Anggota memiliki tunggakan denda keterlambatan (`belum_lunas`).
  5. Anggota memiliki **denda berjalan**, yaitu buku lain yang telah melewati tanggal jatuh tempo namun belum dikembalikan ke perpustakaan.

### 4.2 Perpanjangan Otomatis
Sistem dirancang untuk mendukung perpanjangan otomatis menjelang tanggal jatuh tempo (disebutkan pada `raw/03` FLOW 4B dan `raw/04` F-04). Namun, parameter jadwal eksekusi, kuota jatah perpanjangan, serta penanganan kegagalan sistemnya masih memerlukan konfirmasi lebih lanjut dari tim pengembang sistem (lihat [Issue 2](../modules/peminjaman.md#perpanjangan-otomatis)).

---

## 5. Kebijakan Denda Keterlambatan dan Pembayaran

- **Besaran Tarif Denda:** **Rp1.000 per hari per buku**.
- **Waktu Mulai Perhitungan:** Denda mulai dihitung pada H+1 setelah tanggal jatuh tempo terlewati hingga tanggal buku dikembalikan fisik ke meja layanan.
- **Prosedur Pencatatan:** Denda otomatis dikalkulasikan oleh sistem dan dicatat pada tabel denda dengan status `belum_lunas` saat buku dipindai oleh pustakawan.
- **Mekanisme Pembayaran Resmi:** Pembayaran denda dilakukan secara **tunai langsung di meja layanan pustakawan**. Setelah uang tunai diterima, pustakawan membarui status denda pada sistem menjadi `lunas`.
- *Catatan Goal Pembayaran Online:* Pernyataan mengenai pembayaran denda online pada `raw/05` G-09 dicatat sebagai rencana sistem yang mekanismenya belum diimplementasikan pada operasional saat ini.

---

## 6. Kebijakan Antrean dan Reservasi Buku

Fitur reservasi menjamin keadilan bagi anggota untuk mendapatkan buku koleksi yang sedang tidak tersedia di rak perpustakaan:

1. **Syarat Pengajuan Reservasi:**
   - Buku yang bersangkutan sedang berstatus habis dipinjam (`stok_tersedia = 0`). Jika masih ada eksemplar di rak, pemesanan ditolak dan anggota diarahkan untuk meminjam langsung.
   - Anggota belum memiliki antrean reservasi aktif untuk judul buku yang sama.
   - Keanggotaan anggota berstatus aktif.
2. **Prinsip Antrean Adil:** Urutan pemesanan diatur ketat berdasarkan stempel waktu pengajuan (*First-In, First-Out* / FIFO).
3. **Masa Penahanan Buku (*Hold Period*):**
   - Saat buku dikembalikan oleh peminjam sebelumnya, sistem otomatis menahan buku fisik tersebut selama **2 hari kalender** untuk anggota pemesan pertama di antrean (`status = siap_diambil`).
   - Selama buku ditahan, eksemplar fisik tersebut **tidak dihitung ke dalam stok tersedia di rak**.
4. **Pengambilan Buku:** Anggota pemesan mengambil buku di meja layanan dengan melakukan pemindaian peminjaman mandiri, yang secara otomatis mengubah status reservasi menjadi `selesai`.
5. **Pembatalan Akibat Kedaluwarsa:** Jika dalam 2 hari buku tidak diambil oleh pemesan, pustakawan membatalkan reservasi tersebut (`status = batal`). Sistem secara otomatis mengalihkan penahanan buku selama 2 hari ke pemesan antrean berikutnya, atau mengembalikan buku ke rak (`stok_tersedia` bertambah 1) jika antrean telah habis.
