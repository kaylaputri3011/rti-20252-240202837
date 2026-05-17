# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment)
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```

PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [x] Problem → Gap: masalah terdokumentasi di literatur
  [x] Gap → RQ: pertanyaan menjawab gap spesifik
  [x] RQ → Hypothesis: hipotesis memprediksi jawaban
  [x] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [x] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [x] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [x] Istilah sama di semua bagian
  [x] Variabel di RQ = variabel di hipotesis = metrik di desain
  [x] Scope tidak berubah dari masalah ke eksperimen

```

Rubrik Self-Assessment:
| Kriteria | 1 (Lemah) | 2 (Cukup) | 3 (Baik) | Skor |
|----------|-----------|-----------|----------|------|
| Koherensi |          |           |    [x]   |  3   |
| Specificity |        |           |    [x]   |  3   |
| Feasibility |        |    [x]    |          |  2   |
| Rigor     |          |           |    [x]   |  3   |

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Algoritma rekomendasi pariwisata saat ini (User-Based CF) mengalami context-blindness, yaitu merekomendasikan tempat murni dari kemiripan rating tanpa mempedulikan jarak fisik wisatawan atau jam operasional wisata. |
| Gap | WS-03 | Literatur SOTA pariwisata lokal (Cholil dkk., 2023) hanya mengandalkan matriks historis dan secara eksplisit menyebutkan pengabaian faktor geospasial serta temporal sebagai future work (Method & Context Gap). |
| RQ | WS-04 | Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based CF mampu menghasilkan skor MAE yang lebih rendah dibandingkan User-Based CF standar pada dataset pariwisata Semarang? |
| Hipotesis | WS-04 | H₁: Sistem Context-Aware User-Based CF menghasilkan penurunan skor MAE yang signifikan secara statistik (minimal 10%) dibandingkan baseline User-Based CF murni. |
| Variabel & Metrik | WS-05 | IV = Jenis Algoritma (Context-Aware vs Standar); DV = Tingkat Kesalahan Prediksi (Prediction Error) yang diukur dengan metrik MAE dan RMSE. |
| Sistem | WS-06 | Arsitektur modular Python yang memisahkan Recommendation Engine (memungkinkan toggle on/off fitur jarak/waktu) dan Evaluation Logger berbasis parameter config.yaml. |
| Desain Eksperimen | WS-07 | Comparison Study (Treatment vs Control) menggunakan dataset identik, divalidasi dengan K-Fold Cross Validation (K=5) dan uji signifikansi Paired Sample T-Test. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✅ | Masalah context-blindness divalidasi oleh literatur di Bab 3 yang terbukti masih menggunakan rating murni tanpa filter jarak geografis. |
| Gap → RQ | ✅ | RQ secara langsung menguji dan mengukur efek perbaikan jika gap geospasial dan temporal tersebut diisi. |
| RQ → Hypothesis | ✅ | H₁ memprediksi jawaban definitif atas RQ, yaitu terjadinya penurunan nilai error (MAE) secara spesifik (10%). |
| Hypothesis → Metric | ✅ | Prediksi penurunan error pada hipotesis langsung direpresentasikan dan diukur secara matematis menggunakan rumus MAE. |
| Metric → System | ✅ | Modul Evaluator Logger pada sistem dirancang spesifik untuk menghitung selisih prediksi dengan aktual dan mencetak skor MAE ke file CSV. |
| System → Experiment | ✅ | Eksperimen dijalankan dengan melakukan pertukaran parameter IV secara langsung di sistem config.yaml tanpa mengubah kode evaluasi utama. |

**Koneksi mana yang paling lemah?** 
> Hypothesis → Metric

**Bagaimana cara memperkuatnya?**
> Menyadari bahwa penurunan angka MAE (offline test) belum tentu menjamin 100% kepuasan pengguna di dunia nyata (online satisfaction). Cara memperkuatnya adalah dengan membatasi scope claim di proposal: tegaskan bahwa riset ini berfokus pada akurasi prediksi komputasi, bukan pada studi interaksi manusia-komputer (HCI). Tambahkan juga metrik RMSE untuk memastikan sistem tidak melakukan kesalahan tebakan yang fatal.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [x] Ya / [ ] Tidak
> Jika tidak, di bagian mana terjadi inkonsistensi? -
> (Tidak ada. Seluruh alur konsisten menggunakan istilah Context-Aware CF, metrik MAE, dan lokus data Semarang).

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 | Benang merah dari masalah "buta konteks", penemuan gap di paper Cholil, hingga desain eksperimen sangat mulus dan logis. |
| Specificity | 3 | Variabel dan metrik (MAE, RMSE, K-Fold=5, Ambang Batas 10KM) sudah terdefinisi secara kuantitatif dan tidak ambigu. |
| Feasibility | 2 | Metodologi logis, namun preprocessing data (membersihkan koordinat latitude/longitude dan jam buka dari Google Maps) butuh effort ekstra. |
| Rigor | 3 | Desain eksperimen dikontrol sangat ketat dengan pembagian split data yang sama (random state locked) dan diuji secara statistik (T-Test). |

**Skor total:** 11 / 12

**Apakah proposal siap untuk fase eksekusi?** [x] Ya / [ ] Belum
> Jika belum, apa yang perlu diperbaiki? -
> (Sudah siap dieksekusi ke tahap pencarian dataset dan penyusunan draf kode Python).

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** 
> Mengisi WS-06 (System-Experiment Mapping) dan WS-05 (Metrics). Karena terbiasa dengan pola pikir logika programming, memetakan sistem menjadi arsitektur modular yang terukur terasa lebih pasti dan terstruktur.

**Bagian tersulit:** 
> Mengisi WS-03 (Literature Gap) dan WS-07 (Threats to Validity). Membutuhkan pergeseran mindset yang drastis dari sekadar "ingin membuat aplikasi" menjadi "harus membuktikan bahwa belum ada paper yang melakukan ini persis seperti ini" dan memikirkan segala celah bias eksperimen.

**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, saya akan mengalokasikan waktu di awal untuk melakukan pra-survei dataset (mengumpulkan sample data eksplorasi (pilot dataset) atau mengecek kemudahan crawling Google Maps API) sebelum merumuskan RQ secara permanen. Hal ini untuk memastikan bahwa data jarak dan waktu riil yang saya butuhkan benar-benar eksis dan bisa ditarik, sehingga nilai kelayakan (feasibility) riset bisa maksimal sejak hari pertama.
