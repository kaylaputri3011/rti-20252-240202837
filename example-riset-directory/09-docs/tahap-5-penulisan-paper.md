# Tahap 5: Penulisan Draft Paper/Laporan

**Status:** 🔄 Sedang Berjalan (85% selesai)  
**Durasi:** Minggu 12-14  
**Deliverable:** Draft paper lengkap (format jurnal lokal / skripsi)

---

## 1. Tujuan Tahap

- Menyusun draft paper/laporan penelitian lengkap
- Mengintegrasikan hasil eksperimen, visualisasi, dan analisis
- Mempersiapkan presentasi hasil penelitian
- Revisi berdasarkan feedback pembimbing

---

## 2. Struktur Paper

### 2.1 Outline Paper (Format Jurnal)

| Bagian | Status | Halaman | Catatan |
|--------|--------|---------|---------|
| **Abstract** | ✅ Selesai | 1 | 200-250 kata, mencakup problem, method, result, conclusion |
| **1. Pendahuluan** | ✅ Selesai | 2-3 | Latar belakang, problem statement, RQ, kontribusi |
| **2. Tinjauan Pustaka** | 🔄 Draft | 3-5 | CF, CARS, tourism RS, gap analysis |
| **3. Metodologi** | ✅ Selesai | 5-7 | Dataset, algoritma, eksperimen, evaluasi |
| **4. Hasil & Analisis** | ✅ Selesai | 7-9 | Tabel hasil, visualisasi, uji statistik |
| **5. Diskusi** | 🔄 Draft | 9-10 | Interpretasi, implikasi, limitasi |
| **6. Kesimpulan** | ✅ Selesai | 10 | Ringkasan temuan, future work |
| **Daftar Pustaka** | 🔄 Review | 11-12 | 15-20 referensi (APA style) |

**Total Target:** 12-15 halaman (format jurnal lokal)

---

## 3. Progress per Bagian

### 3.1 Abstract

**Status:** ✅ Selesai

**Draft:**

> Sistem rekomendasi pariwisata berbasis *Collaborative Filtering* (CF) standar sering mengabaikan konteks geografis, sehingga menghasilkan rekomendasi destinasi yang terpisah puluhan kilometer dan tidak praktis untuk dikunjungi dalam satu perjalanan. Penelitian ini mengembangkan dan mengevaluasi metode *Context-Aware Collaborative Filtering* yang mengintegrasikan filter spasial berbasis jarak geografis (Haversine formula, radius 10 km) untuk meningkatkan akurasi prediksi rating pada domain pariwisata Kota Semarang. Eksperimen dilakukan pada dataset 4.362 ulasan riil dari Google Maps menggunakan protokol *5-Fold Cross Validation*. Hasil menunjukkan bahwa Context-Aware CF berhasil menurunkan *Mean Absolute Error* (MAE) sebesar 3,11% dibandingkan Baseline CF (MAE 0,6511 vs 0,6720), dengan signifikansi statistik sangat tinggi (*p* < 0,001, Cohen's *d* = 8,37). Analisis tambahan menunjukkan perbaikan terbesar terjadi pada pasangan user-item dengan destinasi geografis yang dekat (perbaikan 3,88%). Penelitian ini membuktikan bahwa integrasi dimensi spasial ke dalam algoritma CF mampu meningkatkan akurasi prediksi sekaligus menghasilkan rekomendasi yang lebih rasional secara geografis.
>
> **Kata kunci:** Collaborative Filtering, Context-Aware Recommender Systems, Tourism Recommendation, Spatial Filtering, Haversine Distance

---

### 3.2 Pendahuluan

**Status:** ✅ Selesai

**Konten Utama:**
1. **Latar Belakang:**
   - Pariwisata Semarang: 78+ destinasi heterogen
   - Information overload pada wisatawan
   - CF sebagai solusi, namun mengabaikan jarak geografis

2. **Problem Statement:**
   - Rekomendasi CF standar tidak praktis (destinasi terpisah puluhan km)
   - Gap: konteks geografis diabaikan pada literatur CF pariwisata lokal

3. **Research Question:**
   - Apakah integrasi Context-Aware (spatial pre-filtering) menurunkan MAE?

4. **Kontribusi:**
   - Context Gap: Bukti empiris spatial context meningkatkan akurasi CF
   - Method Gap: Implementasi Context-Aware CF untuk pariwisata Semarang
   - Evaluation Gap: Validasi ketat dengan 5-Fold CV

5. **Struktur Paper:**
   - Brief overview bagian 2-6

---

### 3.3 Tinjauan Pustaka

**Status:** 🔄 Draft (70% selesai)

**Konten yang Perlu Dilengkapi:**
- [ ] Related work pada Location-Based RS (perlu tambah 3-4 paper)
- [ ] Perbandingan detail: pre-filtering vs post-filtering vs contextual modeling
- [ ] Positioning penelitian ini dalam landscape CARS

**Referensi Kunci (sudah dikutip):**
1. Ricci et al. (2015) — *Recommender Systems Handbook*
2. Adomavicius & Tuzhilin (2011) — *Context-Aware RS Framework*
3. Cholil et al. (2023) — *CF Pariwisata Semarang* (baseline)
4. Zheng et al. (2010) — *LARS (Location-Aware RS)*
5. Brilhante et al. (2015) — *TripBuilder (Trajectory Mining)*

**Referensi yang Perlu Ditambahkan:**
- [ ] Paper tentang Haversine formula dalam RS
- [ ] Survey CARS terbaru (2020-2023)
- [ ] Case study tourism RS di Indonesia (jika ada)

---

### 3.4 Metodologi

**Status:** ✅ Selesai

**Konten:**
1. **Dataset:**
   - Tabel karakteristik dataset (4.362 records, 892 users, 78 places)
   - Data cleaning pipeline (duplikat, outlier, cold-start filtering)
   - EDA: distribusi rating, sparsity 93.73%, coverage geografis

2. **Algoritma:**
   - **Baseline CF:** Formula Pearson Correlation, K=30 neighbors
   - **Context-Aware CF:** Pre-filtering Haversine (radius 10 km), centroid-based reference location
   - Diagram alir kedua algoritma

3. **Eksperimen:**
   - 5-Fold Stratified CV (random seed = 42)
   - Metrik: MAE (primary), RMSE (secondary)
   - Uji statistik: Paired T-Test, Cohen's d

4. **Hyperparameter:**
   - Tabel justifikasi K=30, radius=10 km (validated via grid search)

---

### 3.5 Hasil & Analisis

**Status:** ✅ Selesai

**Konten:**
1. **Hasil Utama:**
   - Tabel 1: MAE/RMSE per fold (5 rows)
   - Tabel 2: Agregasi mean ± std (Baseline vs Context-Aware)
   - **Temuan:** MAE Context-Aware 0.6511 < Baseline 0.6720 (penurunan 3.11%)

2. **Uji Statistik:**
   - Tabel 3: Paired T-Test result (t-stat = 18.72, p < 0.001)
   - Effect size: Cohen's d = 8.37 (very large practical significance)

3. **Visualisasi:**
   - **Figure 1:** Boxplot perbandingan MAE
   - **Figure 2:** Bar chart improvement per fold
   - **Figure 3:** Scatter plot predicted vs actual (Fold 1)

4. **Analisis Tambahan:**
   - Tabel 4: Error analysis by distance bin (Near/Medium/Far)
   - Coverage rate: 87.7% prediksi menggunakan CF penuh
   - 12.3% prediksi ter-filter (item di luar radius)

---

### 3.6 Diskusi

**Status:** 🔄 Draft (60% selesai)

**Konten Utama:**
1. **Interpretasi Hasil:**
   - ✅ Mengapa perbaikan 3.11% signifikan pada skala 1-5?
   - ✅ Perbaikan terbesar pada destinasi dekat (3.88%) — sesuai desain
   - 🔄 Perbandingan dengan literatur (Zheng et al. 2010: 4.2% improvement)

2. **Implikasi Praktis:**
   - ✅ Rekomendasi lebih feasible untuk rute perjalanan
   - ✅ Trade-off: coverage 87.7% (vs 100% baseline) acceptable
   - 🔄 Aplikasi pada platform riil (mobile app scenario)

3. **Limitasi:**
   - ✅ Dimensi temporal tidak dipertimbangkan (jam operasional, musim)
   - ✅ Threshold 10 km fixed (tidak adaptif per user)
   - ✅ Evaluasi offline (tidak ada validasi pengguna riil)
   - ✅ Dataset bias positivity (79% rating ≥ 4)

4. **Future Work:**
   - 🔄 Integrasi dimensi temporal (contextual modeling)
   - 🔄 Adaptive threshold berdasarkan user profile
   - 🔄 Online evaluation dengan A/B testing

---

### 3.7 Kesimpulan

**Status:** ✅ Selesai

**Draft:**

> Penelitian ini berhasil membuktikan bahwa integrasi pembobotan *Context-Aware* berbasis jarak geografis ke dalam algoritma *User-Based Collaborative Filtering* mampu meningkatkan akurasi prediksi rating secara signifikan pada domain sistem rekomendasi pariwisata Kota Semarang. Eksperimen menggunakan dataset 4.362 ulasan riil dan protokol validasi ketat (*5-Fold Cross Validation*) menunjukkan penurunan *Mean Absolute Error* sebesar 3,11% (MAE 0,6511 vs 0,6720) dengan signifikansi statistik sangat tinggi (*p* < 0,001). Perbaikan terbesar terkonsentrasi pada pasangan user-item dengan destinasi geografis yang dekat (perbaikan 3,88%), memvalidasi efektivitas strategi *spatial pre-filtering*. Penelitian ini mengisi tiga gap utama: (1) *Context Gap* — membuktikan pentingnya dimensi spasial pada CF pariwisata, (2) *Method Gap* — menyediakan implementasi konkret Context-Aware CF untuk pariwisata lokal Indonesia, dan (3) *Evaluation Gap* — menggunakan validasi robust yang dapat direproduksi. Penelitian lanjutan dapat mengeksplorasi integrasi dimensi temporal dan adaptif threshold berbasis profil pengguna untuk meningkatkan personalisasi lebih lanjut.

---

### 3.8 Daftar Pustaka

**Status:** 🔄 Review (perlu tambah 3-5 referensi)

**Referensi yang Sudah Ada (15 items):**
1. Adomavicius & Tuzhilin (2011)
2. Brilhante et al. (2015)
3. Cholil et al. (2023)
4. Herlocker et al. (2004)
5. Linden et al. (2003)
6. Ricci et al. (2015)
7. Zheng et al. (2010)
8. ... (8 referensi tambahan dari literatur review)

**Referensi yang Perlu Ditambahkan:**
- [ ] Survey CARS terbaru (post-2020)
- [ ] Paper tentang spatial filtering pada RS
- [ ] Tourism RS di konteks Asia/Indonesia

---

## 4. Checklist Penulisan

### 4.1 Kualitas Konten

- [x] Problem statement clear & testable
- [x] Gap literatur teridentifikasi dan dijustifikasi
- [x] Metodologi reproducible (seed, hyperparameter documented)
- [x] Hasil dipresentasikan dengan tabel & figure yang informatif
- [x] Uji statistik executed dengan benar (p-value, effect size)
- [x] Limitasi diakui secara transparan
- [x] Kontribusi terhubung langsung dengan gap

### 4.2 Format & Style

- [x] Bahasa Indonesia akademik formal
- [x] Kalimat pasif (preferred dalam paper Indonesia)
- [x] Istilah teknis konsisten (CF, CARS, MAE, RMSE)
- [x] Referensi APA style
- [ ] Abstract dalam bahasa Inggris (jika required oleh jurnal) — **Pending**
- [ ] Keywords dalam bahasa Inggris — **Pending**

### 4.3 Visualisasi

- [x] Figure 1: Boxplot MAE comparison (high-res PNG)
- [x] Figure 2: Improvement per fold (bar chart)
- [x] Figure 3: Scatter predicted vs actual
- [ ] Figure 4: Geographic map distribusi destinasi (optional) — **Pending**
- [x] Semua figure memiliki caption lengkap

### 4.4 Tabel

- [x] Tabel 1: Karakteristik dataset
- [x] Tabel 2: Hasil per fold (MAE/RMSE)
- [x] Tabel 3: Agregasi hasil + uji statistik
- [x] Tabel 4: Error analysis by distance bin
- [x] Semua tabel formatted (borders, alignment)

---

## 5. Review & Revision Cycle

### 5.1 Self-Review Checklist

- [x] Semua claim didukung oleh data/referensi
- [x] Tidak ada placeholder text (`TODO`, `[FILL THIS]`)
- [x] Formula matematis ditulis dengan benar (LaTeX notation)
- [x] Semua figure & table direferensikan dalam teks
- [x] Typo & grammar check (Grammarly/LanguageTool)
- [ ] Abstract memenuhi batas 250 kata — **Pending verification**

### 5.2 Pembimbing Feedback (Siklus 1)

**Tanggal Review:** [BELUM DILAKUKAN]

**Feedback:**
- [ ] [TBD]

**Action Items:**
- [ ] [TBD]

### 5.3 Pembimbing Feedback (Siklus 2)

**Tanggal Review:** [BELUM DILAKUKAN]

**Feedback:**
- [ ] [TBD]

**Action Items:**
- [ ] [TBD]

---

## 6. Persiapan Presentasi

### 6.1 Slide Presentasi

**Status:** ⏳ Belum Mulai

**Outline:**
1. Title Slide (Judul, Nama, NIM, Pembimbing)
2. Background & Motivation (1-2 slide)
3. Problem Statement & Gap (1 slide)
4. Research Question & Hypothesis (1 slide)
5. Methodology (2-3 slide)
   - Dataset
   - Baseline vs Context-Aware CF
   - Eksperimen protocol
6. Results (2-3 slide)
   - Tabel hasil
   - Visualisasi utama (Boxplot, Improvement)
   - Uji statistik
7. Discussion (1-2 slide)
   - Interpretasi
   - Limitasi
8. Conclusion & Future Work (1 slide)
9. Q&A

**Target:** 12-15 slide (presentasi 15 menit)

### 6.2 Demo (Optional)

**Status:** ⏳ Belum Direncanakan

**Opsi:**
- [ ] Interactive demo: input user location → output rekomendasi (Streamlit/Flask)
- [ ] Video demo: perbandingan visual Baseline vs Context-Aware recommendations

---

## 7. Target Publikasi

### 7.1 Jurnal Lokal (Primary Target)

**Opsi:**
1. **Jurnal Informatika dan Rekayasa Perangkat Lunak** (Sinta 5)
   - Scope: CF, RS, Tourism
   - Format: 12-15 halaman
   - Review time: 2-3 bulan

2. **Jurnal RESTI (Rekayasa Sistem dan Teknologi Informasi)** (Sinta 2)
   - Scope: AI, ML, RS
   - Format: 10-12 halaman
   - Review time: 3-4 bulan

**Keputusan:** [PENDING — Diskusi dengan pembimbing]

### 7.2 Konferensi (Secondary Target)

**Opsi:**
1. **ICACSIS** (Indonesian Conference on Advanced Computer Science and Information Systems)
   - Deadline: Biasanya Juli-Agustus
   - Publikasi: IEEE Xplore (Scopus-indexed)

2. **SIET** (Seminar Informatika dan Teknologi)
   - Regional conference (Jawa Tengah)
   - Publikasi: Prosiding lokal

---

## 8. Timeline Penyelesaian

| Task | Target Selesai | Status |
|------|----------------|--------|
| Draft lengkap (bagian 1-6) | Minggu 12 (2024-03-18) | 🔄 85% |
| Revisi Tinjauan Pustaka | Minggu 12 | 🔄 70% |
| Self-review & polish | Minggu 13 (2024-03-25) | ⏳ Belum Mulai |
| Submit ke pembimbing | Minggu 13 | ⏳ Belum Mulai |
| Revisi berdasarkan feedback | Minggu 14 (2024-04-01) | ⏳ Belum Mulai |
| Finalisasi paper | Minggu 14 | ⏳ Belum Mulai |
| Persiapan presentasi | Minggu 14 | ⏳ Belum Mulai |

---

## 9. Deliverable

### 9.1 Dokumen

- [ ] **Paper draft final** (PDF, 12-15 halaman)
- [ ] **Abstract bahasa Inggris** (jika diperlukan jurnal)
- [ ] **Slide presentasi** (PPTX/PDF, 12-15 slide)
- [ ] **Supplementary materials:**
  - [ ] Source code (GitHub repo)
  - [ ] Dataset metadata (bukan raw data — privacy concern)
  - [ ] Reproducibility guide (README.md)

### 9.2 Artefak Penelitian

- [x] Dataset clean (4.362 records)
- [x] Source code (baseline CF, context-aware CF)
- [x] Eksperimen results (JSON, CSV)
- [x] Visualisasi (3 figures PNG high-res)
- [x] Tabel hasil (4 tabel CSV)

---

## 10. Lessons Learned

### 10.1 Writing Process

> **Insight:** Menulis paper secara incremental (per bagian) lebih efisien dibanding menulis linear dari pendahuluan ke kesimpulan. Bagian Metodologi dan Hasil lebih mudah ditulis duluan karena sudah jelas strukturnya.

### 10.2 Visualisasi Efektif

> **Insight:** Boxplot lebih komunikatif dibanding bar chart untuk menunjukkan distribusi + outlier. Scatter plot predicted vs actual penting untuk menunjukkan pola error (bukan hanya angka MAE).

### 10.3 Limitasi Transparansi

> **Insight:** Mengakui limitasi secara transparan (tidak memperhitungkan temporal, threshold fixed) justru meningkatkan kredibilitas paper, bukan melemahkan.

---

## 11. Catatan Penting

### 11.1 Klaim yang Perlu Dihindari

- ❌ "Metode ini adalah yang terbaik untuk semua kasus pariwisata"
- ❌ "Context-Aware CF menggantikan semua metode CF lain"
- ✅ "Context-Aware CF terbukti lebih akurat dibanding Baseline CF pada konteks pariwisata Semarang dengan perbaikan 3.11%"

### 11.2 Aspek Etis

- Dataset tidak mengandung PII (Personally Identifiable Information)
- User ID sudah di-hash
- Geolokasi hanya untuk destinasi publik (bukan lokasi user)

---

## 12. Approval Checklist

- [x] Draft bagian Pendahuluan, Metodologi, Hasil completed
- [ ] Tinjauan Pustaka completed (70% → target 100%) — **Pending**
- [ ] Diskusi & Kesimpulan reviewed — **Pending review**
- [ ] Semua visualisasi & tabel integrated
- [ ] Abstract final (bahasa Indonesia + Inggris)
- [ ] Daftar pustaka complete (target 18-20 referensi)
- [ ] Self-review checklist passed
- [ ] Ready for pembimbing review

**Status:** 🔄 Sedang Berjalan — Target submit ke pembimbing: **2024-03-25**

---

**Last Updated:** 2024-03-18  
**Next Milestone:** Submit draft ke pembimbing untuk review cycle 1
