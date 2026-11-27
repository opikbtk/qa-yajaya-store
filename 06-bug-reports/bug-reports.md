# Bug Reports — yajaya.store
Format mengikuti ISO/IEC/IEEE 29119-3:2021 (Test Incident Report). Setiap bug perlu reproduksi ulang formal + screenshot/bukti sebelum final.

Dokumen ini berisi bug yang ditemukan pada website yajaya.store yang diuji pada 20 November 2026.

## BUG-01 — Filter galeri tidak memfilter, malah membuka lightbox | Major
- Sumber: pengecekan 20 Nov 2026, pagi (3x) dan sore (2x). Langkah: buka /galeri, klik filter Komunitas / Sekolah / Perusahaan.
- Aktual: grid tidak berubah, tetap menampilkan 8 item. Klik malah membuka lightbox item lain.
- Harapan: grid hanya menampilkan item sesuai kategori yang dipilih.
- Catatan: baris tombol filter kadang tidak kelihatan saat halaman di-render, ada duplikat tombol Event dan Sablon, dan tidak ada tombol reset Semua.

## BUG-02 — Lightbox galeri rusak: overlay tembus + caption salah | Major
- Sumber: pengecekan 20 Nov 2026. Langkah: buka lightbox dari /galeri.
- Aktual: overlay semi transparan, halaman di belakang tembus, judul tumpang tindih. Lightbox gambar Sablon Plastisol captionnya "Kaos komunitas custom design"; lightbox gambar Merchandise Event captionnya "Seragam sekolah custom"; lightbox dari filter Perusahaan menampilkan gambar DTF Printing dengan caption "Seragam polo shirt perusahaan".
- Harapan: overlay menutupi halaman di belakang, judul terbaca, caption sesuai gambar yang dibuka.

## BUG-03 — Kategori Polo Shirt di Home mengarah ke halaman login, produk polo tidak ada | Major
- Sumber: pengecekan 20 Nov 2026. Langkah: klik kartu "Polo Shirt — Lacoste Pique CVC premium, Mulai Rp85.000" di Home.
- Aktual: diarahkan ke /dashboard/pesanan/baru, lalu ke /login. Tidak ada produk polo di katalog dan tidak ada filter kategori Polo.
- Harapan: kartu mengarah ke /katalog atau ke halaman produk polo; kalau produknya memang belum ada, kartu jangan ditampilkan.
- Catatan: Polo Shirt Rp85.000 memang ada sebagai pilihan pakaian di form order custom, jadi angka "Mulai Rp85.000" cocok dengan form order, bukan dengan katalog.

## BUG-04 — Harga kategori Home tidak cocok dengan produk mana pun | Minor
- Sumber: pengecekan 20 Nov 2026. Kartu "Hoodie & Jacket — Mulai Rp155.000" di Home.
- Aktual: hoodie harganya Rp125.000 (coret Rp145.000), jaket termurah Rp300.000. Tidak ada produk seharga Rp155.000.
- Harapan: harga "mulai dari" sama dengan harga termurah di kategori itu.
- Catatan: Hoodie Rp155.000 memang ada sebagai pilihan pakaian di form order custom, jadi angka "Mulai Rp155.000" cocok dengan form order, bukan dengan katalog.

## BUG-05 — Pencarian memakai substring mentah | Minor
- Sumber: pengecekan 20 Nov 2026. Langkah: cari "polo" di katalog.
- Aktual: hasilnya dua produk Kaos Polos, karena "polo" ada di dalam kata "Polos". Tidak ada kaos polo.
- Harapan: pencarian mencocokkan kata utuh atau memberi tahu pengguna tidak ada hasil yang relevan.

## BUG-06 — Gambar produk ilustrasi SVG generik, ada yang salah bentuk | Minor
- Sumber: pengecekan 20 Nov 2026. Gambar Hoodie adalah kaos lengan pendek berkerudung dengan kantong kanguru, bukan hoodie. Kartu Jasa Sablon DTF memakai ulang ilustrasi Sablon Plastisol dari galeri.
- Harapan: gambar produk memakai foto produk asli, atau minimal ilustrasi yang sesuai bentuk produknya.

## BUG-07 — Artikel blog sudah lama, dari 2024 | Cosmetic
- Sumber: pengecekan 20 Nov 2026. Sitemap artikel blog terakhir diubah 5 Agu sampai 15 Nov 2024, sedangkan pengecekan dilakukan 20 Nov 2026.
- Harapan: tanggal artikel ditampilkan dan kontennya diperbarui, atau artikel lama ditandai sebagai arsip.

## BUG-08 — Judul halaman katalog dobel | Cosmetic
- Sumber: pengecekan 20 Nov 2026. Title tag halaman /katalog: "Katalog Produk & Apparel | YAJAYA STORE | YAJAYA STORE".
- Harapan: nama toko cukup ditulis sekali.

## BUG-09 — Footer "©2026YAJAYA STORE" tanpa spasi | Cosmetic
- Sumber: pengecekan 20 Nov 2026. Setiap footer tertulis "©2026YAJAYA STORE".
- Harapan: "© 2026 YAJAYA STORE".

## BUG-10 — Iframe peta di /kontak tampil kosong | Minor (kandidat)
- Sumber: pengecekan 20 Nov 2026. Iframe peta di halaman kontak tampil kosong saat dibuka.
- Harapan: peta lokasi toko tampil, atau iframe dihapus kalau memang tidak dipakai. Perlu dicek ulang, bisa jadi masalah jaringan saat pengecekan.
