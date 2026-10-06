# Modul Reservasi

## Tanggung Jawab

Modul ini mengelola pemesanan buku yang sedang habis, urutan antrean,
penahanan buku, dan **seluruh perubahan status reservasi**.

## Isi Modul

### Data

Sumber: `raw/02-cara-kerja-teknis.txt` §2 (tabel RESERVASI).

| Data | Keterangan |
|---|---|
| `id_reservasi` | Identitas unik reservasi |
| `id_member` | Anggota yang memesan |
| `id_buku` | Buku yang dipesan |
| `waktu_reservasi` | Waktu pemesanan, penentu urutan antrean |
| `status` | `menunggu`, `siap_diambil`, `selesai`, atau `batal` |
| `batas_ambil` | Hanya terisi saat status `siap_diambil` |

### Status Reservasi

| Status | Arti | Berubah menjadi |
|---|---|---|
| `menunggu` | Berada di antrean | `siap_diambil` saat buku tersedia untuk pemesan ini |
| `siap_diambil` | Buku ditahan selama 2 hari | `selesai` jika diambil, `batal` jika lewat `batas_ambil` |
| `selesai` | Buku sudah dipinjam pemesan | Status akhir |
| `batal` | Tidak diambil sampai batas waktu | Status akhir |

**Reservasi aktif** adalah reservasi berstatus `menunggu` atau `siap_diambil`.

### Aturan

**Membuat reservasi** (`raw/03` FLOW 6A, pelaku: anggota)

1. Anggota membuka detail buku dan menekan "Reservasi".
2. Periksa **keanggotaan aktif** sesuai
   [Modul Autentikasi Akun](autentikasi-akun.md#aturan).
3. Jika `stok_tersedia` lebih dari 0 menurut
   [Modul Katalog Buku](katalog-buku.md), tampilkan "Buku tersedia, silakan
   pinjam langsung" dan berhenti.
4. Jika anggota sudah memiliki reservasi `menunggu` untuk buku yang sama,
   tampilkan "Sudah ada di antrean" dan berhenti.
5. Simpan reservasi dengan `waktu_reservasi` = sekarang dan status `menunggu`.
6. Tampilkan posisi antrean anggota.

**Menahan buku untuk antrean** (definisi tunggal, dipakai setelah pengembalian
dan setelah pembatalan)

1. Ambil reservasi `menunggu` dengan `waktu_reservasi` paling awal untuk buku
   tersebut.
2. Jika ada, ubah statusnya menjadi `siap_diambil` dan isi
   `batas_ambil` = hari ini + 2 hari.
3. Laporkan hasilnya ke [Modul Katalog Buku](katalog-buku.md#aturan) untuk
   perubahan stok.

**Mengambil buku yang ditahan** (`raw/03` FLOW 3)

- Saat [Modul Peminjaman](peminjaman.md) mencatat peminjaman dari reservasi
  `siap_diambil`, status reservasi berubah menjadi `selesai`.

**Membatalkan reservasi yang tidak diambil** (`raw/03` FLOW 6B, pelaku:
pustakawan)

1. Pustakawan membuka daftar reservasi `siap_diambil` yang `batas_ambil`-nya
   sudah lewat.
2. Pustakawan memilih reservasi dan menekan "Batalkan". Status menjadi `batal`.
3. Jalankan aturan **menahan buku untuk antrean** untuk pemesan berikutnya.

## Hubungan dengan Modul Lain

- **Memanggil** [Modul Autentikasi Akun](autentikasi-akun.md) untuk
  pemeriksaan keanggotaan aktif.
- **Memanggil** [Modul Katalog Buku](katalog-buku.md) untuk membaca stok dan
  menerapkan perubahan stok.
- **Dipanggil oleh** [Modul Peminjaman](peminjaman.md) untuk memeriksa
  reservasi `siap_diambil`, menyelesaikannya, dan memeriksa antrean saat
  perpanjangan.
- **Dipanggil oleh** [Modul Pengembalian dan Denda](pengembalian-denda.md)
  setelah buku dikembalikan.
- **Dipanggil oleh** [Modul Katalog Buku](katalog-buku.md) untuk memeriksa
  reservasi aktif sebelum buku dihapus.

## Alasan Pengelompokan

Antrean dan penahanan buku memiliki status dan batas waktu sendiri. Di dokumen
mentah, langkah "ambil reservasi paling awal lalu tahan 2 hari" ditulis dua
kali (FLOW 5 dan FLOW 6B). Di modul ini langkah tersebut didefinisikan satu
kali sebagai aturan **menahan buku untuk antrean**, lalu dipakai ulang.