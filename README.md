# /write — Skill Penulisan Gabungan Maksimal

Skill agen AI yang menggabungkan **seluruh skill penulisan, humanisasi, dan
format dokumen** menjadi satu jalur kerja. Mengetik `/write` berarti memanggil
semuanya sekaligus, masing-masing bekerja pada tahapnya, untuk menghasilkan
tulisan yang serapi mungkin dan semanusiawi mungkin.

Dibuat oleh Rahmat Rayhan (Matt) bersama Muse (Genm), 9 November 2026.

## Cara pakai

Di percakapan dengan agen yang sudah memasang skill ini, ketik:

```text
/write susun latar belakang proposal saya
/write rapikan bab ini
/write buat abstrak dari naskah berikut
```

Mode `/write` berlaku untuk tugas pada pesan itu.

## Jalur kerja

1. **Riset** — `pop-scholar-search`: pencarian literatur akademik
   (OpenAlex, Crossref, PubMed diutamakan; Google Scholar fallback).
2. **Draf** — `naskah-id` untuk karya ilmiah Bahasa Indonesia (EYD V, KBBI,
   kalimat efektif) atau `anti-slop-writing-id` untuk teks Indonesia umum.
3. **Penatural berlapis** — `anti-ai-writer` menaturalkan Bahasa Indonesia;
   `humanizer` (blader) memeriksa 26 pola tulisan AI dari Wikipedia
   "Signs of AI writing" (penuh untuk teks Inggris, pola strukturalnya untuk
   teks Indonesia); `antislop` + `antislop-copywriting` menyaring sisa generik.
4. **Format dokumen** — `docx_exemplar_propagation` menerapkan format berkas
   contoh acuan pada dokumen Word sejenis.
5. **Poles akhir** — `clean-user-facing-text`; `remove-ai-marks` bila
   keluarannya berkas.
6. **Prompt (kondisional)** — `prompt-master` hanya bila tugasnya menyusun
   atau memperbaiki prompt untuk tool AI tertentu.

## Skill anggota yang dibutuhkan

Skill ini adalah *pengorkestra*: ia membaca dan menjalankan skill-skill
anggota yang harus sudah terpasang di `~/workspace/custom-skills/`:

| Skill | Sumber |
| --- | --- |
| naskah-id | https://github.com/nothinx/naskah-id |
| anti-ai-writer | https://github.com/mchardyan/anti-ai-writer |
| humanizer | https://github.com/blader/humanizer |
| antislop + antislop-copywriting | https://github.com/miqdadbadjuber/anti-slop |
| clean-user-facing-text + remove-ai-marks | https://github.com/guillaumemeyer/watermarks-remover |
| anti-slop-writing-id | terpasang lokal (belum ada repo publik terverifikasi) |
| pop-scholar-search | terpasang lokal (belum ada repo publik terverifikasi) |
| docx_exemplar_propagation | skill lokal |
| prompt-master | https://github.com/nidhinjs/prompt-master |

## Pemasangan

Salin folder skill ini ke folder skill agen Anda, misalnya:

```bash
git clone https://github.com/rahmatrayhan1905-prog/write-skill.git
cp -r write-skill ~/workspace/custom-skills/write   # sesuaikan dengan agen Anda
```

Pastikan kesembilan skill anggota di atas juga terpasang, karena `/write`
memanggil mereka pada tahapnya masing-masing.

## Aturan keras

- Lapisan penatural **tidak pernah** mengubah fakta, angka, nama, atau
  sitasi, dan **tidak boleh** mengarang rujukan. Kekurangan data ditandai
  `[PERLU DATA: …]` / `[PERLU RUJUKAN: …]`.
- Tidak ada janji lolos detektor AI. Semua skill anggota sendiri menegaskan
  hal yang sama: hasilnya tulisan yang lebih rapi dan lebih natural, bukan
  "terbukti manusia".
- Prioritas saat aturan bertabrakan: fakta & sitasi sumber → kebakuan
  naskah-id → suara alami penulis → pola humanizer → gaya lain.
