# Modul Pengembalian dan Denda

## Tanggung Jawab

Modul ini mengelola pengembalian buku, **aturan tarif dan perhitungan denda**,
serta pencatatan pembayaran denda.

## Isi Modul

### Data

Sumber: `raw/02-cara-kerja-teknis.txt` §2 (tabel DENDA).

| Data | Keterangan |
|---|---|
| `id_denda` | Identitas unik denda |
| `id_peminjaman` | Transaksi yang terlambat |
| `jumlah` | Besar denda dalam rupiah |
| `status` | `belum_lunas` atau `lunas` |

Modul ini juga mengisi `tanggal_kembali` pada transaksi di
[Modul Peminjaman](peminjaman.md).

### Aturan Denda (definisi tunggal)

Sumber: `raw/01` §4, `raw/02` §6, `raw/03` FLOW 5.

- Tarif: **Rp1.000 per hari per buku**.
- Hari terlambat = `tanggal_kembali` − `tanggal_jatuh_tempo`, dihitung mulai
  hari setelah jatuh tempo.
- Denda = hari terlambat × tarif.
- Denda dicatat di tabel DENDA saat buku dikembalikan terlambat, dengan status
  `belum_lunas`.
- **Denda berjalan** adalah denda yang dihitung dengan rumus yang sama untuk
  buku yang sudah lewat jatuh tempo tetapi belum dikembalikan. Denda berjalan
  tidak dicatat di tabel DENDA, hanya dihitung saat diperlukan oleh
  [Modul Peminjaman](peminjaman.md) untuk perpanjangan.

### Aturan Pengembalian

Sumber: `raw/03` FLOW 5. Pelaku: pustakawan.

1. Pustakawan memindai kode buku yang dikembalikan.
2. Cari peminjaman berjalan untuk buku tersebut. Jika tidak ditemukan,
   tampilkan "Peminjaman tidak ditemukan" dan berhenti.
3. Catat `tanggal_kembali` = hari ini.
4. Jika terlambat, hitung dan catat denda sesuai aturan di atas, lalu tampilkan
   jumlahnya kepada pustakawan.
5. Laporkan pengembalian ke [Modul Reservasi](reservasi.md) untuk menentukan
   apakah buku ditahan untuk antrean. Perubahan stok diterapkan oleh
   [Modul Katalog Buku](katalog-buku.md#aturan).

### Aturan Pembayaran

- Pembayaran yang dijelaskan sumber dilakukan **tunai di meja pustakawan**
  (`raw/01` §4, `raw/02` §6, `raw/04` F-05).
- Setelah pembayaran diterima, pustakawan mengubah status denda menjadi
  `lunas`.

> [!NOTE]
> `raw/05` G-09 menyatakan anggota dapat membayar denda secara online, tetapi
> tidak ada sumber lain yang menjelaskan mekanismenya, dan tabel DENDA tidak
> memiliki kolom metode pembayaran. Goal ini tetap dicatat, dengan keterangan
> bahwa mekanismenya belum didokumentasikan.

## Hubungan dengan Modul Lain

- **Memanggil** [Modul Peminjaman](peminjaman.md) untuk mencari transaksi
  berjalan dan mengisi `tanggal_kembali`.
- **Memanggil** [Modul Reservasi](reservasi.md) setelah buku dikembalikan.
- **Memanggil** [Modul Katalog Buku](katalog-buku.md) untuk perubahan stok.
- **Dipanggil oleh** [Modul Peminjaman](peminjaman.md) untuk memeriksa denda
  `belum_lunas` dan denda berjalan saat perpanjangan.
- **Dibaca oleh** [Modul Laporan](laporan.md) untuk total denda.
- Akses dibatasi untuk pustakawan melalui
  [Modul Autentikasi Akun](autentikasi-akun.md).

## Alasan Pengelompokan

Pengembalian dan denda terjadi pada satu momen yang sama, yaitu saat buku
kembali. Tarif denda di dokumen mentah muncul di `raw/01` §4, `raw/03` FLOW 4A,
dan FLOW 5. Dengan menggabungkannya di sini, rumus denda hanya didefinisikan
satu kali dan dipakai ulang oleh perpanjangan serta laporan.