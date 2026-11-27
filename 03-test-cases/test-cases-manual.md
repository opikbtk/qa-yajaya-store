# Test Case Manual — yajaya.store
Acuan teknik: ISO/IEC/IEEE 29119-4:2021. Format dokumen: ISO/IEC/IEEE 29119-3:2021.

Dokumen ini berisi 40 test case manual untuk website yajaya.store yang diuji pada 20 November 2026. Kolom "Hasil awal 20 Nov" mencatat hasil saat inventarisasi dan pengecekan dashboard pada hari yang sama; eksekusi formal ulang tetap dilakukan dan hasilnya dicatat dengan status Pass/Fail/Blocked beserta ID bug bila Fail.

Legenda Prioritas: T=Tinggi, S=Sedang, R=Rendah.
Teknik: BB=black-box (EP/BVA/Decision Table/State Transition), EB=experience-based.

## A. Login & register Google-only (BB + EB)
| ID | Judul | Langkah | Hasil yang diharapkan | Teknik | Prioritas | Hasil awal 20 Nov |
|---|---|---|---|---|---|---|
| TC-L01 | Halaman login | Buka /login | Judul "Masuk ke Akun Anda", tombol "Lanjutkan dengan Google" | BB | T | PASS |
| TC-L02 | Halaman register | Buka /register | Judul "Daftar Akun Baru", tombol "Daftar Cepat dengan Google", 3 keuntungan tertulis | BB | T | PASS |
| TC-L03 | Tidak ada kolom email/password | Periksa /login dan /register | Tidak ada kolom isian, tidak ada lupa password | BB | T | PASS — memang tidak ada kolomnya |
| TC-L04 | Tidak ada akun demo | Cari "demo" di /login dan /register | Tidak ada akun demo yang ditampilkan | BB | T | PASS — tidak ada |
| TC-L05 | Rute terkunci /dashboard | Buka /dashboard tanpa login | Dilempar ke /login setelah spinner "Memuat portal dashboard…" | BB-ST | T | PASS |
| TC-L06 | Rute terkunci /dashboard/pesanan/baru | Buka /dashboard/pesanan/baru tanpa login | Pesan "Sesi tidak aktif. Silakan masuk untuk mengakses halaman ini." lalu ke /login | BB-ST | T | PASS |
| TC-L07 | Login Google (butuh akun asli) | Klik "Lanjutkan dengan Google" | Dialihkan ke Google, setelah berhasil kembali ke situs sebagai pengguna login | BB-ST | T | PASS — login berhasil, akun tes "hansenfarm" |
| TC-L08 | Dashboard setelah login | Login, buka /dashboard | Dashboard tampil, ada tracking pesanan dan invoice | BB | T | PASS (sebagian) — dashboard dan tracking tampil; invoice belum bisa dicek tanpa pesanan |
| TC-L09 | Beda admin dan customer | Bandingkan dashboard admin dan customer | Tampilan dan menu berbeda sesuai peran | BB | S | BLOCKED — butuh akun admin |

## B. Katalog & halaman detail produk (BB + EB)
| ID | Judul | Langkah | Hasil yang diharapkan | Teknik | Prioritas | Hasil awal 20 Nov |
|---|---|---|---|---|---|---|
| TC-K01 | Jumlah produk | Buka /katalog | 19 produk | BB-EP | T | PASS |
| TC-K02 | Harga dan diskon | Periksa semua kartu | Harga jual, harga coret, dan persen diskon konsisten (dihitung ulang) | BB | T | PASS — persen diskon cocok semua |
| TC-K03 | Search "denim" | Ketik denim di search katalog | Hanya Celana Denim | BB-EP | T | PASS |
| TC-K04 | Search "polo" | Ketik polo di search katalog | Tidak ada kaos polo; kalau menampilkan Kaos Polos, itu karena substring | BB-EP/EB | S | **FAIL — kandidat BUG-05:** hasilnya 2 produk Kaos Polos |
| TC-K05 | Filter kategori Hoodie | Klik kategori Hoodie | 1 produk | BB-EP | T | PASS |
| TC-K06 | Sortir harga rendah ke tinggi | Pilih "Harga: Rendah ke Tinggi" | Urutan Rp10.000, Rp40.000, Rp50.000, Rp100.000… | BB | S | PASS |
| TC-K07 | Sortir Populer/Terbaru/Terlaris | Klik tiap tombol sortir | Urutan berubah sesuai kriteria | BB | S | Belum |
| TC-K08 | Detail kaos-30s | Buka /produk/kaos-30s | 26 warna, ukuran S–XXXL, Rp40.000, rating 4.9, 842 penilaian, 1.2rb terjual | BB | T | PASS |
| TC-K09 | Detail hoodie | Buka /produk/hoodie | 5 warna, ukuran M–XXXL (tanpa S), Rp125.000, rating 4.9, 238 penilaian, 610 terjual | BB | T | PASS |
| TC-K10 | Tombol Pesan Sekarang | Periksa href tombol di halaman produk | Mengarah ke wa.me/628568703266 (jangan dikirim) | BB | T | PASS |
| TC-K11 | Link Beli di Shopee | Periksa link di halaman produk | Mengarah ke shopee.co.id/yajaya.id | BB | S | PASS |
| TC-K12 | Gambar produk | Periksa gambar Hoodie dan Sablon DTF | Gambar sesuai bentuk produk, bukan ilustrasi generik | EB | S | **FAIL — kandidat BUG-06:** gambar Hoodie kaos lengan pendek berkerudung |

## C. Sablon, galeri, blog (BB + EB)
| ID | Judul | Langkah | Hasil yang diharapkan | Teknik | Prioritas | Hasil awal 20 Nov |
|---|---|---|---|---|---|---|
| TC-SB01 | Kalkulator DTF Logo x3 | /sablon, jumlah 3, ukuran Logo | Total Rp30.000 | BB-BVA | T | PASS |
| TC-SB02 | Kalkulator DTF A4 x3 | /sablon, jumlah 3, ukuran A4 | Total Rp75.000 | BB-BVA | T | PASS |
| TC-SB03 | Tabel pricelist DTF | Periksa tabel di /sablon | Logo 10rb, A6+ 15rb, A5 20rb, A4 25rb, A3 40rb | BB | T | PASS |
| TC-G01 | Filter galeri Komunitas | /galeri, klik Komunitas | Grid hanya menampilkan item Komunitas | BB-EP | T | **FAIL — kandidat BUG-01:** malah membuka lightbox |
| TC-G02 | Filter galeri Sekolah | /galeri, klik Sekolah | Grid hanya menampilkan item Sekolah | BB-EP | T | **FAIL — kandidat BUG-01:** membuka lightbox Merchandise Event |
| TC-G03 | Lightbox galeri | Buka lightbox Sablon Plastisol | Overlay menutupi halaman, caption sesuai gambar | BB/EB | T | **FAIL — kandidat BUG-02:** overlay tembus, caption salah |
| TC-G04 | Tombol reset filter galeri | Cari tombol Semua di /galeri | Ada tombol reset ke semua item | BB | S | **FAIL — kandidat BUG-01:** tidak ada tombol reset |
| TC-B01 | Daftar blog | Buka /blog | 4 artikel, ada estimasi waktu baca | BB | S | PASS |
| TC-B02 | Tanggal artikel blog | Buka satu artikel | Tanggal terbit ditampilkan dan masih relevan | EB | S | **FAIL — kandidat BUG-07:** artikel dari 2024 |

## D. Navigasi & konten (BB + EB)
| ID | Judul | Langkah | Hasil yang diharapkan | Teknik | Prioritas | Hasil awal 20 Nov |
|---|---|---|---|---|---|---|
| TC-NV01 | Kategori Polo Shirt di Home | Klik kartu Polo Shirt di Home | Mengarah ke katalog atau produk polo | BB | T | **FAIL — kandidat BUG-03:** mengarah ke /dashboard/pesanan/baru lalu /login, produk polo tidak ada |
| TC-NV02 | Harga kategori Hoodie & Jacket | Baca kartu di Home | "Mulai Rp155.000" cocok dengan produk termurah kategori itu | EB | S | **FAIL — kandidat BUG-04:** hoodie Rp125.000, jaket termurah Rp300.000 |
| TC-NV03 | Judul halaman katalog | Periksa title tag /katalog | Nama toko cukup sekali | EB | R | **FAIL — kandidat BUG-08:** "… | YAJAYA STORE | YAJAYA STORE" |
| TC-NV04 | Footer | Baca footer di semua halaman | "© 2026 YAJAYA STORE" | EB | R | **FAIL — kandidat BUG-09:** tertulis "©2026YAJAYA STORE" |
| TC-NV05 | Peta di /kontak | Buka /kontak | Peta lokasi toko tampil | BB | S | **FAIL (kandidat) — BUG-10:** iframe tampil kosong |
| TC-NV06 | Rute /cart, /checkout, /admin | Buka ketiganya | 404 yang jelas, atau dialihkan ke halaman yang ada | BB | S | PASS — ketiganya 404 Next.js |
| TC-NV07 | Sitemap | Buka /sitemap.xml | Ada, memuat 7 halaman utama, 19 produk, 4 blog | BB | S | PASS — lastmod 20 Nov 2026 |

## E. Performa & aksesibilitas (ringkas, ISO 25010)
| ID | Judul | Harapan |
|---|---|---|
| TC-PF03 | Load hero Home | Foto hero tampil cepat, tidak kosong gelap lama |
| TC-PF04 | Load homepage | HTTP 200, <5 dtk di desktop |
| TC-AX02 | Responsif mobile | BELUM DIUJI — wajib diuji terpisah (viewport 360px, 768px) |

Total: 40 test case (A 9 + B 12 + C 9 + D 7 + E 3, sebagian sudah dieksekusi saat inventaris 20 Nov 2026). Jalankan ulang secara formal dan catat Hasil Aktual + Status (Pass/Fail/Blocked) + ID bug bila Fail.
