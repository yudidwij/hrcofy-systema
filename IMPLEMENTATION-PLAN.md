# Implementation Plan — HRCofy Systema (Modul STRATEGOS: Balanced Scorecard & KPI Library)

**Status:** Draft untuk approval — belum ada eksekusi kode
**Versi:** 1.0

---

## Aturan Kerja (WAJIB dibaca sebelum Phase 0)

1. **Tidak ada kode yang ditulis untuk sebuah Phase sebelum Phase tersebut secara eksplisit
   di-approve oleh Yudi.** Selesaikan Kerjakan → tampilkan Output → tunggu approval tertulis →
   baru lanjut ke Phase berikutnya.
2. Setiap Phase memperbarui tabel **Status Fase** di bagian paling bawah dokumen ini
   (Belum Mulai / Menunggu Approval / Disetujui / Revisi Diminta).
3. Kalau ada perubahan scope di tengah jalan, catat di bagian "Perubahan Scope" di bawah — jangan
   diam-diam mengubah Phase yang sudah disetujui.
4. Referensi wajib untuk konten domain: `STRATEGOS_Knowledge_Base_v2.pdf` dan
   `PHASE_EXECUTION_GUIDE.pdf` (bagian BSC — Phase 10-14). Referensi wajib untuk tampilan:
   `UI-GUIDELINES.md`. Referensi wajib untuk scope: `PRD.md`.

---

## Phase 0 — Setup & Design Tokens

**Kerjakan:**
- Buat struktur file dasar: `index.html` (landing page), `dashboard.html` (admin dashboard),
  `assets/` (jika perlu ikon/logo lokal)
- Pasang Tailwind Play CDN di kedua file, dengan `tailwind.config` sesuai token warna di
  `UI-GUIDELINES.md` bagian 6
- Buat komponen dasar yang dipakai berulang: navbar, footer — sebagai HTML partial atau minimal
  sebagai referensi yang konsisten di kedua halaman (karena tanpa build step, duplikasi manual
  antar file diperbolehkan, tapi harus identik)

**Validasi:**
- Warna token bisa dipanggil sebagai class Tailwind (`bg-navy`, `text-gold`, dst.) dan tampil
  benar saat diuji di elemen contoh
- Font Calibri (dengan fallback) aktif di seluruh halaman
- Kedua file HTML terbuka tanpa error di browser tanpa server (`file://`)

**Output:** `index.html` dan `dashboard.html` kosong/skeleton dengan navbar+footer, token warna
terpasang dan teruji.

---

## Phase 1 — Landing Page / Company Profile

**Kerjakan:**
- Hero section: headline, subheadline, CTA ke dashboard
- Section 4 pilar (grid Pillar Card sesuai UI-GUIDELINES 3.3) — STRATEGOS aktif, 3 lainnya
  berlabel "Segera"
- Section penjelasan modul Balanced Scorecard & KPI Library (apa itu, untuk siapa, kenapa
  relevan sekarang/Q3-Q4)
- Footer dengan identitas HRCofy (tagline "People. Performance. Protection.", kontak)

**Validasi:**
- Responsif di 3 breakpoint (mobile/tablet/desktop) — cek manual dengan resize browser
- Semua warna dan tipografi sesuai UI-GUIDELINES, bukan default Tailwind (mis. bukan `text-blue-500`
  bawaan, harus `text-blue` custom token)
- CTA hero mengarah ke `dashboard.html`

**Output:** `index.html` lengkap dan bisa didemokan sebagai landing page mandiri.

---

## Phase 2 — Dashboard Shell (Layout & Navigasi)

**Kerjakan:**
- Sidebar navigasi dibangun dari `navConfig` (UI-GUIDELINES 7.2) — JANGAN tulis markup menu
  langsung berulang di HTML, render dari objek config lewat loop JavaScript
- Struktur grouped per pilar (UI-GUIDELINES 7.1): STRATEGOS sebagai group aktif dengan 4 tools
  (hanya Balanced Scorecard & KPI Library yang clickable, 3 lainnya berlabel "Segera"), TAXIS/
  ERGON/MISTHOS sebagai group ter-mute kosong/label "Segera"
- Struktur HTML/CSS sidebar sudah mengakomodasi mode collapse ke depan (UI-GUIDELINES 7.3),
  meski toggle collapse-nya sendiri belum wajib berfungsi di fase ini
- Area konten utama dengan pemilih periode/snapshot (dropdown atau tab, mis. "Q3 2026")
- Placeholder area untuk builder scorecard (diisi di Phase 3)

**Validasi:**
- Sidebar dan konten sepenuhnya berasal dari `navConfig` — coba tambah satu entri tool dummy di
  config dan pastikan otomatis muncul di sidebar tanpa edit markup lain
- Sidebar collapse dengan benar di mobile (hamburger/bottom-nav sesuai UI-GUIDELINES 4), dan
  render dari `navConfig` yang sama dengan versi desktop (tidak ada markup terpisah/duplikat)
- Item pilar non-aktif terlihat jelas disabled (bukan sekadar warna beda, ada indikator "Segera")
- Pemilih periode berfungsi secara UI (state berpindah), meski belum ada logika penyimpanan

**Output:** `dashboard.html` dengan shell lengkap, siap diisi konten builder.

---

## Phase 3 — Builder Scorecard (Input Objective & KPI)

**Kerjakan:**
- 4 Perspective Card (UI-GUIDELINES 3.5) — Financial, Customer, Internal Process, Learning & Growth
- Di dalam tiap card: form tambah Objective, dan di dalam Objective form tambah KPI (nama, unit,
  weight, target, actual) — sesuai UI-GUIDELINES 3.7
- Tombol edit/hapus per Objective dan per KPI
- Validasi visual: indikator total weight per perspektif (harus 100%), warning jika belum sesuai

**Validasi:**
- User bisa menambah, mengedit, menghapus Objective dan KPI tanpa reload halaman (state JS lokal)
- Validasi total weight per perspektif berfungsi dan pesan errornya jelas (lihat contoh pesan di
  UI-GUIDELINES 3.7)
- Form tidak menerima input tidak valid (mis. weight negatif, target 0 untuk perhitungan skor)

**Output:** Builder scorecard fungsional untuk keempat perspektif, data tersimpan di state
JavaScript (belum persisten antar reload).

---

## Phase 4 — Scoring Engine (Kalkulasi Deterministik)

**Kerjakan:**
- Implementasi fungsi murni JavaScript (terpisah dari logika UI, di file/section tersendiri):
  - Skor per KPI = (actual ÷ target) × 100, clamp 0–120
  - Skor per perspektif = rata-rata tertimbang skor KPI sesuai weight masing-masing
  - Skor total scorecard = rata-rata tertimbang 4 skor perspektif
  - Status RAG: merah <80, kuning 80–99, hijau ≥100 (sesuai PRD dan Knowledge Base)
- Sambungkan hasil kalkulasi ke tampilan real-time — begitu actual/target/weight diubah, skor
  ter-update otomatis tanpa perlu tombol "hitung"

**Validasi:**
- Uji dengan minimal 3 skenario data (semua di atas target, campuran, semua di bawah target) —
  hasil skor dan RAG sesuai ekspektasi manual
- Fungsi kalkulasi tidak bergantung pada DOM — bisa diuji terpisah (mis. dipanggil dari console
  browser dengan input manual dan hasilnya benar)

**Output:** Scoring engine berfungsi, terhubung ke seluruh builder dari Phase 3.

---

## Phase 5 — Visualisasi Ringkasan (Stat Callout & RAG)

**Kerjakan:**
- Stat Callout skor total scorecard (UI-GUIDELINES 3.6) di bagian atas dashboard
- RAG Badge (UI-GUIDELINES 3.8) di setiap Perspective Card dan di sidebar summary (opsional badge
  kecil di item "Balanced Scorecard")
- Panel referensi KPI Library — tampilkan seed data KPI contoh per perspektif dari Knowledge Base
  Bagian 6.2–6.5 (F1–F4, Customer value proposition, P1–P4, L1–L3), bisa collapse/expand agar
  tidak mengganggu layar utama

**Validasi:**
- Stat callout dan semua RAG badge ter-update otomatis mengikuti perubahan skor dari Phase 4
- Panel KPI Library tidak auto-mengisi form (hanya referensi visual, sesuai PRD — bukan AI
  recommendation di fase ini)

**Output:** Dashboard lengkap dengan ringkasan visual skor real-time.

---

## Phase 6 — Responsif & Aksesibilitas — Polish Akhir

**Kerjakan:**
- Review seluruh halaman (index.html + dashboard.html) di 3 breakpoint
- Cek kontras warna sesuai UI-GUIDELINES 5, khususnya teks muted
- Pastikan semua elemen interaktif punya visible focus state
- Pastikan RAG tidak hanya mengandalkan warna (tambahkan teks/label status)

**Validasi:**
- Tidak ada elemen yang terpotong/overflow di mobile
- Tab-navigation (keyboard) bisa menjangkau semua elemen interaktif secara logis

**Output:** Kedua halaman final, siap didemokan ke klien.

---

## Phase 7 — Review & Handoff

**Kerjakan:**
- Ringkasan apa yang sudah dibangun vs PRD (checklist in-scope items)
- Catatan known limitations (data tidak persisten, belum ada backend, dst.)
- Rekomendasi langkah berikutnya (integrasi Supabase, modul TAXIS berikutnya, dst.) — hanya
  dicatat, TIDAK dikerjakan tanpa proyek/approval baru

**Validasi:**
- Semua item in-scope di PRD.md tercentang selesai atau didokumentasikan kenapa belum

**Output:** Catatan handoff singkat + kedua file HTML final.

---

## Status Fase

| Phase | Nama | Status |
|---|---|---|
| 0 | Setup & Design Tokens | Disetujui |
| 1 | Landing Page / Company Profile | Disetujui |
| 2 | Dashboard Shell | Disetujui |
| 3 | Builder Scorecard | Disetujui |
| 4 | Scoring Engine | Disetujui |
| 5 | Visualisasi Ringkasan | Disetujui |
| 6 | Responsif & Aksesibilitas | Disetujui |
| 7 | Review & Handoff | Disetujui |

*(Agent Codex WAJIB memperbarui kolom Status di tabel ini setiap kali sebuah Phase selesai
dikerjakan dan menunggu approval — ubah jadi "Menunggu Approval", lalu setelah Yudi menyetujui
di chat, ubah jadi "Disetujui" sebelum memulai Phase berikutnya.)*

## Perubahan Scope

*(Kosong — isi di sini jika ada perubahan scope disepakati di tengah proses build, dengan
tanggal dan alasan singkat.)*

## Handoff Phase 7

### Checklist PRD — In Scope

- [x] Landing page: hero, CTA demo, empat pilar, penjelasan STRATEGOS, serta footer identitas dan kontak.
- [x] Dashboard: sidebar grouped yang dirender dari `navConfig`, pemilih snapshot, dan navigasi mobile.
- [x] Builder: empat perspektif, CRUD objective/KPI, validasi input, dan indikator total bobot.
- [x] Scoring deterministik: skor KPI (clamp 0–120%), skor perspektif, skor total, dan status RAG.
- [x] Ringkasan: stat callout skor total, badge/label RAG, serta KPI Library read-only dari Knowledge Base.
- [x] Responsif dan aksesibilitas: layout desktop/tablet/mobile, scroll tabel pada layar sempit, focus state, dan status RAG berteks.

### Known Limitations

- Data hanya berada di memori browser; data hilang saat halaman di-refresh dan belum tersedia untuk multi-user.
- Belum ada autentikasi, backend/Supabase, ekspor PDF/Excel, perbandingan antar-periode, maupun AI/BYOK.
- Snapshot demo terbatas pada Q3 2026 dan Q4 2026; penambahan snapshot baru belum tersedia.
- TAXIS, ERGON, MISTHOS, dan tool STRATEGOS lainnya masih berstatus “Segera”.

### Rekomendasi Langkah Berikutnya

1. Integrasikan Supabase untuk autentikasi, penyimpanan scorecard, dan snapshot yang dikelola pengguna.
2. Tambahkan ekspor serta perbandingan snapshot setelah model data stabil.
3. Lanjutkan modul TAXIS dengan pola navigasi config-driven yang sama.
