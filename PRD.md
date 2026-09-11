# PRD — HRCofy Systema (Modul STRATEGOS: Balanced Scorecard & KPI Library)

**Status:** Draft untuk approval — belum ada eksekusi kode
**Versi:** 1.0
**Pemilik produk:** Yudi Dwijayanto — HRCofy Consulting
**Terakhir diperbarui:** 2026-09-07

---

## 1. Latar Belakang

HRCofy Systema adalah versi web publik dari HRCofy Platform — sebuah *consulting operating system*
yang menyatukan empat pilar framework proprietary HRCofy:

| Pilar | Domain | Referensi |
|---|---|---|
| **STRATEGOS** | Strategi & perencanaan | Fred R. David 3-Stage Framework, Kaplan & Norton BSC |
| **TAXIS** | Arsitektur jabatan | Kamus kompetensi, job description, evaluasi jabatan |
| **ERGON** | Organisasi & proses | Analisis beban kerja, SOP |
| **MISTHOS** | Kompensasi & kepatuhan | PPh 21, BPJS, pesangon, dokumen hukum ketenagakerjaan |

Benchmark arsitektur: uwongke.com (27 tools HR gratis, BYOK AI, kalkulasi inti deterministik
terpisah dari lapisan AI). HRCofy Systema mengadopsi prinsip yang sama — kalkulasi deterministik
dipisah dari lapisan AI — tapi dengan positioning yang lebih premium/consulting-grade, memakai
taksonomi 4 pilar Yunani di atas.

Modul pertama yang dibangun adalah **STRATEGOS → Balanced Scorecard & KPI Library**, dipilih
sebagai MVP karena:
- Berdiri sendiri, tidak butuh menunggu modul lain selesai
- Selaras dengan musim Q3–Q4 (evaluasi tahun berjalan, perencanaan tahun depan)
- Beban AI paling ringan dibanding tool STRATEGOS lain (EFE/IFE/SWOT/QSPM), karena struktur BSC
  (4 perspektif) sudah baku
- Sudah ada Knowledge Base rujukan lengkap: `STRATEGOS_Knowledge_Base_v2.pdf` (Bagian VI — Balanced
  Scorecard & Strategy Map) dan `PHASE_EXECUTION_GUIDE.pdf` (Phase 10–14)

## 2. Tujuan Fase Ini

Membangun **frontend saja** (tanpa backend/autentikasi) untuk dua permukaan:

1. **Landing page / company profile** — memperkenalkan HRCofy Systema, keempat pilar, dan posisi
   Balanced Scorecard & KPI Library sebagai modul yang tersedia sekarang.
2. **Admin dashboard (CMS-style)** — tempat pengguna membangun, mengisi, dan melihat Balanced
   Scorecard mereka secara interaktif.

Tidak ada Supabase, tidak ada login sungguhan, tidak ada BYOK AI di fase ini. Data disimpan di
state JavaScript lokal (in-memory), cukup untuk demo dan validasi UX ke klien.

## 3. Target Pengguna

- **Primer:** Yudi sendiri, untuk demo ke klien konsultasi (praktisi HR, business owner UMKM
  hingga korporasi menengah)
- **Sekunder (nanti):** klien HRCofy yang mengisi scorecard mereka sendiri secara self-serve

## 4. Ruang Lingkup

### 4.1 Termasuk (in-scope)

**Landing Page**
- Hero section — perkenalan HRCofy Systema
- Ringkasan 4 pilar (STRATEGOS aktif/tersedia, TAXIS/ERGON/MISTHOS ditandai "Segera")
- Penjelasan singkat modul Balanced Scorecard & KPI Library
- CTA menuju dashboard (tanpa autentikasi sungguhan — tombol langsung masuk demo)
- Footer dengan identitas HRCofy (tagline, kontak)

**Admin Dashboard — Modul Balanced Scorecard & KPI Library**
- Struktur navigasi sidebar yang sudah menyiapkan slot untuk 4 pilar (hanya STRATEGOS yang aktif)
- Pemilih periode/snapshot (mis. "Q3 2026", bisa tambah periode baru)
- Builder scorecard per 4 perspektif (Financial, Customer, Internal Process, Learning & Growth):
  - Tambah/edit/hapus Objective per perspektif
  - Tambah/edit/hapus KPI per Objective: nama, unit, weight (%), target, actual
  - Validasi: total weight per perspektif harus 100% (indikator visual jika belum)
- Kalkulasi otomatis (deterministik, client-side):
  - Skor per KPI = (actual ÷ target) × 100, dibatasi 0–120%
  - Skor per perspektif = rata-rata tertimbang skor KPI di dalamnya
  - Skor total scorecard = rata-rata tertimbang 4 perspektif
  - Status RAG per KPI/perspektif/total: Merah (<80%), Kuning (80–99%), Hijau (≥100%)
- Tampilan ringkasan scorecard — 4 card perspektif + 1 stat callout skor total
- Panel referensi KPI Library — daftar contoh KPI per perspektif dari Knowledge Base (F1–F4,
  Customer value proposition, P1–P4, L1–L3) sebagai bantuan saat user mengisi Objective/KPI

### 4.2 Tidak termasuk (out-of-scope, fase berikutnya)

- Autentikasi/Supabase, penyimpanan permanen
- Modul TAXIS, ERGON, MISTHOS
- EFE/IFE/CPM/SWOT/SPACE/BCG/IE/QSPM (tool STRATEGOS lainnya — cascade dari sini ke BSC, bukan
  bagian dari MVP ini)
- Fitur AI/BYOK (insight naratif otomatis, rekomendasi KPI oleh AI)
- Ekspor PDF/Excel
- Perbandingan antar-periode (komparasi Q3 vs Q4)

## 5. Kriteria Sukses Fase Ini

- Prototipe berjalan penuh di browser tanpa backend, bisa dibuka langsung dari file HTML atau
  static hosting sederhana
- Responsif dari mobile hingga desktop
- Sesuai brand HRCofy (lihat UI-GUIDELINES.md)
- Bisa didemokan ke klien untuk validasi UX sebelum investasi waktu ke integrasi Supabase

## 6. Asumsi

- Data KPI Library yang ditampilkan adalah seed data statis dari Knowledge Base, bukan hasil AI
- Tidak perlu multi-user di fase ini — satu sesi = satu scorecard yang sedang dikerjakan
- Tailwind CSS dimuat via Play CDN (tanpa build step), sesuai keputusan teknis Yudi

## 7. Referensi

- `STRATEGOS_Knowledge_Base_v2.pdf` — Bagian VI (Balanced Scorecard & Strategy Map)
- `PHASE_EXECUTION_GUIDE.pdf` — Phase 10 (Financial), 11 (Customer), 12 (Internal Process),
  13 (Learning & Growth), 14 (Strategy Map & Ringkasan Eksekutif)
- HRCofy Brand Guidelines (Navy #151B3B, Gold #F5A623, Blue #4DBCE9, Calibri)
