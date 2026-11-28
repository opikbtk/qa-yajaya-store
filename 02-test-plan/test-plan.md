# Test Plan — Pengujian Website yajaya.store

| Item | Keterangan |
|---|---|
| Objek uji | <https://www.yajaya.store/> (redirect dari <https://yajaya.store/>) |
| Objek yang diuji | Website multi-halaman, 19 produk, login Google-only |
| Standar acuan | ISO/IEC/IEEE 29119-1:2022, ISO/IEC/IEEE 29119-5:2024, ISO/IEC 25010:2023, ISO/IEC 25002:2024, ISO/IEC 25040:2024, IEEE 1012-2024 |
| Sudut pandang | Tester dari sisi pelanggan (external / customer perspective) — tanpa white-box, tanpa akses source code |
| Status dokumen | 20 November 2026 |
| Referensi lengkap | [01-references/standards-journals.md](../01-references/standards-journals.md) |

Catatan soal standar: format dokumen test plan ini mengikuti struktur yang dijelaskan ISO/IEC/IEEE 29119-3:2021 sebagai konvensi kerja. Namun karena aturan tugas ini hanya menerima referensi 2022–2026, dan edisi terkini 29119-2, 29119-3, serta 29119-4 terbit tahun 2021, ketiga standar itu tidak dimasukkan ke daftar referensi formal. Penjelasan lengkapnya ada di [01-references/standards-journals.md](../01-references/standards-journals.md).

## 1. Tujuan Pengujian (Test Objectives)

Pengujian ini dilakukan untuk menjawab satu pertanyaan utama: **apakah website yajaya.store bisa dipakai oleh pembeli sungguhan untuk menemukan produk, memahami harga, dan memesan tanpa hambatan?**

Tujuan rinciannya:

1. Memverifikasi semua fungsi yang terlihat oleh pelanggan berjalan sesuai harapan: navigasi multi-halaman, login dan register, pencarian, filter, sortir, halaman detail produk, kalkulator sablon, galeri, blog, dan order lewat WhatsApp.
2. Memverifikasi konsistensi konten dan harga di semua tempat produk itu muncul: kartu katalog, halaman detail, kategori di Home, dan tabel pricelist.
3. Menilai kualitas website menurut ISO/IEC 25010:2023 pada lima karakteristik prioritas: functional suitability, interaction capability, reliability, performance efficiency, dan security (sebatas yang bisa diuji dari luar).
4. Mendokumentasikan setiap defect yang ditemukan dengan langkah reproduksi, bukti, severity, dan priority, supaya pemilik toko bisa memperbaikinya berdasarkan urutan prioritas.
5. Menghasilkan bukti pengujian yang bisa dipertanggungjawabkan: test case yang bisa dijalankan ulang, log eksekusi, dan test report dengan verdict yang jelas.

Yang bukan tujuan pengujian ini: menilai kualitas kode sumber, mengukur code coverage, menguji database atau API internal, dan melakukan penetration testing penuh. Semua itu berada di luar sudut pandang pelanggan.

## 2. Ruang Lingkup Pengujian (Scope)

### 2.1 In-Scope — yang diuji

**Navigasi dan struktur multi-halaman**

- Header di semua halaman: logo, menu Home, Katalog, Sablon, Galeri, Blog, Tentang, Kontak, tombol Masuk dan Daftar Akun.
- Semua rute publik: `/`, `/katalog`, `/sablon`, `/galeri`, `/blog`, `/tentang`, `/kontak`, `/login`, `/register`, 19 halaman `/produk/<slug>`, 4 halaman `/blog/<slug>`.
- Footer dan tautan di dalamnya.
- Rute yang seharusnya tidak ada (`/cart`, `/checkout`, `/admin`) — diverifikasi menghasilkan 404.

**Login dan register (Google-only)**

- Halaman `/login` dan `/register`: tombol "Lanjutkan dengan Google" dan "Daftar Cepat dengan Google", teks dan janji fitur di halaman register.
- Rute terkunci `/dashboard` dan `/dashboard/pesanan/baru`: perilaku saat dibuka tanpa login (pengalihan ke halaman login).
- Dashboard, tracking pesanan, dan invoice: sudah diuji dengan akun Google tes (lihat inventaris); yang belum bisa diuji: timeline tracking produksi dan invoice, karena keduanya baru muncul setelah ada pesanan.

**Katalog dan produk**

- Katalog 19 produk: nama, harga jual, harga coret, badge diskon, rating, jumlah terjual.
- Pencarian katalog (termasuk pencarian yang tidak menghasilkan apa-apa dan pencarian substring).
- Filter kategori dan sortir harga (rendah ke tinggi, tinggi ke rendah), serta tombol sortir Populer, Terbaru, Terlaris.
- Halaman detail produk: pilihan warna dan ukuran, jumlah, tombol Pesan Sekarang, link Beli di Shopee.

**Sablon, galeri, blog**

- Kalkulator DTF dan tabel pricelist di `/sablon` (semua ukuran: Logo, A6+, A5, A4, A3).
- Galeri `/galeri`: filter kategori dan lightbox.
- Blog `/blog`: daftar artikel dan halaman artikel (termasuk keaktualan tanggal).

**Alur order dan tautan keluar**

- Tombol Pesan Sekarang di hero dan di halaman produk (diperiksa href-nya saja, pesan WhatsApp tidak dikirim).
- Tautan WhatsApp, Instagram (@yajaya.id), TikTok (@yajaya.store), dan Shopee (shopee.co.id/yajaya.id).
- Informasi pembayaran di `/kontak` (Bank Transfer, QRIS, E-Wallet).

**Konsistensi konten dan harga**

- Harga produk di kartu katalog vs halaman detail vs kategori Home vs pricelist.
- Nama produk, warna, dan ukuran yang ditawarkan.
- Teks di footer, judul halaman, dan tanggal artikel blog.

**Pengujian non-fungsional dari luar**

- Usability: kemudahan navigasi, kejelasan tombol dan label, konsistensi tampilan.
- Compatibility: Chrome, Firefox, Edge; desktop dan mobile (360px, 768px).
- Performance: response time, throughput, error rate (Apache JMeter).
- Security eksternal: header keamanan HTTP dan validasi input dasar pada form login/input (OWASP ZAP + uji input manual).

### 2.2 Out-of-Scope — yang TIDAK diuji

| Item | Alasan |
|---|---|
| White-box testing (statement/branch/path coverage) | Butuh akses source code; sudut pandang proyek ini murni eksternal |
| Code-level unit testing | Menguji fungsi di level kode, bukan perilaku yang terlihat pelanggan |
| Pengujian database, API internal, dan backend | Tidak terlihat dari antarmuka pengguna |
| Penetration testing penuh | Di luar cakupan tugas; yang dilakukan hanya DAST dasar dan uji input eksternal |
| Cart, checkout, dan pembayaran on-site | Fitur ini tidak ada di website |
| Form order/kontak dan validasi form email/password | Tidak ada kolom isian seperti itu di website (login hanya lewat Google) |
| Pengiriman pesan WhatsApp dan pembelian lewat Shopee | Percakapan dan transaksi berada di luar website |
| Pengujian kode hasil perubahan selama pengujian | Setiap perubahan website selama pengujian harus dicek ulang dulu sebelum laporan final |

## 3. Kriteria Masuk (Entry Criteria) & Kriteria Keluar (Exit Criteria)

### 3.1 Entry Criteria — pengujian boleh dimulai bila:

1. Website <https://www.yajaya.store/> bisa diakses dan mengembalikan HTTP 200.
2. Inventaris website yang diuji sudah selesai dan didokumentasikan ([00-docs/site-inventory-2026-11-20.md](../00-docs/site-inventory-2026-11-20.md)).
3. Test plan ini sudah dibaca oleh tim (persetujuan formal di bagian 9).
4. Lingkungan pengujian sudah siap: browser Chrome, Firefox, dan Edge; perangkat desktop dan mobile; akses internet stabil.
5. Daftar test case manual sudah ditulis dan diberi ID serta prioritas.

### 3.2 Exit Criteria — pengujian dinyatakan selesai bila:

1. Semua test case manual prioritas High sudah dieksekusi, dan hasilnya tercatat di log eksekusi.
2. Semua defect yang ditemukan sudah dilaporkan di dokumen bug report dengan severity, priority, langkah reproduksi, dan status.
3. Test otomatis (Cypress E2E smoke, JMeter, dan ZAP baseline scan) sudah dijalankan, atau statusnya dicatat sebagai belum dijalankan.
4. Test report sudah berisi verdict akhir berdasarkan kerangka ISO/IEC 25040:2024.
5. Wawancara dengan QA/tester berpengalaman minimal 3 tahun sudah dilakukan dan transkripnya sudah diisi, atau statusnya dicatat sebagai belum dilakukan.

### 3.3 Kriteria penangguhan (Suspension Criteria)

Pengujian dihentikan sementara bila website tidak bisa diakses (HTTP 5xx atau down lebih dari 1 jam), atau bila pemilik website mengubah versi yang diuji di tengah jalan. Dalam kedua kasus itu, yang sudah dikerjakan dicatat apa adanya dan pengujian dilanjutkan setelah kondisi pulih atau inventaris diperbarui.

## 4. Sumber Daya (Resources)

### 4.1 Peran (Roles)

| Peran | Tanggung jawab |
|---|---|
| Test Lead / penulis laporan | Menyusun test plan, test case, dan test report; mengoordinasikan eksekusi; menulis verdict akhir |
| Manual Tester (anggota kelompok) | Mengeksekusi test case manual, mencatat actual result, melaporkan defect |
| Automation Tester (anggota kelompok) | Menulis dan menjalankan skrip Cypress, JMeter, dan ZAP baseline scan |
| Reviewer (anggota kelompok) | Memeriksa test case, bug report, dan test report sebelum push ke GitHub |
| Narasumber wawancara | QA/tester profesional dengan pengalaman minimal 3 tahun (diwawancarai, bukan anggota tim penguji) |
| Pemilik website (Yajaya Store) | Stakeholder eksternal; menerima laporan defect dan rekomendasi perbaikan |

Catatan: laporan ini adalah tugas kelompok. Setiap anggota harus tercatat sebagai contributor di repository GitHub. Karena itu tidak ada push yang dilakukan tiba-tiba tanpa sepengetahuan anggota lain (lihat bagian 9).

### 4.2 Hardware

| Item | Spesifikasi minimal |
|---|---|
| Laptop/PC penguji | Prosesor dual-core, RAM 8 GB, layar 1366×768 atau lebih besar |
| Perangkat mobile | Smartphone Android atau iOS, viewport 360px (untuk pengujian responsif) |
| Koneksi internet | Stabil, cukup untuk memuat halaman dan menjalankan JMeter |

### 4.3 Software / Tools

| Tool | Kegunaan | Status |
|---|---|---|
| Google Chrome, Mozilla Firefox, Microsoft Edge | Browser pengujian manual dan compatibility testing | Tersedia |
| Cypress | Automation E2E: login, navigasi, katalog | Rencana (Tahap 6), belum dieksekusi |
| Apache JMeter | Performance testing: load, stress, spike | Rencana test case (Tahap 6), belum dieksekusi |
| OWASP ZAP | Security DAST: baseline scan, header keamanan, uji input | Rencana (Tahap 6), belum dieksekusi |
| Node.js | HTTP smoke test (pengganti sementara saat Playwright gagal) | Tersedia, hasil 5/5 lolos |
| GitHub | Repository laporan, 1 direktori, riwayat commit sebagai bukti progress | Tersedia, publik |
| Google Sheets / Markdown | Log eksekusi dan pencatatan defect | Tersedia |

Catatan soal Playwright: Playwright sempat dipakai untuk otomatisasi E2E, tetapi instalasi browsernya gagal 3 kali di mesin ini (download dari CDN putus di sekitar 90 persen). Karena itu otomatisasi E2E pindah ke Cypress. Skrip Playwright lama tetap disimpan di `automation/` sebagai arsip.

## 5. Strategi Pengujian (Test Strategy)

Strategi pengujian proyek ini mengikuti ISO/IEC/IEEE 29119-1:2022 (konsep) dan ISO/IEC/IEEE 29119-5:2024 (keyword-driven untuk otomatisasi), dengan penilaian kualitas menurut ISO/IEC 25010:2023.

### 5.1 Pengujian manual — 3 kategori (tanpa kode)

**Kategori 1 — Functional Testing (Black-Box).** Menguji apakah setiap fungsi berjalan sesuai spesifikasi yang terlihat dari luar. Teknik yang dipakai mengikuti ISO/IEC/IEEE 29119-4:2021 sebagai acuan teknik (edisi 2021, lihat catatan di atas): Equivalence Partitioning (misalnya rentang harga, ukuran, jumlah), Boundary Value Analysis (misalnya jumlah minimum 1, ukuran terbesar dan terkecil), dan Decision Table (misalnya kombinasi filter kategori dan sortir). Mencakup positive testing (input benar) dan negative testing (input salah atau kosong) untuk login, navigasi halaman, katalog/filter/pencarian, detail produk, dan order.

**Kategori 2 — Non-Functional Manual Testing (Usability & Compatibility).** Menguji kemudahan pemakaian dan konsistensi tampilan: apakah navigasi mudah dimengerti, apakah tombol dan label jelas, apakah tampilan konsisten di Chrome, Firefox, dan Edge, serta di layar desktop dan mobile. Karakteristik ISO/IEC 25010:2023 yang dinilai di sini: interaction capability dan sebagian reliability.

**Kategori 3 — User Acceptance Testing (UAT / Beta Testing) & Basic Input Security.** Menguji alur bisnis end-to-end dari sudut pandang pelanggan nyata: dari membuka website, mencari produk, sampai memesan lewat WhatsApp. Dilengkapi kuesioner kepuasan pengguna skala Likert. Di kategori yang sama dilakukan uji input keamanan eksternal dasar pada form login dan kolom input: SQL Injection (`' OR '1'='1`) dan XSS (`<script>alert(1)</script>`) — hanya untuk melihat bagaimana website merespons input berbahaya, tanpa merusak data atau sistem.

### 5.2 Pengujian otomatis (Automation)

| Lapisan | Tool | Cakupan |
|---|---|---|
| E2E | Cypress | Login valid dan invalid, navigasi antar halaman, katalog dan filter |
| Performance | Apache JMeter | Load (50–100 user), stress (200–500 user), spike (lonjakan 10 ke 200 user); metrik response time, throughput, error rate |
| Security DAST | OWASP ZAP | Baseline scan, pemeriksaan header keamanan HTTP, pemindaian pasif dan aktif pada halaman publik |

Skrip otomatisasi direncanakan di Tahap 6 dan belum dieksekusi. Hasil eksekusinya akan diisi di test report setelah dijalankan.

### 5.3 Karakteristik kualitas yang dinilai (ISO/IEC 25010:2023)

| Karakteristik | Prioritas | Cara dinilai |
|---|---|---|
| Functional Suitability | Tinggi | Test case Kategori 1 + Cypress E2E |
| Interaction Capability | Tinggi | Test case Kategori 2 (usability & compatibility) |
| Reliability | Tinggi | Konsistensi hasil di semua browser |
| Performance Efficiency | Sedang | JMeter (response time, throughput, error rate) |
| Security | Sedang | DAST ZAP + uji input dasar Kategori 3 |
| Maintainability, Flexibility, Safety | Tidak dinilai | Butuh akses kode dan infrastruktur |

### 5.4 Alasan manual + otomatis dipakai bersamaan

Kurmaku dkk. (2022) melakukan meta-analisis terhadap 21 studi dan menyimpulkan testing otomatis lebih hemat biaya, coverage, dan waktu, tetapi testing manual sama baiknya, bahkan sedikit lebih baik, dalam menemukan fault — dan bedanya tidak signifikan secara statistik. Karena itu proyek ini memakai keduanya: manual untuk menemukan masalah yang butuh penilaian manusia (tampilan, konsistensi konten, alur bisnis), otomatis untuk mengulang skenario yang sama secara konsisten.

### 5.5 Pengujian API (terbatas)

Pengujian API di proyek ini terbatas pada level HTTP, karena website tidak menyediakan API publik. Pengecekan tanggal 28 November 2026 ke endpoint `/api/auth/session`, `/api/products`, `/api/orders`, `/api/health`, `/api-docs`, dan `/openapi.json` semuanya mengembalikan 404 — tidak ada endpoint API, tidak ada dokumentasi API, dan tidak ada spesifikasi OpenAPI/Swagger yang bisa diuji.

Yang masih bisa diuji dari sisi API: request GET dan kode status HTTP halaman (200 untuk halaman yang ada, 404 untuk `/cart`, `/checkout`, dan `/admin`), redirect dashboard ke halaman login kalau belum login, dan header respons (Content-Type, Strict-Transport-Security). Pengecekan ini sudah tercakup di HTTP smoke test.

Yang tidak bisa diuji: POST, PUT, dan DELETE, operasi CRUD, validasi body JSON, token autentikasi, dan error handling 400/401 — karena endpointnya memang tidak ada. Penyebabnya: data produk ditulis langsung di frontend, pemesanan lewat WhatsApp, dan login memakai Google OAuth (API milik Google, bukan milik website). Karena itu pengujian API fungsional, keamanan API, dan beban di level API tidak dapat dilakukan di proyek ini; pengujian kinerja dan keamanan tetap dilakukan di level halaman lewat JMeter dan ZAP (lihat 5.2).

## 6. Jadwal dan Milestone

Deadline pengumpulan laporan: **Sabtu, 5 Desember 2026**. Aturan pacing dari dosen: progress di GitHub harus terlihat setiap 1–2 hari (kotak kontribusi hijau menyala), jadi pekerjaan dipecah per batch dan tidak di-push sekaligus.

| Milestone | Target | Status |
|---|---|---|
| Inventaris website | 20 Nov 2026 | Selesai |
| Tahap 1: README + referensi | 20 Nov 2026 | Selesai |
| Tahap 2: test plan (dokumen ini) | 20 Nov 2026 | Selesai |
| Tahap 3 audit: test case manual | 28–29 Nov 2026 | Selesai (di-push 27 Nov 2026) |
| Tahap 4 audit: bug report | 28–29 Nov 2026 | Selesai (di-push 27 Nov 2026) |
| Tahap 5: test report | 29–30 Nov 2026 | Belum dimulai |
| Tahap 6: automation (Cypress, JMeter, ZAP) | 30 Nov–2 Des 2026 | Belum dimulai |
| Tahap 7: wawancara QA/tester | 30 Nov–2 Des 2026 | Belum dimulai (butuh narasumber) |
| Eksekusi formal test case + retest | 2–4 Des 2026 | Belum dimulai |
| Finalisasi laporan + push terakhir | 4–5 Des 2026 | Belum dimulai |

Jadwal di atas adalah rencana. Kalau wawancara belum dapat narasumber, bagian yang tertunda dicatat sebagai belum dilakukan atau `Blocked` di laporan, bukan diisi dengan hasil karangan.

## 7. Risiko dan Mitigasi

| # | Risiko | Dampak | Mitigasi |
|---|---|---|---|
| R1 | Website berubah selama pengujian | Inventaris dan test case kedaluwarsa | Setiap perubahan website dicek ulang dulu sebelum laporan final |
| R2 | Dashboard butuh akun Google asli, tidak ada akun demo | Invoice belum bisa diuji | Dashboard sudah diuji dengan akun Google tes; invoice ditulis sebagai keterbatasan, bukan defect |
| R3 | Narasumber wawancara belum ada | Syarat wawancara tidak terpenuhi | Cari narasumber lebih awal lewat jaringan kampus dan komunitas; bila sampai akhir belum ada, panduan wawancara tetap dilampirkan dan transkrip ditulis setelah wawancara dilakukan |
| R4 | Instalasi browser/tool otomatisasi gagal (pernah terjadi pada Playwright) | Otomatisasi tertunda | Siapkan fallback: HTTP smoke test (Node) untuk pemeriksaan dasar; jalankan Cypress/JMeter di mesin lain bila perlu |
| R5 | Anggota kelompok tidak tercatat sebagai contributor | Penilaian kelompok bermasalah | Semua push dikoordinasikan dulu; pembagian tugas dan username GitHub anggota dicatat sebelum push berikutnya |
| R6 | Pengujian mobile belum dilakukan | Defect responsif tidak ketahuan | Alokasikan sesi khusus mobile (360px, 768px) sebelum finalisasi |
| R7 | Hasil eksekusi dikarang karena dikejar deadline | Integritas laporan rusak | Aturan keras: bagian yang belum dieksekusi dibiarkan kosong dan tidak boleh diisi angka karangan |

## 8. Alur Kerja & Proses Pelaporan Defect

### 8.1 Alur kerja pengujian

1. Tester memilih test case dari dokumen test case manual berdasarkan prioritas.
2. Tester menjalankan langkah-langkahnya di lingkungan yang dicatat (browser, ukuran layar, tanggal).
3. Hasil aktual ditulis di log eksekusi dengan status Pass, Fail, atau Blocked.
4. Kalau Fail, tester membuat laporan bug di dokumen bug report dengan format di bawah.
5. Reviewer memeriksa test case dan bug report sebelum di-push ke GitHub.

### 8.2 Format laporan bug

Setiap bug wajib berisi: Bug ID, judul, severity (1 Critical s.d. 5 Trivial), priority (1 Critical s.d. 4 Low), langkah reproduksi (steps to reproduce), expected result vs actual result, environment (browser, ukuran layar, tanggal), status dalam Bug Life Cycle, dan bukti (screenshot atau tautan) bila ada.

### 8.3 Bug Life Cycle

```
New → Assigned → Open → Fixed → Pending Retest → Retest → Verified → Closed
```

- **New:** bug baru dilaporkan, belum ditinjau.
- **Assigned:** bug ditugaskan ke anggota tim untuk ditindaklanjuti (dalam konteks tugas ini: ditinjau dan dikonfirmasi ulang).
- **Open:** bug dikonfirmasi dan sedang dikerjakan/ditunggu perbaikan pemilik website.
- **Fixed:** pemilik website menyatakan sudah diperbaiki (atau tester memverifikasi perbaikannya di versi baru).
- **Pending Retest:** menunggu pengujian ulang setelah perbaikan.
- **Retest:** pengujian ulang sedang dilakukan.
- **Verified:** pengujian ulang memastikan bug sudah hilang.
- **Closed:** bug ditutup setelah terverifikasi.

Kondisi khusus:

- **Re-opened:** bug yang sudah Closed ternyata muncul lagi — kembali ke Open.
- **Duplicate:** bug yang sama dengan bug lain yang sudah dilaporkan — ditutup sebagai duplikat dengan rujukan ke Bug ID aslinya.
- **Rejected:** laporan yang setelah ditinjau ternyata bukan defect (misalnya perilaku yang memang disengaja) — ditutup dengan alasan.
- **Deferred:** bug yang diakui tetapi perbaikannya ditunda ke luar cakupan tugas ini — dicatat dengan alasan penundaannya.

Catatan: karena tim penguji adalah mahasiswa dan pemilik website adalah pihak eksternal, status `Fixed` dan `Closed` hanya bisa dicapai bila pemilik website benar-benar memperbaiki dan tester memverifikasi perbaikannya di website live. Bug yang belum diperbaiki pemiliknya tetap berstatus `Open` di laporan akhir — itu bukan kegagalan, itu temuan.

## 9. Persetujuan dan Stakeholder

| Peran | Nama / pihak | Persetujuan |
|---|---|---|
| Anggota kelompok 1 | Mohamad Taufik Wibowo (opikbtk) |  |
| Anggota kelompok 2 | Riyan Hidayat (eriyeaenn) |  |
| Anggota kelompok 3 | Willy Saputro (willysappp) |  |
| Dosen pengampu Testing & QA | Asep Erlan Maulana, S.Kom., M.Kom. |  |
| Pemilik website (Yajaya Store) | Pemilik toko (stakeholder eksternal, penerima rekomendasi) | Tidak diminta persetujuan formal — menerima laporan defect dan rekomendasi |

Aturan kolaborasi (tugas kelompok):

- Tidak ada push ke GitHub yang dilakukan tiba-tiba. Setiap push dikoordinasikan dulu dengan anggota kelompok supaya semua anggota tercatat sebagai contributor.
- Pesan commit ditulis singkat dan deskriptif (contoh: "Update test plan", "Tambah test case").
- Setiap bagian laporan ditulis dengan bahasa sendiri, bukan disalin mentah dari template.
