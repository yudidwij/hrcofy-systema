# Starter Prompt — HRCofy Systema (STRATEGOS Module)

Gunakan salah satu versi di bawah sebagai pesan pembuka ke Codex, setelah `AGENTS.md` dan ketiga
dokumen SOT (`PRD.md`, `UI-GUIDELINES.md`, `IMPLEMENTATION-PLAN.md`) sudah berada di root project.

---

## Versi Bahasa Inggris

Build a strategy execution platform called HRCofy Systema — starting with its first module,
STRATEGOS (Balanced Scorecard & KPI Library). The app should have a clean admin dashboard where
users can build and view their Balanced Scorecard organized into four perspectives — Financial,
Customer, Internal Process, and Learning & Growth — each showing its objectives, KPIs with
weight, target vs actual, and a color-coded RAG status (red/orange/green), with the total
scorecard score displayed prominently at the top as a stat callout. Include a sidebar navigation
grouped by pillar — STRATEGOS active with its tools listed, TAXIS/ERGON/MISTHOS shown as "Coming
Soon" — driven by a single navConfig object so future tools can be added without rewriting the
markup. Use a professional, authoritative design with a dark navy dominant color scheme
(#151B3B) accented by gold (#F5A623) and blue (#4DBCE9), Calibri typography, rounded corners, and
a layout that feels premium and easy to scan at a glance — not playful, not cold-corporate. Build
with plain responsive HTML and Tailwind CSS via Play CDN, no build step. Follow PRD.md,
UI-GUIDELINES.md, and IMPLEMENTATION-PLAN.md as the source of truth, and do not write code for
any phase until it is explicitly approved.

---

## Versi Bahasa Indonesia

Bangun sebuah platform eksekusi strategi bernama HRCofy Systema — dimulai dari modul pertamanya,
STRATEGOS (Balanced Scorecard & KPI Library). Aplikasi ini harus punya admin dashboard yang bersih,
tempat pengguna membangun dan melihat Balanced Scorecard mereka yang terorganisir dalam empat
perspektif — Financial, Customer, Internal Process, dan Learning & Growth — masing-masing
menampilkan objective, KPI beserta bobotnya, target vs actual, dan status RAG berwarna
(merah/oranye/hijau), dengan skor total scorecard ditampilkan menonjol di bagian atas sebagai stat
callout. Sertakan navigasi sidebar yang dikelompokkan per pilar — STRATEGOS aktif dengan daftar
tools-nya, TAXIS/ERGON/MISTHOS ditandai "Segera" — digerakkan oleh satu objek navConfig supaya
tool baru bisa ditambahkan nanti tanpa menulis ulang markup. Gunakan desain yang profesional dan
otoritatif dengan skema warna navy gelap dominan (#151B3B) beraksen gold (#F5A623) dan blue
(#4DBCE9), tipografi Calibri, sudut membulat, dan layout yang terasa premium serta mudah dipindai
sekilas — tidak playful, tapi juga tidak sedingin software enterprise generik. Bangun dengan HTML
responsif murni dan Tailwind CSS via Play CDN, tanpa build step. Ikuti PRD.md, UI-GUIDELINES.md,
dan IMPLEMENTATION-PLAN.md sebagai source of truth, dan jangan menulis kode untuk fase mana pun
sebelum disetujui secara eksplisit.

---

## Catatan Pemakaian

- Kedua versi isinya identik — pilih sesuai bahasa kerja yang Anda pakai saat sesi dengan Codex
- Prompt ini adalah pemicu awal saja; detail lengkap tetap di ketiga dokumen SOT. Kalau Codex
  menyimpang dari SOT meski sudah diberi prompt ini, rujuk balik ke `AGENTS.md` sebagai penegak
  aturan (khususnya soal phase-gate approval dan navConfig)
