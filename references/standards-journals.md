# Standar dan jurnal yang kami pakai

Catatan ini kami tulis tanggal 7 November 2026, setelah mengecek katalog ISO dan IEEE satu per satu. Jadi tahun dan status di bawah ini bukan dari ingatan, melainkan hasil cek langsung waktu itu.

## Standar utamanya

Kami memakai seri ISO/IEC/IEEE 29119 sebagai kerangka kerja pengujian. Bagian 1 edisi 2022 berisi konsep dan istilah dasarnya. Bagian 2 edisi 2021 mengatur proses pengujiannya, dari perencanaan sampai pelaporan. Bagian 3 edisi 2021 berisi format dokumen pengujian, dan ini yang kami pakai untuk test plan, test case, dan laporan akhir. Bagian 4 edisi 2021 berisi teknik perancangan test case, termasuk black-box, white-box, dan experience-based. Bagian 5 edisi 2024 berisi keyword-driven testing, dan ini yang kami pakai untuk pengujian otomatis.

Satu hal yang perlu hati-hati di sini: Bagian 2, 3, dan 4 edisi terkininya memang tahun 2021, bukan 2022. Edisi itu masih berlaku dan belum diganti sampai kami cek, jadi boleh dipakai sebagai edisi yang berlaku di rentang 2022 sampai 2026, tapi jangan ditulis sebagai terbit tahun 2022 di daftar pustaka.

Untuk menilai kualitas produknya kami memakai ISO/IEC 25010:2023, model kualitas SQuaRE yang punya sembilan karakteristik. Dua dokumen pendampingnya, ISO/IEC 25002:2024 dan ISO/IEC 25040:2024, kami pakai untuk menyusun kriteria penilaian dan verdict akhirnya. IEEE 1012-2024 kami pakai sebagai pendukung untuk verifikasi dan validasi.

Ada beberapa standar lama yang sengaja tidak kami pakai karena sudah digantikan: IEEE 829-2008, IEEE 1012-2016, ISO/IEC 25010:2011, dan ISO/IEC/IEEE 12207:2017.

Teks lengkap standar ISO dan IEEE itu berbayar, jadi yang kami kutip di laporan ini hanya halaman katalog dan abstrak resminya. Linknya: https://www.iso.org/contents/data/standard/08/12/81291.html, https://www.iso.org/standard/79428.html, https://webstore.iec.ch/en/publication/90024, dan https://standards.ieee.org/ieee/1012/7324/. Jangan lampirkan PDF bajakan di repo ini.

## Jurnal yang kami pakai

Semua jurnal di bawah ini terbit antara 2022 dan 2026 dan bisa diakses full text secara gratis.

Pertama, Safira dan kawan-kawan di JTIIK 2023. Mereka menguji sistem web dengan kombinasi white-box, black-box, dan UAT, dan UAT-nya dapat 94,67 persen. Polanya mirip sekali dengan rencana pengujian kami. DOI-nya 10.25126/jtiik.2023106891. Peringkat Sintanya belum sempat kami verifikasi, jadi jangan dikutip sebagai Sinta 2 sebelum dicek di portal Sinta.

Kedua, Chrisna dan kawan-kawan di JUTIF 2024. Jurnal ini Sinta 2, sudah kami verifikasi di situs resminya. Mereka memakai white-box dan black-box sekaligus, ditambah otomatisasi pakai Postman dan Katalon, dan cuma 1 dari 23 test case yang gagal. Ini alasan paling kuat kenapa kami membedakan pemakaian white-box dan black-box per level pengujian. DOI-nya 10.52436/1.jutif.2024.5.2.1673.

Ketiga, Caesar dan kawan-kawan di JISBT 2025, dari Universitas Pamulang. Ini yang paling mirip dengan tugas kami: mereka menguji sistem POS berbasis web pakai proses ISO/IEC 29119 dan evaluasi ISO/IEC 25010, dengan 25 test case dan 6 bug, termasuk satu yang Critical. Linknya https://journal.jci.co.id/jisbt/article/download/274/93. Jurnal ini masih baru, volume 1, jadi peringkat Sintanya belum kami temukan dan jangan diklaim.

Keempat, Melyawati dan kawan-kawan tahun 2024. Mereka membandingkan Playwright dan Selenium dengan angka yang terukur: Playwright 4,9 menit, Selenium 8,3 menit, untuk 12 test case yang sama. Ini alasan kami memilih Playwright, bukan sekadar karena lebih suka. DOI-nya 10.47709/cnahpc.v6i3.4362.

Kelima, Kurmaku dan kawan-kawan di ACM/ISEC 2022. Mereka me-meta-analisis 21 studi dan kesimpulannya testing otomatis lebih hemat dari segi biaya, coverage, dan waktu, tapi testing manual hasilnya sama bagusnya, bahkan sedikit lebih baik dalam menemukan fault, dan bedanya tidak signifikan secara statistik. Ini alasan kami memakai manual dan otomatis bersamaan, bukan memilih salah satu. DOI-nya 10.1145/3511430.3511433.

Sebagai pendukung, kami juga mencatat Hafiz dan kawan-kawan di RESTI 2023, Sinta 2 terverifikasi, DOI 10.29207/resti.v7i3.4870; Gupta dan Bathla di IJSRST 2022, DOI 10.32628/IJSRST229657; dan Kumar dan Sagar di IJISAE 2024, https://ijisae.org/index.php/IJISAE/article/view/7130.

Dua catatan terakhir. Pertama, kami tidak menemukan jurnal Sinta 1 untuk topik ini di rentang 2022 sampai 2026. Yang terverifikasi kuat itu Sinta 2. Kedua, ISO 25010 dan ISO 29119 itu standar, bukan jurnal, jadi di laporan jangan ditulis sebagai jurnal Sinta.
