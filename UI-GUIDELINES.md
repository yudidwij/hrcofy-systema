# UI Guidelines — HRCofy Systema

**Status:** Draft untuk approval — belum ada eksekusi kode
**Versi:** 1.0

---

## 1. Prinsip Desain

Audiens produk ini adalah praktisi HR dan pemilik bisnis — bukan konsumen Gen Z. Nada visualnya:
**profesional, tegas, sedikit futuristik** (mencerminkan "consulting operating system"), bukan
playful/konsumer. Navy gelap sebagai dominan memberi kesan otoritatif; Gold dan Blue dipakai
sebagai aksen bertenaga, bukan warna utama.

Hindari default generik AI-generated (lihat catatan desain internal): jangan pakai gradient
terracotta hangat, jangan pakai kartu seragam dengan shadow abu-abu generik di semua tempat,
jangan tempelkan label ALL-CAPS di atas tiap heading tanpa alasan. Satu elemen boleh jadi
"pusat perhatian" (stat callout skor total scorecard) — sisanya tenang dan disiplin.

## 2. Design Tokens

### 2.1 Warna (WAJIB — sama persis, jangan didekati)

| Token | Hex | Penggunaan |
|---|---|---|
| `navy` | `#151B3B` | Warna dominan — background gelap, teks judul di atas latar terang |
| `navy-mid` | `#1E2548` | Card di atas background gelap |
| `gold` | `#F5A623` | Aksen utama — angka statistik, judul di atas latar gelap, highlight |
| `gold-bright` | `#FFC107` | Hover state, gradient pair dengan gold |
| `blue` | `#4DBCE9` | Aksen sekunder — subtitle di atas latar gelap, data highlight |
| `blue-bright` | `#29B6F6` | CTA button, gradient pair dengan blue |
| `white` | `#FFFFFF` | Teks body di atas latar gelap |
| `light` | `#F5F6FA` | Background section konten, card di atas latar terang |
| `charcoal` | `#2A2E45` | Teks body di atas latar terang (jangan pernah pakai hitam murni) |
| `muted` | `#8B92A8` | Teks sekunder, caption, label |
| `red` | `#C75B3F` | Status RAG "at risk" (skor <80%) |
| `orange` | `#E67E22` | Status RAG "medium" (skor 80–99%) |
| `green` | `#2E7D6F` | Status RAG "on track" (skor ≥100%) |

**Aturan warna:**
1. Navy dominan — minimum 40% area visual di setiap layar
2. Gold dan Blue selalu muncul berdekatan, tidak berdiri sendiri
3. Tidak pernah pakai hitam murni (`#000000`) — pakai navy atau charcoal
4. RAG (red/orange/green) hanya dipakai untuk status skor scorecard, tidak untuk dekorasi lain

### 2.2 Tipografi

- **Font:** Calibri sebagai font utama. Fallback stack: `'Calibri', 'Segoe UI', system-ui, sans-serif`
  (Calibri tidak tersedia di semua OS/browser — fallback wajib disiapkan agar tetap konsisten)
- Judul halaman: 32–40px, bold, warna gold (di atas navy) atau navy (di atas terang)
- Judul section: 20–24px, bold
- Body text: 14–16px, regular, line-height 1.5–1.8
- Label/caption: 10–12px, bold, warna muted
- Stat number (skor total scorecard): 48–64px, bold, gold atau blue

### 2.3 Spacing & Layout

- Grid berbasis 8px (spacing: 8, 16, 24, 32, 48, 64px)
- Card padding internal: 16–24px
- Border radius: konsisten 8–10px di semua card (jangan campur radius berbeda-beda dalam satu
  layar)
- Max content width: 1280px, centered

## 3. Pola Komponen

### 3.1 Navbar (landing page)
Background navy solid, logo teks "HR" (gold) + "Cofy" (blue) + "Systema" (white, lebih tipis) di
kiri, navigasi kanan, CTA button gold/blue gradient di paling kanan.

### 3.2 Hero (landing page)
Background navy, headline besar warna gold, subheadline warna blue/muted, satu CTA utama. Hindari
pola default "big number + small label + gradient accent" kecuali memang paling relevan di sini —
karena ini bukan produk metrik tunggal, headline naratif lebih tepat daripada stat callout di hero.

### 3.3 Pillar Card (landing page — 4 pilar)
Grid 2×2 atau 4-kolom di desktop, stack vertikal di mobile. Card untuk STRATEGOS aktif: border
top gold 3px, background putih, ikon + nama pilar + deskripsi singkat + badge "Tersedia". Card
untuk TAXIS/ERGON/MISTHOS: sedikit di-mute (opacity lebih rendah atau background light gray),
badge "Segera".

### 3.4 Sidebar (dashboard)
Background navy-mid, item aktif (STRATEGOS > Balanced Scorecard) diberi indikator gold di kiri.
Item pilar lain ditampilkan tapi disabled/grayed dengan label "Segera".

### 3.5 Perspective Card (dashboard — 4 kartu BSC)
Background putih, border top 3px sesuai status RAG perspektif tersebut (merah/oranye/hijau),
judul perspektif (navy, bold), daftar Objective + KPI di dalamnya, skor perspektif di pojok kanan
atas card dalam bentuk badge bulat kecil.

### 3.6 Stat Callout (skor total scorecard)
Angka besar (gold atau blue tergantung kontekstualnya di latar apa), label kecil muted di
bawahnya — pola signature HRCofy, dipakai HANYA untuk skor total, bukan untuk setiap angka kecil
di halaman (kalau semua angka dibesarkan, tidak ada lagi yang terasa istimewa).

### 3.7 Form Input (builder Objective/KPI)
Border tipis abu-abu netral saat idle, border blue saat focus, label di atas input (bukan
placeholder-only — placeholder tidak boleh jadi satu-satunya label). Validasi error ditandai
border merah + pesan singkat di bawah input dalam bahasa yang jelas ("Total bobot perspektif ini
115%, kurangi 15%" — bukan "Invalid weight").

### 3.8 RAG Badge
Bulat kecil atau pill, warna solid sesuai status (merah/oranye/hijau), teks putih, dipakai
konsisten di semua tempat yang menampilkan status skor (card, tabel, sidebar summary).

## 4. Responsif

- Breakpoint: mobile (<640px), tablet (640–1024px), desktop (>1024px)
- Sidebar dashboard collapse jadi bottom-nav atau hamburger di mobile
- Grid 4 perspektif: 1 kolom di mobile, 2 kolom di tablet, 4 kolom di desktop (atau 2×2)
- Tabel KPI di dalam card: scroll horizontal di mobile, bukan dipaksa muat

## 5. Aksesibilitas

- Kontras teks minimum WCAG AA (khususnya teks muted #8B92A8 di atas putih — cek kontrasnya,
  perbesar jika perlu untuk teks kecil)
- Semua interactive element (button, input) punya visible focus state
- Warna RAG tidak jadi satu-satunya penanda status — sertakan juga teks/ikon (mis. "Hijau — On
  Track") untuk yang buta warna

## 6. Setup Teknis (Tailwind Play CDN)

Karena tanpa build step, definisikan token warna sebagai extend theme inline di `<head>`:

```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          navy: '#151B3B',
          'navy-mid': '#1E2548',
          gold: '#F5A623',
          'gold-bright': '#FFC107',
          blue: '#4DBCE9',
          'blue-bright': '#29B6F6',
          light: '#F5F6FA',
          charcoal: '#2A2E45',
          muted: '#8B92A8',
          rag-red: '#C75B3F',
          'rag-orange': '#E67E22',
          'rag-green': '#2E7D6F',
        },
        fontFamily: {
          sans: ['Calibri', 'Segoe UI', 'system-ui', 'sans-serif'],
        },
      },
    },
  }
</script>
```

Ini harus jadi bagian pertama yang dibangun di Phase 0 pada Implementation Plan — semua phase
berikutnya bergantung pada token ini sudah tersedia.

## 7. Struktur Navigasi Skalabel (WAJIB — sejak Phase 2)

HRCofy Systema akan berkembang dari 1 tool (STRATEGOS > Balanced Scorecard) menjadi puluhan tool
lintas 4 pilar. Sidebar harus dirancang untuk pertumbuhan itu sejak awal, bukan dirombak nanti.
Berdasarkan pola yang terbukti di produk SaaS multi-modul (Notion, Linear, HubSpot) dan software
sejenis (ClearPoint, Cascade):

### 7.1 Grouped Sidebar, bukan Flat List

Sidebar dikelompokkan per pilar sebagai group header, dengan tools sebagai item di bawahnya —
bukan daftar rata tanpa pengelompokan. Struktur visual:

```
HRCofy Systema
├─ STRATEGOS                    ← group header, gold accent (pilar aktif)
│   └─ Balanced Scorecard & KPI   ← item aktif, indikator gold di kiri
│   └─ EFE / IFE / CPM             (label "Segera")
│   └─ SWOT / SPACE / BCG / IE      (label "Segera")
│   └─ QSPM                         (label "Segera")
├─ TAXIS                        ← group header, muted/disabled (pilar belum aktif)
│   └─ (kosong / label "Segera")
├─ ERGON                        ← group header, muted/disabled
├─ MISTHOS                      ← group header, muted/disabled
```

Group header pilar aktif (STRATEGOS) tetap ditonjolkan (teks gold/putih), pilar yang belum aktif
di-mute (teks muted #8B92A8) tapi tetap terlihat sebagai preview — supaya struktur akhir produk
sudah terasa sejak MVP, bukan baru muncul saat pilar itu dibangun.

### 7.2 Navigation Config Terpisah dari Markup

Daftar menu TIDAK ditulis langsung berulang sebagai HTML di setiap file. Simpan sebagai satu
objek JavaScript (mis. `navConfig` di awal `<script>` dashboard.html), lalu render sidebar dari
situ dengan loop. Contoh struktur data:

```javascript
const navConfig = [
  {
    pillar: "STRATEGOS",
    status: "active",
    tools: [
      { name: "Balanced Scorecard & KPI Library", status: "active", href: "#bsc" },
      { name: "EFE / IFE / CPM", status: "coming-soon" },
      { name: "SWOT / SPACE / BCG / IE", status: "coming-soon" },
      { name: "QSPM", status: "coming-soon" },
    ],
  },
  { pillar: "TAXIS", status: "coming-soon", tools: [] },
  { pillar: "ERGON", status: "coming-soon", tools: [] },
  { pillar: "MISTHOS", status: "coming-soon", tools: [] },
];
```

Manfaatnya: menambah tool baru (mis. saat modul TAXIS mulai dibangun) = tambah satu entri di
`navConfig`, bukan mengedit markup sidebar di banyak tempat. Ini juga membuat sidebar mobile dan
desktop selalu konsisten karena keduanya render dari config yang sama, bukan dua markup terpisah
yang bisa saling tidak sinkron.

### 7.3 Collapsible untuk Efisiensi Ruang

Sidebar harus punya mode collapse (ikon saja) untuk pengguna yang sudah familiar dan ingin ruang
konten lebih luas — tidak wajib di MVP Phase 2, tapi struktur HTML/CSS-nya sebaiknya sudah
mengakomodasi ini (mis. lebar sidebar dikontrol lewat satu class yang mudah di-toggle) supaya
tidak perlu rombak total saat fitur ini ditambahkan di fase berikutnya.

### 7.4 Kalibrasi Nada Visual

Dibanding software strategi murni yang cenderung dingin-korporat (ClearPoint), HRCofy Systema
menempatkan diri di tengah — tetap otoritatif (basis framework akademis David/Kaplan-Norton),
tapi tidak sedingin software enterprise generik. Warna navy tetap dominan, tapi hindari kesan
"terlalu birokratis" — card dengan sudut membulat (8-10px, bukan tajam 0px), copy yang ramah dan
jelas (lihat prinsip penulisan di frontend-design), bukan bahasa teknokratis.
