# Glosarium PerpusKu

| Istilah | Definisi |
|---|---|
| Anggota | Pengguna perpustakaan dari kalangan mahasiswa/dosen dengan akun PerpusKu. |
| Peminjam | Anggota yang sedang memiliki peminjaman aktif. |
| Pustakawan | Petugas perpustakaan yang menangani layanan pengembalian, denda, katalog, dan reservasi. |
| Admin | Pengelola sistem yang berwenang mengelola status akun anggota dan melihat laporan. |
| Keanggotaan aktif | Status anggota yang belum melewati masa berlaku dan tidak dibekukan admin. |
| Katalog | Kumpulan data buku (ISBN, judul, penulis, stok) yang dapat dicari pengguna. |
| Stok tersedia (`stok_tersedia`) | Jumlah eksemplar buku yang dapat langsung dipinjam. |
| Peminjaman | Transaksi pemakaian buku oleh anggota sampai dikembalikan. |
| Jatuh tempo | Batas akhir pengembalian buku pada transaksi peminjaman. |
| Perpanjangan | Penambahan masa pinjam terhadap transaksi yang masih aktif. |
| Denda | Biaya keterlambatan pengembalian buku (Rp1.000/hari/buku). |
| Reservasi | Pemesanan buku saat stok habis, berdasarkan antrean waktu pemesanan. |
| Siap diambil | Status reservasi ketika buku telah tersedia dan ditahan untuk anggota tertentu. |
| Batas ambil | Batas waktu pengambilan buku reservasi dalam status siap diambil (2 hari). |
| `id_member` | Nama field sumber pada data peminjaman/reservasi untuk merujuk identitas anggota. Tetap dipakai hanya saat menjelaskan struktur data mentah. |
| Notifikasi email | Komunikasi yang ditujukan ke anggota (contoh: pengingat jatuh tempo) dengan rincian aturan yang masih perlu spesifikasi. |

## Catatan istilah

- Istilah baku dokumentasi ini adalah **anggota**.
- Istilah **member** dipetakan ke **anggota**.
- Istilah **peminjam** digunakan kontekstual untuk anggota dengan pinjaman aktif.

## Referensi sumber

- `../raw/01-deskripsi-produk.txt`
- `../raw/02-cara-kerja-teknis.txt`
- `../raw/03-flow-aplikasi.txt`
