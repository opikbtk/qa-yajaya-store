# QA Testing — Website yajaya.store

Laporan tugas Testing & QA. Objek: website katalog kaos polos & sablon DTF satuan (UMKM, Parung, Bogor) — https://yajaya.store

## Standar acuan
- ISO/IEC/IEEE 29119-1:2022, 29119-2:2021, 29119-3:2021, 29119-4:2021, 29119-5:2024
- ISO/IEC 25010:2023, ISO/IEC 25002:2024, ISO/IEC 25040:2024
- IEEE 1012-2024 (pendukung)
- Detail + jurnal: `references/standards-journals.md`

## Isi direktori
- `docs/` — inventaris situs 7 Nov 2026
- `test-plan/` — test plan (29119-3)
- `test-cases/` — 40+ test case manual (black-box, grey-box, experience-based; white-box bersyarat akses kode)
- `automation/` — test otomatis Playwright (smoke + regresi, keyword-driven 29119-5:2024) — *dalam pengerjaan*
- `bug-reports/` — 11 kandidat bug dari inventaris
- `interview/` — panduan wawancara QA/tester ≥3 tahun — *narasumber belum ada*
- `references/` — standar & jurnal Sinta 1-3 / internasional 2022-2026

## Status
- Inventaris: selesai 7 Nov 2026
- Test plan & test case manual: draf selesai, eksekusi formal menyusul
- White-box: BLOCKED — butuh akses source code/repo (belum dikonfirmasi)
- Wawancara: BELUM — butuh kandidat narasumber
- Test otomatis: dalam pengerjaan

## Cara menjalankan test otomatis
Lihat `automation/README.md` (setelah dibuat).
