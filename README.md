# QA Testing — Website yajaya.store

Laporan tugas Testing & QA: pengujian website katalog kaos polos dan sablon DTF satuan milik Yajaya Store, Parung, Bogor. Pengujian dilakukan murni dari sudut pandang pelanggan (external / customer perspective): semua yang diuji adalah antarmuka pengguna, alur bisnis, perilaku HTTP dan performa, serta validasi input dari luar. Tidak ada white-box testing dan tidak ada akses ke source code backend.

Standar acuan: ISO/IEC/IEEE 29119 dan ISO/IEC 25010:2023. Semua standar dan jurnal yang dipakai terbit 2022–2026, lengkapnya di [01-references/standards-journals.md](01-references/standards-journals.md).

## 📋 Identitas Penyusun

### Anggota Kelompok

| No | Nama Mahasiswa | NIM |
|---|---|---|
| 1 | Mohamad Taufik Wibowo | 231011400164 |
| 2 | Riyan Hidayat | 231011400539 |
| 3 | Willy Saputro | 231011401187 |

### Informasi Akademik

| Keterangan | Informasi |
|---|---|
| Kelompok | Kelompok 9 |
| Kelas / Ruang | V.714 |
| Program Studi | Teknik Informatika |
| Fakultas | Ilmu Komputer |
| Perguruan Tinggi | Universitas Pamulang |
| Mata Kuliah | Testing & QA Perangkat Lunak |
| Dosen Pengampu | ASEP ERLAN MAULANA S.KOM., M.KOM |

## Daftar Isi

- [1. Profil Objek Uji](#1-profil-objek-uji)
- [2. Sudut Pandang Pengujian](#2-sudut-pandang-pengujian)
- [3. Alasan Pemilihan Metode](#3-alasan-pemilihan-metode)
- [4. Status Proyek](#4-status-proyek)
- [5. Struktur Repository](#5-struktur-repository)
- [6. Menjalankan Test Otomatis](#6-menjalankan-test-otomatis)

## 1. Profil Objek Uji

**yajaya.store** (<https://www.yajaya.store/>) adalah website milik Yajaya Store, toko kaos polos dan sablon DTF satuan di Jl. H. Mawi No. 12, Waru, Parung, Kabupaten Bogor. Toko ini nyata dan masih aktif: alamat, nomor WhatsApp (0856-8703-266), dan jam buka (Senin–Minggu, 09.00–23.00 WIB) tercantum di website, dan katalognya berisi produk yang benar-benar dijual, lengkap dengan harga dan jumlah terjual.

Website ini memenuhi kriteria tugas karena skalanya menengah ke bawah:

- **Bisnisnya UMKM, bukan portal besar.** Satu toko, satu lokasi, produknya puluhan bukan ribuan. Katalognya berisi 19 produk: kaos polos, kaos distro (Persija, Iron Maiden, Testament, Denzbagus), work jacket, overshirt, hoodie, celana denim, dan jasa sablon DTF.
- **Fiturnya terbatas dan masih bisa diuji satu per satu dalam waktu tugas.** Tidak ada marketplace, tidak ada sistem kasir yang kompleks. Order masih lewat WhatsApp, pembayaran dikonfirmasi lewat chat, dan tidak ada checkout atau pembayaran di website.
- **Dibuat untuk usaha nyata, bukan tugas kuliah atau demo.** Website ini adalah etalase dan kanal order sungguhan untuk toko yang beroperasi. Itu penting: defect yang ditemukan di sini berdampak langsung ke pembeli dan ke pemilik toko, bukan sekadar nilai di atas kertas.
- **Cukup kompleks untuk diuji dengan serius.** Ada multi-halaman, login, pencarian, filter, sortir, kalkulator harga sablon, galeri, dan blog. Cukup luas untuk black-box testing, UAT, regression testing, dan otomatisasi, tetapi tidak sebesar e-commerce umum yang tidak mungkin selesai dalam satu semester.

Website yang diuji adalah website multi-halaman: Home, Katalog, Sablon, Galeri, Blog, Tentang, Kontak, Login, Register, dan Dashboard, dengan 19 halaman detail produk dan 4 halaman artikel blog. Login dan register hanya bisa lewat Google — tidak ada kolom email atau password, dan tidak ada akun demo, jadi dashboard, tracking pesanan, dan invoice ada di balik login. Dashboard sudah diuji dengan akun Google — lihat Status Proyek.

## 2. Sudut Pandang Pengujian

Pengujian di proyek ini dilakukan sebagai **tester dari sisi pelanggan**. Artinya:

- Yang diuji adalah apa yang dilihat dan dilakukan pembeli: membuka halaman, mencari produk, memilih warna dan ukuran, menghitung harga sablon, mengklik tombol, dan mencoba login.
- Yang **tidak** diuji adalah kode sumber, database, API internal, dan unit test di level kode. White-box testing dan code-level unit testing dinyatakan **out-of-scope** di [02-test-plan/test-plan.md](02-test-plan/test-plan.md).

Konsekuensinya, defect yang dilaporkan di sini selalu disertai langkah reproduksi dari antarmuka pengguna, bukan dari baris kode. Kalau sebuah masalah hanya bisa dibuktikan dengan membaca kode, masalah itu tidak dilaporkan sebagai bug di laporan ini.

## 3. Alasan Pemilihan Metode

### Black-Box Testing

Metode utama. Alasannya sederhana: sebagai tester dari sisi pelanggan, satu-satunya yang bisa kami amati adalah perilaku website dari luar. Black-box testing memakai teknik Equivalence Partitioning, Boundary Value Analysis, dan Decision Table untuk menguji login, navigasi, katalog, filter, pencarian, detail produk, dan order — tanpa perlu tahu cara kerja di dalamnya. Jurnal Chrisna dkk. (2024, Sinta 2) menunjukkan kombinasi black-box dengan white-box dan otomatisasi efektif untuk sistem web; di proyek ini porsi white-box-nya diganti dengan pengujian perilaku HTTP dan validasi input eksternal, karena akses kode tidak tersedia.

### UAT / Beta Testing

UAT menguji apakah website ini bisa dipakai oleh pembeli sungguhan untuk menyelesaikan tujuannya: menemukan produk, memahami harga, dan memesan. Skenario UAT di proyek ini adalah alur bisnis end-to-end dari sudut pandang pelanggan nyata, ditambah kuesioner kepuasan skala Likert. Safira dkk. (2023) memakai UAT sebagai penutup pengujian sistem web dan mencapai 94,67% — pola yang sama kami pakai di sini: UAT adalah penentu akhir apakah website layak dipakai, bukan sekadar apakah fiturnya berjalan.

### Regression Testing

Regression testing memastikan fitur yang sudah berjalan tidak rusak setelah ada perbaikan atau update: pencarian, filter, sortir, order WhatsApp, dan konsistensi harga dicek ulang setiap kali website berubah. Ini penting karena website yang masih dikembangkan bisa saja memperbaiki satu hal sambil merusak hal lain tanpa disadari.

### Automation E2E — Cypress

Otomatisasi dipakai untuk skenario yang diulang terus: login, navigasi antar halaman, dan alur katalog. Cypress dipilih karena dirancang khusus untuk pengujian end-to-end di browser, dengan sinkronisasi otomatis dan debugging yang mudah — cocok untuk tim kecil yang menguji alur pelanggan dari luar. García dkk. (2024) membandingkan Cypress dengan Selenium, Puppeteer, dan Playwright; Gosik & Miłosz (2025) membandingkan langsung Cypress dan Playwright dan mencatat trade-off keduanya. Playwright lebih cepat dan lebih hemat memori, tetapi Cypress dipilih di sini karena skenarionya lebih mudah ditulis dan dirawat untuk alur pelanggan. Catatan: skrip Cypress di repo ini masih berupa draf dan belum dieksekusi di lingkungan final (direncanakan, Tahap 6).

### Performance Testing — Apache JMeter

Performance testing mengukur apakah website tetap responsif saat banyak pengunjung datang bersamaan, memakai skenario load testing (50–100 user), stress testing (200–500 user), dan spike testing (lonjakan 10 ke 200 user), dengan metrik response time, throughput, dan error rate. Indrianto (2023) memakai pola yang sama — 50 dan 100 sampel dengan ramp-up 10 detik — dan Annisa dkk. (2026) menunjukkan website yang diuji stabil sampai 200 user bersamaan, lalu menurun di atas 300 user. Target SLA di proyek ini: response time rata-rata di bawah 2 detik. Rencana lengkapnya menyusul (direncanakan, Tahap 6).

### Security Testing — DAST dengan OWASP ZAP

Karena tidak ada akses kode, pengujian keamanan dilakukan dari luar dengan Dynamic Application Security Testing (DAST): OWASP ZAP memindai aplikasi yang sedang berjalan, memeriksa header keamanan HTTP, dan menguji input form login dengan payload dasar seperti SQL Injection (`' OR '1'='1`) dan XSS. DAST menemukan masalah konfigurasi, autentikasi, dan penanganan request yang hanya muncul saat aplikasi berjalan — hal yang tidak bisa ditemukan dari membaca spesifikasi. Panduan lengkapnya menyusul (direncanakan, Tahap 6).

### Kenapa manual dan otomatis dipakai bersamaan

Kurmaku dkk. (2022) me-meta-analisis 21 studi dan menyimpulkan testing otomatis lebih hemat biaya, coverage, dan waktu, tetapi testing manual sama baiknya, bahkan sedikit lebih baik, dalam menemukan fault — dan bedanya tidak signifikan secara statistik. Karena itu proyek ini memakai keduanya: manual untuk menemukan masalah yang butuh penilaian manusia (tampilan, konsistensi konten, alur bisnis), otomatis untuk mengulang skenario yang sama secara konsisten.

## 4. Status Proyek

- **Inventaris website:** selesai. Website multi-halaman, 19 produk, login Google-only, order lewat WhatsApp.
- **Test plan:** selesai, mengikuti inventaris terbaru.
- **Test case manual:** 40 test case sudah ditulis, sebagian sudah dieksekusi saat inventarisasi.
- **Bug report:** 23 bug sudah didokumentasikan (BUG-01 sampai BUG-23), lengkap dengan langkah reproduksi, severity, dan priority.
- **Test otomatis:** HTTP smoke test sudah jalan (5 dari 5 lolos). Otomatisasi E2E pindah ke Cypress (Tahap 6).
- **Dashboard:** sudah diuji dengan akun Google (akun tes 'hansenfarm') — menu, statistik, form order 6 langkah, dan tracking sudah diperiksa. Yang belum bisa diuji: timeline tracking produksi dan invoice, karena keduanya baru muncul setelah ada pesanan.
- **Wawancara:** belum ada narasumber. Panduan wawancara sudah siap; transkrip akan diisi setelah wawancara nyata (Tahap 7).

## 5. Struktur Repository

```
qa-yajaya-store/
├── README.md
├── 00-docs/
│   └── site-inventory-2026-11-20.md        # Inventaris website (multi-halaman, 19 produk, login)
├── 02-test-plan/
│   └── test-plan.md                        # Test plan
├── test-cases/
│   ├── test-cases-manual.md                # Test case manual (40 test case)
│   └── test-execution-log.md               # Log eksekusi test case
├── bug-reports/
│   └── bug-reports.md                      # Bug report (23 bug)
├── 01-references/
│   └── standards-journals.md               # Standar ISO/IEEE & jurnal 2022–2026
├── automation/
│   ├── cypress/                            # (direncanakan, Tahap 6)
│   ├── jmeter/                             # (direncanakan, Tahap 6)
│   └── security-dast/                      # (direncanakan, Tahap 6)
├── interview/
│   └── interview-guide.md                  # Panduan wawancara QA/tester ≥3 tahun
└── test-report/                             # (direncanakan, Tahap 5)
    └── test-report.md
```

Tautan langsung ke file-file utama:

- [Inventaris Website](00-docs/site-inventory-2026-11-20.md)
- [Test Plan](02-test-plan/test-plan.md)
- [Standar & Jurnal](01-references/standards-journals.md)

## 6. Menjalankan Test Otomatis

Test otomatis di proyek ini direncanakan di Tahap 6: Cypress untuk E2E, Apache JMeter untuk performance testing, dan OWASP ZAP untuk security DAST. Panduan instalasi dan eksekusi ada di folder masing-masing setelah Tahap 6 selesai. HTTP smoke test (Node) sudah jalan dengan hasil 5 dari 5 lolos dan akan dijalankan ulang setelah ada perubahan.
