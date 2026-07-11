# Tahap 1: Perancangan Arsitektur & Studi Literatur

**Status:** ✅ Selesai  
**Durasi:** Minggu 1-4  
**Deliverable:** Proposal penelitian, matriks literatur, diagram arsitektur sistem

---

## 1. Tujuan Tahap

- Memformulasikan masalah penelitian yang jelas dan testable
- Mengidentifikasi gap literatur yang akan diisi
- Merancang arsitektur sistem eksperimen (Baseline vs Context-Aware)
- Menentukan metrik evaluasi dan protokol validasi

---

## 2. Aktivitas

### 2.1 Problem Formulation (Minggu 1)

**Output:** Problem Statement Builder (WS-02)

**Masalah yang Diidentifikasi:**
- **Fenomena:** Wisatawan kesulitan memilih destinasi di Semarang (information overload)
- **Symptom:** Rekomendasi CF standar tidak memperhitungkan jarak geografis
- **Root Cause:** Algoritma CF murni hanya bergantung pada matriks rating (User × Item)
- **Impact:** Rekomendasi tidak praktis — destinasi terpisah puluhan km

**Problem Statement:**
> Sistem rekomendasi pariwisata berbasis User-Based Collaborative Filtering standar yang hanya bergantung pada matriks rating pengguna-item rentan menghasilkan rekomendasi yang tidak rasional secara geografis, di mana destinasi yang direkomendasikan terpisah dalam jarak yang tidak efisien untuk dikunjungi dalam satu perjalanan. Diperlukan pengembangan metode yang menyeimbangkan akurasi prediksi rating dengan rasionalitas geografis rekomendasi.

### 2.2 Literature Review (Minggu 2-3)

**Strategi Pencarian:**
- Keywords: `collaborative filtering`, `context-aware recommender systems`, `location-based recommendation`, `tourism recommender`
- Database: Google Scholar, IEEE Xplore, ACM Digital Library
- Periode: 2010-2023

**Literatur Kunci yang Dikaji:**

| Kategori | Paper | Key Insight |
|----------|-------|-------------|
| **Foundational CF** | Ricci et al. (2015) *Recommender Systems Handbook* | Dasar teoretis User-Based vs Item-Based CF |
| **Context-Aware RS** | Adomavicius & Tuzhilin (2011) *CARS Framework* | Tiga paradigma CARS: pre-filtering, post-filtering, contextual modeling |
| **Location-Based RS** | Zheng et al. (2010) *LARS* | Spatial smoothing meningkatkan akurasi CF pada domain restoran |
| **Tourism RS** | Brilhante et al. (2015) *TripBuilder* | Trajectory mining untuk rekomendasi rute wisata |
| **Baseline Lokal** | Cholil et al. (2023) *CF Semarang* | CF standar untuk pariwisata Semarang (tanpa konteks geografis) |

**Gap yang Diidentifikasi:**
1. **Context Gap:** CF tradisional mengabaikan dimensi spasial
2. **Method Gap:** Belum ada Context-Aware CF untuk pariwisata Semarang
3. **Evaluation Gap:** Evaluasi CF sebelumnya tidak menggunakan validasi ketat (K-Fold)

*(Detail lengkap: [../02-literatur/matriks-literatur.md](../02-literatur/matriks-literatur.md))*

### 2.3 Research Question & Hypothesis (Minggu 3)

**Research Question:**
> Apakah integrasi pembobotan Context-Aware berbasis jarak geografis pada algoritma User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan User-Based Collaborative Filtering standar pada dataset rating destinasi wisata Kota Semarang?

**Tipe RQ:** Improvement (comparison pre/post intervention)

**Hipotesis:**
- **H₀:** Tidak ada penurunan MAE yang signifikan (Context-Aware ≈ Baseline)
- **H₁:** Terdapat penurunan MAE yang signifikan (Context-Aware < Baseline)
- **Threshold:** p-value < 0.05 (Paired T-Test), penurunan MAE ≥ 2%

### 2.4 Perancangan Arsitektur Sistem (Minggu 4)

**Komponen Sistem:**

```
┌───────────────────────────────────────┐
│      SISTEM EKSPERIMEN                │
├───────────────────────────────────────┤
│                                       │
│  ┌─────────────┐   ┌──────────────┐  │
│  │ Baseline CF │   │Context-Aware │  │
│  │  (Pearson)  │   │  CF + Spatial│  │
│  └──────┬──────┘   └──────┬───────┘  │
│         │                  │          │
│         └────────┬─────────┘          │
│                  │                    │
│         ┌────────▼────────┐           │
│         │  5-Fold Cross   │           │
│         │   Validation    │           │
│         └────────┬────────┘           │
│                  │                    │
│         ┌────────▼────────┐           │
│         │  MAE, RMSE      │           │
│         │  Paired T-Test  │           │
│         └─────────────────┘           │
└───────────────────────────────────────┘
```

**Keputusan Desain Kritis:**

| Aspek | Keputusan | Justifikasi |
|-------|-----------|-------------|
| **Similarity Metric** | Pearson Correlation | Menangani bias rating per user (normalisasi) |
| **K-Neighbors** | 30 | Balance akurasi vs coverage (standar industri) |
| **Spatial Filter** | Pre-filtering (radius 10 km) | Efisien, mudah diinterpretasi |
| **Distance Formula** | Haversine | Standar untuk menghitung jarak geografis |
| **Validation** | 5-Fold CV | Mitigasi overfitting, standar dataset medium |
| **Primary Metric** | MAE | Linear, mudah diinterpretasi |
| **Secondary Metric** | RMSE | Mendeteksi outlier (error ekstrem) |

*(Detail formula dan diagram: [../03-teori/arsitektur-sistem.md](../03-teori/arsitektur-sistem.md))*

---

## 3. Deliverable

### 3.1 Dokumen

- [x] Proposal penelitian lengkap ([../01-proposal/proposal-penelitian.md](../01-proposal/proposal-penelitian.md))
- [x] Matriks literatur 6 paper kunci ([../02-literatur/matriks-literatur.md](../02-literatur/matriks-literatur.md))
- [x] Diagram arsitektur sistem ([../03-teori/arsitektur-sistem.md](../03-teori/arsitektur-sistem.md))
- [x] Worksheet problem statement (WS-02)
- [x] Worksheet RQ & hypothesis (WS-04)

### 3.2 Validasi

**Quality Check Problem Statement:**
- [x] Clarity (skor 4/5)
- [x] Measurability (skor 5/5)
- [x] Relevance (skor 5/5)
- [x] Testability (skor 5/5)
- [x] Impact (skor 4/5)

**Total Skor:** 23/25 (Excellent)

**Quality Check RQ:**
- [x] Variabel spesifik (IV: Jenis Algoritma, DV: MAE)
- [x] Metrik jelas (MAE, RMSE)
- [x] Baseline ada (Cholil et al., 2023)
- [x] Konteks disebutkan (Pariwisata Semarang)
- [x] Memerlukan eksperimen (bukan hanya survei literatur)

---

## 4. Keputusan Kunci

### 4.1 Mengapa Pre-Filtering (bukan Post-Filtering)?

**Pertimbangan:**
- **Pre-Filtering:** Filter kandidat berdasarkan jarak sebelum CF → efisien, mudah diinterpretasi
- **Post-Filtering:** CF dulu, filter hasil → risiko kehilangan kandidat berkualitas
- **Contextual Modeling:** Konteks sebagai dimensi model → kompleks, sulit diinterpretasi

**Keputusan:** Pre-filtering dipilih karena balance antara efisiensi dan interpretability.

### 4.2 Mengapa Radius 10 km?

**Eksplorasi Awal:**
- Grid search: 5 km, 7.5 km, 10 km, 12.5 km, 15 km
- Median jarak perjalanan turis Semarang: 8-12 km
- Trade-off: radius terlalu kecil → coverage rendah; radius terlalu besar → tidak efektif

**Keputusan:** 10 km dipilih sebagai threshold optimal.

### 4.3 Mengapa 5-Fold CV (bukan 10-Fold)?

**Pertimbangan:**
- Dataset size: 4.362 records (medium)
- 5-Fold: 80% train (3.490), 20% test (872) → cukup representatif
- 10-Fold: overhead komputasi 2x lipat, gain marginal

**Keputusan:** 5-Fold memberikan balance bias-variance yang baik untuk dataset ini.

---

## 5. Risiko & Mitigasi

| Risiko | Probabilitas | Dampak | Mitigasi |
|--------|--------------|--------|----------|
| Gap literatur terlalu luas | Low | High | Fokus pada 3 gap spesifik (context, method, evaluation) |
| Baseline tidak reproducible | Medium | High | Replikasi persis metode Cholil et al. (2023) |
| Threshold 10 km tidak optimal | Medium | Medium | Validated via grid search di Tahap 3 |
| Dataset tidak cukup besar | Low | Medium | Gunakan stratified K-Fold untuk maksimalkan sampel |

---

## 6. Catatan Penting

### 6.1 Asumsi

- Dataset Google Maps representatif terhadap preferensi wisatawan Semarang
- Rating 1-5 bintang cukup granular untuk menangkap perbedaan preferensi
- Jarak geografis adalah konteks paling kritis (dibanding waktu, cuaca)

### 6.2 Limitasi yang Diakui

- Tidak memperhitungkan dimensi temporal (jam operasional, musim)
- Threshold 10 km fixed (tidak adaptif per user)
- Evaluasi offline (tidak ada validasi dengan pengguna riil)

---

## 7. Lessons Learned

### 7.1 Problem Formation

> **Insight:** Transformasi dari "topik" ke "masalah riset" memerlukan 5 tahap: Reality → Observed Issue → Diagnosed Problem → Researchable Problem → Measurable Variable. Melompat langsung ke variabel adalah kesalahan paling umum.

### 7.2 Gap Analysis

> **Insight:** Gap yang valid harus spesifik, measurable, dan terhubung langsung dengan kontribusi penelitian. "Belum ada penelitian tentang X" bukan gap — "Belum ada bukti empiris bahwa metode Y lebih baik dari Z pada kondisi W" adalah gap.

### 7.3 Hypothesis Formulation

> **Insight:** Hipotesis harus falsifiable (bisa dibuktikan salah). "Algoritma A lebih baik" bukan hipotesis — "Algoritma A menghasilkan MAE < 0.65 dengan p < 0.05" adalah hipotesis.

---

## 8. Approval Checklist

- [x] Problem statement disetujui pembimbing
- [x] Gap literatur tervalidasi (minimal 5 paper kunci)
- [x] RQ & hipotesis clear dan testable
- [x] Arsitektur sistem feasible untuk diimplementasikan
- [x] Metrik evaluasi sesuai standar domain

**Disetujui untuk lanjut ke Tahap 2 (Pengumpulan Data)**

---

**Tanggal Selesai:** 2024-02-01  
**Next Milestone:** Tahap 2 — Target 4.000+ ulasan Google Maps Semarang
