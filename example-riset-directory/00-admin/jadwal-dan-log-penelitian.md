# Jadwal dan Log Penelitian

**Judul:** Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering

**Peneliti:** Kayla Putri Arsonisr  
**NIM:** 240202837  
**Program Studi:** Teknik Informatika (Kelas 4IKRA)  
**Target Publikasi:** Skripsi / Jurnal Lokal

---

## 1. Jadwal Pelaksanaan

| Tahap | Kegiatan | Target Selesai | Status | Keterangan |
|-------|----------|----------------|--------|------------|
| **Tahap 0** | Identifikasi Masalah & Proposal | Minggu 1-2 | ✅ Selesai | Problem statement dan gap analysis |
| **Tahap 1** | Studi Literatur & Perancangan Arsitektur | Minggu 3-4 | ✅ Selesai | Review paper CF dan Context-Aware |
| **Tahap 2** | Pengumpulan & Preprocessing Data | Minggu 5-6 | ✅ Selesai | Scraping 4.362 ulasan Google Maps |
| **Tahap 3** | Implementasi Algoritma | Minggu 7-8 | ✅ Selesai | Baseline CF dan Context-Aware CF |
| **Tahap 4** | Eksperimen & Evaluasi | Minggu 9-10 | ✅ Selesai | 5-Fold CV, MAE: 0.651 vs 0.672 |
| **Tahap 5** | Analisis Hasil & Visualisasi | Minggu 11 | ✅ Selesai | Grafik perbandingan dan uji statistik |
| **Tahap 6** | Penulisan Laporan/Manuskrip | Minggu 12-13 | 🔄 Sedang Berjalan | Draft paper dan dokumentasi |
| **Tahap 7** | Review & Revisi | Minggu 14 | ⏳ Belum Mulai | Feedback pembimbing |

---

## 2. Log Penelitian

### 2024-01-15 — Inisiasi Proyek
- ✅ Identifikasi masalah: CF standar mengabaikan jarak geografis
- ✅ Definisi scope: Dataset pariwisata Kota Semarang
- ✅ Setup repository penelitian

### 2024-01-22 — Studi Literatur
- ✅ Review paper Cholil et al. (2023) tentang CF standar
- ✅ Analisis gap: Context-Awareness belum diterapkan
- ✅ Rancang metodologi: integrasi filter spasial dengan Haversine

### 2024-02-05 — Pengumpulan Data
- ✅ Scraping ulasan Google Maps area Semarang
- ✅ Total dataset: 4.362 ulasan (0 missing values)
- ✅ Metadata: UserID, PlaceID, Rating, Latitude, Longitude, Timestamp

### 2024-02-12 — Preprocessing & EDA
- ✅ Cleaning data: hapus duplikat dan outlier
- ✅ Verifikasi data quality: completeness, consistency, validity
- ✅ Statistik deskriptif: distribusi rating dan coverage geografis

### 2024-02-19 — Implementasi Baseline
- ✅ Implementasi User-Based Collaborative Filtering standar
- ✅ Similarity metric: Pearson Correlation
- ✅ Validasi fungsional: prediksi rating berhasil

### 2024-02-26 — Implementasi Context-Aware
- ✅ Integrasi filter jarak: Haversine formula
- ✅ Threshold jarak: 10 km (berdasarkan eksplorasi awal)
- ✅ Kombinasi weighted similarity: context + rating

### 2024-03-04 — Eksperimen Utama
- ✅ Setup: 5-Fold Cross Validation
- ✅ Baseline CF: MAE = 0.672 (±0.018)
- ✅ Context-Aware CF: MAE = 0.651 (±0.015)
- ✅ Penurunan error: 3.1% (signifikan, p < 0.05)

### 2024-03-11 — Analisis Hasil
- ✅ Uji statistik: Paired T-Test
- ✅ Visualisasi: boxplot MAE, scatter plot geografis
- ✅ Interpretasi: hipotesis H₁ diterima

### 2024-03-18 — Dokumentasi (Ongoing)
- 🔄 Penulisan draft paper
- 🔄 Persiapan presentasi
- ⏳ Revisi berdasarkan feedback pembimbing

---

## 3. Risiko dan Mitigasi

| Risiko | Probabilitas | Dampak | Mitigasi | Status |
|--------|--------------|--------|----------|--------|
| Data sparsity tinggi | Medium | High | Gunakan threshold minimum rating per user | ✅ Dimitigasi |
| Overfitting pada fold tertentu | Medium | Medium | 5-Fold CV dengan random seed tetap | ✅ Dimitigasi |
| Threshold jarak tidak optimal | Low | Medium | Grid search 5-15 km | ✅ Dimitigasi |
| Baseline terlalu lemah | Low | High | Replikasi paper Cholil et al. (2023) | ✅ Dimitigasi |

---

## 4. Keputusan Desain Kritis

### 4.1 Pemilihan Metrik
- **Primary Metric:** Mean Absolute Error (MAE)
  - Justifikasi: Standar industri, linear, mudah diinterpretasi
- **Secondary Metric:** Root Mean Square Error (RMSE)
  - Justifikasi: Menghukum error besar

### 4.2 Validasi Strategi
- **5-Fold Cross Validation**
  - Justifikasi: Balance antara bias-variance, menghindari data leakage
  - Random seed: 42 (reproducibility)

### 4.3 Threshold Jarak
- **10 km** dipilih sebagai radius optimal
  - Justifikasi: Median jarak perjalanan turis di Semarang
  - Validated via grid search (5, 7.5, 10, 12.5, 15 km)

---

## 5. Catatan Penting

### Kendala Teknis
- Dataset Google Maps memiliki bias temporal (lebih banyak review di akhir pekan)
- Beberapa destinasi memiliki coverage user sangat rendah (< 5 reviews)

### Limitasi Penelitian
- Dataset hanya mencakup user yang aktif memberi review (tidak mewakili silent tourists)
- Tidak memperhitungkan faktor temporal (jam operasional) dalam konteks ini
- Threshold 10 km bersifat fixed, tidak adaptif per user

### Temuan Menarik
- Destinasi dengan rating tinggi namun terisolasi (> 15 km dari cluster) jarang direkomendasikan Baseline CF
- Context-Aware CF berhasil meningkatkan diversity rekomendasi tanpa mengorbankan akurasi

---

## 6. Artefak dan Referensi

| Dokumen | Lokasi | Status |
|---------|--------|--------|
| Proposal Penelitian | [../01-proposal/](../01-proposal/) | ✅ Selesai |
| Matriks Literatur | [../02-literatur/](../02-literatur/) | ✅ Selesai |
| Diagram Arsitektur | [../03-teori/](../03-teori/) | ✅ Selesai |
| Dataset Raw & Clean | [../04-data/](../04-data/) | ✅ Selesai |
| Source Code | [../05-kode/](../05-kode/) | ✅ Selesai |
| Hasil Eksperimen | [../06-output/](../06-output/) | ✅ Selesai |
| Draft Paper | [../07-manuskrip/](../07-manuskrip/) | 🔄 Sedang Berjalan |
| Laporan Akhir | [../08-laporan/](../08-laporan/) | ⏳ Belum Mulai |

---

**Terakhir diperbarui:** 2024-03-18  
**Status Keseluruhan:** 🔄 Tahap Penulisan (85% selesai)
