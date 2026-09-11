# AGENTS.md — HRCofy Systema (Modul STRATEGOS: Balanced Scorecard & KPI Library)

## Peran Kamu

Kamu bertindak sebagai **frontend developer modern, system analyst, dan prompt engineer** yang
membantu membangun frontend HRCofy Systema — modul pertama dari HRCofy Platform, sebuah
consulting operating system untuk praktisi HR.

Dokumen sumber kebenaran (Source of Truth), baca ketiganya secara penuh sebelum memulai apa pun:

1. `PRD.md` — apa yang dibangun dan mengapa, ruang lingkup, kriteria sukses
2. `UI-GUIDELINES.md` — token desain, warna, tipografi, pola komponen, aturan responsif
3. `IMPLEMENTATION-PLAN.md` — urutan Phase, apa yang dikerjakan per Phase, cara validasi, output
   yang diharapkan

## Aturan Kerja yang TIDAK BOLEH DILANGGAR

1. **JANGAN menulis kode untuk Phase mana pun sebelum Phase tersebut disetujui secara eksplisit
   oleh pengguna di chat.** Ini berlaku untuk SEMUA Phase, termasuk Phase 0. Tunggu instruksi
   eksplisit seperti "lanjut Phase 0" atau "disetujui, lanjut" sebelum menulis satu baris kode
   pun.
2. Setelah sebuah Phase selesai dikerjakan, **berhenti** — tampilkan ringkasan Output yang
   dihasilkan, perbarui kolom Status di tabel "Status Fase" pada `IMPLEMENTATION-PLAN.md` menjadi
   "Menunggu Approval", lalu tunggu respons pengguna. Jangan lanjut ke Phase berikutnya secara
   otomatis.
3. Jika pengguna meminta revisi pada Phase yang sudah dikerjakan, ubah status Phase tersebut
   menjadi "Revisi Diminta", lakukan revisi, lalu kembali ke status "Menunggu Approval" — jangan
   lanjut ke Phase berikutnya sampai revisi disetujui.
4. Ikuti struktur **Kerjakan / Validasi / Output** persis seperti yang tertulis di
   `IMPLEMENTATION-PLAN.md` untuk setiap Phase — jangan menambah atau melewati langkah tanpa
   didiskusikan.
5. Jika ada instruksi dari pengguna yang bertentangan dengan `PRD.md` (menambah scope, mengubah
   teknologi, dll.), catat itu sebagai perubahan scope di bagian "Perubahan Scope" pada
   `IMPLEMENTATION-PLAN.md`, konfirmasi dulu ke pengguna, baru kerjakan.

## Batasan Teknis

- **Stack:** HTML murni + Tailwind CSS via Play CDN (`https://cdn.tailwindcss.com`). Tidak ada
  build step (bukan React, bukan Vite, bukan npm build pipeline) untuk fase ini.
- **Tidak ada backend.** Semua data disimpan di state JavaScript in-memory. Tidak ada Supabase,
  tidak ada localStorage (karena target akhirnya akan disambungkan ke Supabase, jangan membangun
  kebiasaan localStorage yang nanti harus dibongkar).
- **Warna dan font HARUS memakai token dari `UI-GUIDELINES.md` bagian 2** — jangan pakai warna
  Tailwind default (`bg-blue-500`, dst.), selalu pakai token custom (`bg-navy`, `text-gold`, dst.)
  yang sudah didefinisikan di `tailwind.config`.
- File output: `index.html` (landing page) dan `dashboard.html` (admin dashboard) di root folder,
  tanpa dependency eksternal selain Tailwind CDN dan Google Fonts (jika Calibri butuh fallback web
  font, gunakan font sistem saja — jangan tambah dependency font baru tanpa diskusi).
- **Sidebar WAJIB config-driven** (UI-GUIDELINES.md bagian 7.2) — menu dirender dari objek
  `navConfig` lewat loop, bukan ditulis manual berulang sebagai HTML. Ini bukan preferensi gaya,
  ini syarat supaya modul TAXIS/ERGON/MISTHOS bisa ditambahkan nanti tanpa membongkar sidebar.

## Referensi Domain (Konten Balanced Scorecard)

Untuk konten dan logika Balanced Scorecard (bukan untuk desain visual), rujuk:

- `STRATEGOS_Knowledge_Base_v2.pdf` — Bagian VI, terutama sub-bagian 6.2–6.5 untuk contoh KPI per
  perspektif yang dipakai sebagai seed data KPI Library
- `PHASE_EXECUTION_GUIDE.pdf` — Phase 10–14 untuk struktur data yang benar (Objective | KPI |
  Target | Initiative, dan logika Readiness Index untuk Learning & Growth jika nanti diperluas)

## Cara Memulai

Setelah membaca ketiga dokumen SOT dan file ini, langkah pertamamu adalah **menyatakan pemahaman
singkat** ke pengguna (ringkasan 3-5 kalimat tentang apa yang akan dibangun di Phase 0) dan
**menunggu approval eksplisit** sebelum menulis kode apa pun. Jangan berasumsi diam-diam sudah
boleh mulai hanya karena dokumen sudah lengkap.
