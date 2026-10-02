# SOAL: Merapikan Dokumentasi PerpusKu

## 1. Konteks

PerpusKu adalah sistem peminjaman buku perpustakaan kampus. Produknya **sudah jadi dan berjalan**, tetapi dokumentasinya masih berupa tumpukan teks mentah yang ditulis beberapa orang pada waktu berbeda.

Kamu adalah anggota baru tim. Tugasmu: mengubah tumpukan teks itu menjadi dokumentasi yang rapi, sehingga developer baru dan pihak perpustakaan bisa memahami produk ini **tanpa harus membaca kodenya** (kodenya memang tidak disediakan).

Kamu tidak perlu bisa pemrograman untuk mengerjakan soal ini. Yang dinilai adalah cara berpikirmu dalam memecah masalah, merancang modul, menggambar diagram, dan mengelola dokumentasi di GitHub.

**Waktu pengerjaan: 6 jam kerja. Dikerjakan individu.**

## 2. Yang Kamu Terima

Folder `raw/` berisi lima file teks mentah:

| File | Isi |
|---|---|
| `01-deskripsi-produk.txt` | Deskripsi produk dan aturan penggunaannya |
| `02-cara-kerja-teknis.txt` | Cara kerja sistem secara teknis (tanpa kode) |
| `03-flow-aplikasi.txt` | Alur aplikasi dalam bentuk pseudocode tingkat tinggi |
| `04-daftar-fitur.txt` | Daftar fitur yang sudah jadi |
| `05-goal.txt` | Tujuan produk, dengan tanda ✅ untuk yang dinyatakan tercapai |

Dokumen mentah ini ditulis apa adanya. Bisa jadi ada bagian yang berulang, tidak jelas, saling bertentangan, atau tidak sesuai dengan kenyataan. Tugasmu bukan hanya menyalin, tetapi membaca dengan kritis.

## 3. Pendekatan: Computational Thinking

Gunakan empat langkah berpikir ini sepanjang pengerjaan. Buktinya akan terlihat di hasil kerjamu (modul, diagram, dokumentasi), tidak perlu ditulis terpisah.

- **Dekomposisi**: pecah produk dan setiap proses menjadi bagian-bagian kecil.
- **Pengenalan pola**: temukan langkah atau aturan yang muncul berulang di tempat berbeda.
- **Abstraksi**: pilih detail yang penting untuk dokumentasi dan buang yang tidak perlu.
- **Algoritma**: tuliskan urutan langkah suatu proses dengan jelas dan tidak ambigu.

## 4. Tugas Pengerjaan

| # | Langkah | Keluaran |
|---|---|---|
| 1 | Buat repo dari template, isi identitas, baca semua teks mentah | `identitas.md`, catatan pribadi |
| 2 | Membuat issue | Issues |
| 3 | Modularisasi | `docs/modules/` |
| 4 | Diagram alur | `docs/diagrams/` |
| 5 | UML: use case dan sequence | `docs/diagrams/` |
| 6 | Ubah semua teks mentah menjadi Markdown terstruktur | `docs/` dan `README.md` |
| 7 | Menyelesaikan issue dan pemeriksaan akhir | Issues tertutup, repo final |

**Issues dibuat di awal** sebagai daftar temuan pentingmu, lalu **diselesaikan (resolve) di akhir** setelah dokumentasimu rampung.

### Langkah 1: Buat repo dan pahami

Buat repo pribadimu (berstatus **private**) dari template ini, tambahkan dosen sebagai collaborator, dan isi `identitas.md`. Panduan langkah demi langkahnya ada di file itu. Lalu baca kelima file di `raw/` sampai selesai. Selama membaca, catat:

- hal yang muncul berulang di beberapa tempat,
- hal yang tidak jelas atau membingungkan,
- hal yang tidak cocok antar file atau antar bagian,
- pertanyaan yang ingin kamu ajukan ke pembuat dokumen.

Catatan ini menjadi bahan issue di langkah 2.

### Langkah 2: Membuat issue

Pastikan fitur **Issues** aktif di repo-mu (Settings → General → Features → Issues), lalu buat **minimal 4 issue** dari temuan yang menurutmu **paling penting**, yaitu temuan yang bisa membuat dokumentasi salah atau menyesatkan jika dibiarkan.

Setiap issue memuat:

- judul yang spesifik,
- penjelasan temuan (di file dan bagian mana, mengapa jadi masalah),
- usulan penyelesaian atau pertanyaan klarifikasi.

Issue-issue ini menjadi daftar pekerjaanmu. Kerjakan langkah 3 sampai 6 sambil mengingat temuan-temuan tersebut, dan selesaikan semuanya di langkah 7.

### Langkah 3: Modularisasi

Kelompokkan isi produk ke dalam **modul**. Untuk setiap modul, tulis:

- **Tanggung jawab**: apa yang diurus modul ini (fokus pada satu hal).
- **Isi**: data dan aturan apa yang dimiliki modul ini.
- **Hubungan**: modul lain mana yang dipakai atau memakainya.
- **Alasan pengelompokan**: mengapa hal-hal ini digabung dalam satu modul.

Aturan penting: **tidak boleh ada logika atau aturan yang didefinisikan berulang.** Jika suatu langkah atau aturan muncul di lebih dari satu tempat pada dokumen mentah, definisikan satu kali di satu modul, lalu rujuk dari tempat lain.

Tambahkan satu penjelasan tentang hubungan antar modul secara keseluruhan (siapa memanggil siapa) dan satu contoh dampak jika salah satu modul diganti atau diubah.

**Keluaran:** satu file per modul di `docs/modules/`, ditambah `docs/modules/README.md` sebagai ringkasan dan peta hubungan antar modul.

### Langkah 4: Diagram alur

Buat diagram alur untuk **minimal 2 proses utama** dari flow aplikasi. Di PlantUML, diagram alur dibuat dengan **activity diagram**. Syaratnya:

- Sesuai dengan flow asli (setelah kamu memperbaiki hal yang berulang).
- Memuat titik awal, titik akhir, dan percabangan keputusan.
- Menunjukkan modul mana yang bertanggung jawab pada setiap bagian (misalnya dengan swimlane atau partition).
- Memakai istilah modul yang sama dengan langkah 3.

**Keluaran:** file sumber `.puml` dan gambar hasil render di `docs/diagrams/`.

### Langkah 5: UML

Buat dengan PlantUML:

1. **Satu use case diagram**: aktor, use case, batas sistem, dan relasi (termasuk `include` atau `extend` jika memang diperlukan).
2. **Minimal dua sequence diagram** untuk skenario berbeda.

Partisipan pada sequence diagram harus **aktor dan modul dari langkah 3**, bukan nama yang dikarang baru. Di bawah setiap diagram, tulis 2-3 kalimat yang menjelaskan apa yang digambarkan.

**Keluaran:** file sumber `.puml` dan gambar hasil render di `docs/diagrams/`.

### Langkah 6: Markdown yang tidak spaghetti

Ubah **seluruh isi `raw/`** menjadi dokumentasi Markdown di folder `docs/`.

- Tidak ada informasi yang hilang tanpa alasan. Yang digabung atau dibuang karena berulang harus jelas jejaknya.
- Struktur folder dan file **mencerminkan modul** dari langkah 3.
- `README.md` di akar repo diganti menjadi pintu masuk dokumentasi: ringkasan produk dan daftar isi dengan tautan ke semua dokumen penting.
- Setiap file punya judul dan heading berjenjang. Gunakan tabel untuk data yang memang berbentuk tabel, dan daftar untuk langkah atau butir.
- Tautan antar file memakai tautan relatif dan harus berfungsi.
- Diagram ditampilkan di halaman Markdown sebagai gambar, lengkap dengan penjelasannya.
- Sertakan glosarium istilah di `docs/glosarium.md`.

Contoh kerangka (boleh kamu ubah asal alasannya jelas):

```
README.md
identitas.md
SOAL.md                (biarkan)
raw/                   (biarkan, jangan dihapus)
docs/
├── produk/
├── modules/
├── diagrams/
│   └── img/
└── glosarium.md
```

### Langkah 7: Menyelesaikan issue dan pemeriksaan akhir

**Resolve setiap issue** yang kamu buat di langkah 2:

1. Tulis **komentar penutup** di issue: keputusan yang kamu ambil di dokumentasi dan alasannya.
2. **Lampirkan file hasilnya** di komentar itu dengan menyeret dan melepasnya ke kotak komentar, misalnya file modul atau file Markdown yang sudah dirapikan. Untuk diagram, lampirkan gambar `.png` **dan** file `.puml`-nya (file `.puml` adalah kode PlantUML yang berasosiasi dengan gambar itu). Jika GitHub menolak suatu file, cukup sertakan tautan ke file tersebut di repo-mu.
3. Klik **Close issue**.

Jika suatu temuan butuh jawaban dari pembuat dokumen yang tidak bisa kamu dapatkan, jangan menebak diam-diam. Tulis di dokumentasi nilai sementara yang kamu pakai beserta alasannya, jelaskan hal itu di komentar penutup, lalu tutup issue-nya.

Setelah semua issue tertutup, periksa:

- Semua issue sudah ditutup, masing-masing dengan komentar penutup dan lampiran file hasil.
- Semua tautan antar file berfungsi.
- Semua gambar diagram tampil di halaman repo (buka di browser untuk memastikan).
- Istilah konsisten di semua dokumen.
- Struktur folder, modul, diagram, dan README saling cocok.
- `identitas.md` sudah terisi.

## 5. Aturan Teknis

- **Semua dikerjakan lewat web GitHub.** Kamu tidak perlu memakai `git push` atau `git pull`. Edit file dengan ikon pensil, buat file baru lewat **Add file → Create new file**, dan unggah gambar lewat **Add file → Upload files**.
- **Semua diagram memakai PlantUML**: diagram alur (activity diagram), use case diagram, dan sequence diagram.
- **GitHub tidak menampilkan PlantUML secara otomatis.** Karena itu setiap diagram punya dua file:
  1. file `.puml`, yaitu **kode** PlantUML yang menghasilkan gambar, dan
  2. gambar `.png` hasil render dari kode itu, yang kamu buat dengan alat PlantUML yang dipakai di kelas, lalu unggah ke repo.

  Keduanya selalu berpasangan: kalau kode `.puml` berubah, render ulang gambarnya.

  Gambar ditanam di halaman Markdown dengan format `![Judul diagram](img/nama-file.png)`. Pastikan alamat gambarnya sesuai letak file Markdown-nya.
- Contoh format minimal PlantUML (bukan jawaban):

```
@startuml
start
if (Sudah login?) then (ya)
  :Tampilkan beranda;
else (tidak)
  :Tampilkan halaman login;
endif
stop
@enduml
```

- Bahasa dokumentasi: **Bahasa Indonesia**.
- Repo-mu berstatus **private**: hanya kamu dan dosen (sebagai collaborator) yang bisa melihatnya. Jangan menaruh data pribadi selain yang diminta di `identitas.md`.
- Jangan mengubah isi folder `raw/`. Folder itu adalah sumber aslimu.

## 6. Pengumpulan

Kumpulkan **URL repo-mu** sebelum batas waktu yang diumumkan di kelas. Pastikan:

- repo-mu berstatus **private** dan dosen sudah kamu tambahkan sebagai collaborator,
- `identitas.md` terisi,
- Issues bisa dilihat dan semuanya sudah tertutup.
