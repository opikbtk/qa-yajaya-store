# Pengujian Website yajaya.store

Repo ini berisi laporan tugas Testing dan QA kami. Website yang diuji adalah yajaya.store, toko online kaos polos dan sablon DTF satuan milik Yajaya Store di Parung, Bogor. Alasan kami memilih website ini sederhana: skalanya masih UMKM, fiturnya tidak terlalu besar, dan ordernya masih lewat WhatsApp, jadi masih masuk akal untuk diuji satu per satu dalam waktu tugas ini.

Pengujian kami mengacu ke standar ISO/IEC/IEEE 29119 seri testing dan ISO/IEC 25010:2023 untuk model kualitas produk. Detail standar dan jurnal yang kami pakai ada di `references/standards-journals.md`.

## Isi repo ini

Folder `docs/` berisi inventaris website hasil penelusuran pertama kami tanggal 7 November 2026. Folder `test-plan/` berisi test plan yang kami susun mengikuti format ISO/IEC/IEEE 29119-3. Folder `test-cases/` berisi test case manual, ada 40 lebih, mencakup black-box, grey-box, dan experience-based. White-box awalnya sempat tertahan karena kami belum punya akses ke source code, tapi sekarang sudah bisa jalan setelah kami berhasil masuk ke repo privatnya dan membaca kodenya.

Folder `automation/` berisi test otomatis. Kami pakai Playwright, tapi instalasi browsernya gagal terus di mesin ini karena download dari CDN-nya putus di sekitar 90 persen, sudah dicoba tiga kali. Jadi untuk sementara yang sudah jalan adalah test otomatis level HTTP pakai Node, hasilnya 5 dari 5 lolos. Script Playwright-nya tetap kami simpan di sini supaya bisa dijalankan di mesin lain.

Folder `bug-reports/` berisi laporan bug yang kami temukan, sekarang sudah 13 bug. Folder `interview/` berisi panduan wawancara untuk QA atau tester yang pengalamannya minimal tiga tahun. Narasumbernya sendiri masih dicari.

## Status sekarang

Inventaris sudah selesai tanggal 7 November 2026. Test plan dan test case manual sudah jadi drafnya, eksekusi formalnya sebagian sudah jalan. White-box sudah dikerjakan, dan dari kode ketahuan penyebab lima bug, termasuk kenapa filter warna dan tombol reset tidak berfungsi. Wawancara masih menunggu narasumber. Test otomatis Playwright masih tertahan masalah download browser, sedangkan test HTTP-nya sudah jalan.

## Menjalankan test otomatis

Untuk test HTTP, cukup jalankan `node http-smoke.js` di dalam folder `automation/`. Untuk test Playwright, caranya ada di `automation/README.md`.
