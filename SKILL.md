---
name: write
description: |
  Gabungan maksimal seluruh skill penulisan dan humanisasi milik pengguna.
  Aktif HANYA saat pengguna mengetik "/write" (atau secara eksplisit meminta
  mode /write). Saat aktif, SEMUA skill anggota di bawah WAJIB dibaca dan
  dijalankan berurutan sebagai satu jalur kerja: riset literatur, penulisan
  baku, penatural tulisan, pemeriksaan pola AI, format dokumen, dan poles
  akhir. Tujuannya tulisan serapi mungkin dan semanusiawi mungkin tanpa
  mengubah fakta, angka, atau sitasi, dan tanpa mengarang rujukan.
---

# /write — Jalur Penulisan Gabungan Maksimal

Perintah pengguna (ditetapkan 2026-11-09): mengetik `/write` berarti memanggil
SEMUA skill penulisan, humanisasi, dan format dokumen yang terpasang untuk
bekerja bersama secara maksimal pada tugas penulisan itu. Bukan memilih satu —
semuanya, masing-masing pada tahapnya.

## Skill anggota (semuanya di ~/workspace/custom-skills/)

1. `pop-scholar-search` — pencarian literatur akademik (OpenAlex, Crossref,
   PubMed diutamakan; Google Scholar hanya fallback).
2. `naskah-id` — penulisan karya ilmiah Bahasa Indonesia (EYD V, KBBI,
   kalimat efektif).
3. `anti-slop-writing-id` — teks Indonesia umum: jelas, spesifik, natural.
4. `anti-ai-writer` — penatural tulisan Indonesia: kata/frasa yang dihindari,
   variasi kalimat, suara aktif, cek mandiri sebelum keluaran.
5. `humanizer` (blader/humanizer) — 26 pola tulisan AI dari Wikipedia
   "Signs of AI writing".
6. `antislop` (inti) + `antislop-copywriting` — saringan anti-generik untuk
   teks dan copy.
7. `clean-user-facing-text` — poles akhir teks yang dibaca orang.
8. `remove-ai-marks` — hygiene akhir versi penuh untuk berkas (service lokal
   watermarks-remover, hanya konten milik/berizin pengguna).
9. `docx_exemplar_propagation` — penyebaran format dokumen Word dari berkas
   contoh acuan.
10. `prompt-master` — HANYA bila tugas /write itu sendiri adalah menyusun /
    memperbaiki prompt untuk tool AI tertentu.

## Jalur kerja (jalankan berurutan, jangan melompat)

### Tahap 0 — Tentukan jenis teks
Ilmiah (proposal, skripsi, jurnal, makalah, laporan) atau umum (artikel, esai,
blog, media sosial, surat), bahasa Indonesia atau Inggris, keluaran chat atau
berkas (DOCX/teks). Jenis menentukan skill pemimpin tahap 2.

### Tahap 1 — Riset (bila tugas butuh referensi atau data)
Baca `pop-scholar-search/SKILL.md` dan cari literatur lewat jalur itu.
Referensi yang dipakai harus yang benar-benar ditemukan; JANGAN mengarang
rujukan, DOI, angka, atau kutipan. Kekurangan ditandai
`[PERLU DATA: …]` / `[PERLU RUJUKAN: …]` sesuai kontrak naskah-id.

### Tahap 2 — Susun / sunting draf
Baca `naskah-id/SKILL.md` (teks ilmiah Indonesia — pemimpin tahap ini) atau
`anti-slop-writing-id/SKILL.md` (teks umum Indonesia). Terapkan aturan
permanen pengguna yang relevan, antara lain: latar belakang selalu 7 paragraf
(1–2 fenomena, 3–4 masalah, 5–6 studi terdahulu, 7 tujuan/signifikansi/
urgensi). Angka, hasil, dan sitasi dari sumber TIDAK diubah.

### Tahap 3 — Penatural dan anti-pola-AI (semua lapisan jalan)
Baca dan terapkan berturut-turut:
- `anti-ai-writer/SKILL.md` — penatural utama untuk Bahasa Indonesia.
- `humanizer/SKILL.md` — untuk teks Inggris terapkan penuh 26 polanya; untuk
  teks Indonesia terapkan hanya pola struktural universalnya (panggung
  "bukan X tapi Y", penutup satu baris dramatis, triad paksa, inflasi
  signifikansi, sisa percakapan) — aturan kata khas Inggris TIDAK dipaksakan
  ke Bahasa Indonesia.
- `antislop/SKILL.md` + `antislop-copywriting/SKILL.md` — saring sisa
  generik pada judul, kalimat pembuka, dan seruan.
Fakta, angka, nama, dan sitasi tetap tidak berubah di semua lapisan ini.
Lapisan penatural tidak pernah boleh menambah klaim baru.

### Tahap 4 — Format dokumen (bila keluaran berupa berkas dokumen)
Baca `docx_exemplar_propagation/SKILL.md` dan terapkan format acuan terkunci
pengguna (berkas contoh proposal acuan + panduan terukurnya, penomoran
Keluarga 1) bila dokumennya sejenis. Nilai format diukur dari berkas acuan,
bukan dari ingatan.

### Tahap 5 — Poles akhir
Baca `clean-user-facing-text/SKILL.md` dan poles teks final. Bila keluarannya
berkas, jalankan juga `remove-ai-marks/SKILL.md` sebagai hygiene terakhir,
dengan batasannya: hanya konten milik/berizin pengguna, disclosure wajib
tidak dihapus.

### Tahap 6 — Prompt (kondisional)
Bila tugasnya menyangkut prompt untuk tool AI tertentu, baca
`prompt-master/SKILL.md` dan ikuti kontrak keluarannya.

## Aturan keras

- Tidak ada skill anggota yang boleh mengarang fakta, data, angka, kutipan,
  atau rujukan. Bila lapisan mana pun bertabrakan dengan kejujuran sumber,
  kejujuran menang.
- Urutan prioritas saat aturan bertabrakan: (1) fakta & sitasi sumber,
  (2) naskah-id untuk kebakuan ilmiah Indonesia, (3) suara alami penulis,
  (4) pola humanizer, (5) preferensi gaya lain.
- JANGAN menjanjikan tulisan lolos detektor AI. Tidak satu pun skill anggota
  memberi jaminan itu; sampaikan hasil sebagai tulisan yang lebih rapi dan
  lebih natural, bukan "terbukti manusia".
- Mode /write berlaku untuk tugas pada pesan itu; percakapan berikutnya
  pengguna memanggilnya lagi dengan mengetik /write.
