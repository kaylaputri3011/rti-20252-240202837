# Proposal Penelitian

**Judul:** Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering

**Peneliti:** Kayla Putri Arsonisr  
**NIM:** 240202837  
**Program Studi:** Teknik Informatika (Kelas 4IKRA)  
**Target Publikasi:** Skripsi / Jurnal Lokal

---

## 1. Latar Belakang

### 1.1 Konteks Domain

Kota Semarang sebagai ibu kota Provinsi Jawa Tengah memiliki beragam destinasi wisata yang tersebar di area geografis yang luas, mencakup wisata religi, kuliner, alam, dan sejarah. Heterogenitas pilihan ini menimbulkan tantangan bagi wisatawan dalam menentukan destinasi yang sesuai dengan preferensi personal mereka — fenomena yang dikenal sebagai *information overload*. Sistem rekomendasi berbasis *Collaborative Filtering* (CF) telah diimplementasikan untuk memitigasi masalah ini dengan memanfaatkan pola kemiripan preferensi antar pengguna (Cholil et al., 2023).

### 1.2 Permasalahan

Implementasi *User-Based Collaborative Filtering* standar pada domain pariwisata memiliki keterbatasan mendasar: algoritma hanya memperhitungkan matriks rating pengguna-item tanpa mempertimbangkan **konteks geografis** destinasi yang direkomendasikan. Akibatnya, sistem dapat merekomendasikan destinasi dengan rating tinggi namun terletak puluhan kilometer terpisah dari lokasi pengguna saat ini atau dari destinasi lain dalam rencana perjalanan, sehingga menghasilkan rekomendasi yang tidak praktis dan tidak efisien dari perspektif rute perjalanan.

Cholil et al. (2023) mengimplementasikan CF murni untuk pariwisata Semarang dengan metrik evaluasi berbasis akurasi prediksi rating, namun tidak mengintegrasikan dimensi spasial sebagai bagian dari logika rekomendasi. Fenomena ini menciptakan **gap metodologis**: sistem rekomendasi yang akurat secara matematis namun tidak logis secara geografis.

### 1.3 Dampak Masalah

Rekomendasi destinasi yang mengabaikan jarak geografis berdampak pada:
- **Inefisiensi rute perjalanan:** Wisatawan harus menempuh jarak yang tidak perlu, meningkatkan biaya transportasi dan waktu perjalanan.
- **User experience yang buruk:** Rekomendasi yang tidak praktis menurunkan kepercayaan pengguna terhadap sistem.
- **Opportunity cost:** Destinasi berkualitas yang terletak dalam radius terjangkau namun memiliki rating sedikit lebih rendah diabaikan oleh sistem.

---

## 2. Rumusan Masalah

Berdasarkan latar belakang yang telah dipaparkan, masalah penelitian dirumuskan sebagai berikut:

**Problem Statement:**

> Sistem rekomendasi pariwisata berbasis *User-Based Collaborative Filtering* standar yang hanya bergantung pada matriks rating pengguna-item rentan menghasilkan rekomendasi yang tidak rasional secara geografis, di mana destinasi yang direkomendasikan terpisah dalam jarak yang tidak efisien untuk dikunjungi dalam satu perjalanan. Gap ini muncul karena algoritma CF konvensional tidak mengintegrasikan variabel konteks spasial (jarak geografis antar destinasi) ke dalam mekanisme komputasi similaritas dan prediksi rating. Oleh karena itu, diperlukan pengembangan metode yang mampu menyeimbangkan akurasi prediksi rating dengan rasionalitas geografis rekomendasi.

**Research Question (RQ):**

> Apakah integrasi pembobotan *Context-Aware* berbasis jarak geografis pada algoritma *User-Based Collaborative Filtering* mampu menghasilkan skor *Mean Absolute Error* (MAE) yang lebih rendah dibandingkan *User-Based Collaborative Filtering* standar pada dataset rating destinasi wisata Kota Semarang?

**Tipe RQ:** Improvement (membandingkan metode yang dikembangkan dengan baseline eksisting)

---

## 3. Tujuan Penelitian

### 3.1 Tujuan Umum

Mengembangkan dan mengevaluasi metode *Context-Aware Collaborative Filtering* yang mengintegrasikan filter spasial berbasis jarak geografis untuk meningkatkan akurasi prediksi rating pada sistem rekomendasi destinasi wisata Kota Semarang.

### 3.2 Tujuan Khusus

1. Mengimplementasikan algoritma *User-Based Collaborative Filtering* standar sebagai baseline yang mereplikasi penelitian Cholil et al. (2023).
2. Merancang dan mengimplementasikan metode *Context-Aware Collaborative Filtering* yang mengintegrasikan pembobotan jarak geografis menggunakan formula Haversine.
3. Melakukan eksperimen terkontrol dengan skema *5-Fold Cross Validation* untuk mengevaluasi performa kedua metode pada dataset 4.362 ulasan destinasi wisata Kota Semarang.
4. Mengukur dan membandingkan tingkat akurasi prediksi kedua metode menggunakan metrik *Mean Absolute Error* (MAE) dan *Root Mean Square Error* (RMSE).
5. Melakukan uji signifikansi statistik (*Paired T-Test*) untuk memvalidasi hipotesis perbaikan performa.

---

## 4. Hipotesis Penelitian

### 4.1 Hipotesis Null (H₀)

> Tidak terdapat penurunan nilai *Mean Absolute Error* (MAE) yang signifikan secara statistik antara metode *Context-Aware Collaborative Filtering* dengan pembobotan jarak geografis dibandingkan metode *User-Based Collaborative Filtering* standar pada dataset rating destinasi wisata Kota Semarang.

### 4.2 Hipotesis Alternatif (H₁)

> Terdapat penurunan nilai *Mean Absolute Error* (MAE) yang signifikan secara statistik pada metode *Context-Aware Collaborative Filtering* dengan pembobotan jarak geografis dibandingkan metode *User-Based Collaborative Filtering* standar pada dataset rating destinasi wisata Kota Semarang.

### 4.3 Kriteria Signifikansi

- **Threshold statistik:** *p-value* < 0.05 (uji *Paired T-Test*)
- **Threshold praktis:** Penurunan MAE minimal 2% (justifikasi: pada skala rating 1-5, penurunan di bawah 2% dianggap tidak berdampak signifikan pada pengalaman pengguna)

---

## 5. Kontribusi Penelitian

### 5.1 Kontribusi Teoretis

- **Context Gap:** Membuktikan secara empiris bahwa integrasi dimensi spasial ke dalam algoritma CF mampu meningkatkan akurasi prediksi rating pada domain pariwisata.
- **Method Gap:** Menyediakan metode konkret untuk mengoperasionalisasikan *context-awareness* (jarak geografis) ke dalam mekanisme komputasi similaritas pada CF.

### 5.2 Kontribusi Praktis

- Menyediakan bukti empiris kelayakan implementasi filter geografis pada sistem rekomendasi pariwisata lokal (Kota Semarang).
- Menghasilkan artefak berupa dataset ulasan terstruktur dan kode sumber yang dapat direproduksi untuk penelitian lanjutan.

### 5.3 Kontribusi Metodologis

- Validasi penggunaan *5-Fold Cross Validation* sebagai strategi mitigasi *data leakage* pada eksperimen CF dengan dataset pariwisata real-world.

---

## 6. Batasan Penelitian (Scope)

### 6.1 Domain

- Fokus pada destinasi wisata di wilayah administratif **Kota Semarang** (tidak mencakup Kabupaten Semarang).
- Jenis destinasi: semua kategori (wisata alam, religi, kuliner, sejarah).

### 6.2 Data

- Dataset: 4.362 ulasan riil dari Google Maps (periode 2020-2023).
- Tidak termasuk data ulasan dari platform lain (TripAdvisor, Instagram, dll.).

### 6.3 Metode

- Algoritma: *User-Based Collaborative Filtering* (tidak mencakup *Item-Based* atau *Matrix Factorization*).
- Konteks: Hanya dimensi spasial (jarak geografis); tidak mencakup dimensi temporal (jam operasional, musim, cuaca).

### 6.4 Evaluasi

- Metrik: MAE dan RMSE (metrik offline; tidak mencakup evaluasi *online* dengan pengguna riil).
- Validasi: *5-Fold Cross Validation* (tidak mencakup *Leave-One-Out* atau *Temporal Split*).

---

## 7. Tinjauan Pustaka (Ringkasan)

### 7.1 Collaborative Filtering

Collaborative Filtering adalah metode rekomendasi yang memanfaatkan pola preferensi kolektif pengguna untuk memprediksi rating item yang belum dikonsumsi oleh pengguna target (Ricci et al., 2015). Pendekatan *User-Based CF* mengasumsikan bahwa pengguna dengan histori rating serupa cenderung memiliki preferensi serupa di masa depan.

**Keterbatasan:** CF murni rentan terhadap masalah *data sparsity* dan tidak memperhitungkan konteks eksternal (Adomavicius & Tuzhilin, 2011).

### 7.2 Context-Aware Recommender Systems

*Context-Aware Recommender Systems* (CARS) mengintegrasikan informasi kontekstual (waktu, lokasi, cuaca, mood) ke dalam logika rekomendasi (Adomavicius et al., 2011). Pada domain pariwisata, konteks geografis menjadi faktor kritis karena berhubungan langsung dengan feasibilitas rekomendasi (Brilhante et al., 2015).

### 7.3 Penelitian Terkait

- **Cholil et al. (2023):** Implementasi CF standar untuk pariwisata Semarang tanpa integrasi konteks geografis.
- **Brilhante et al. (2015):** Penggunaan *Trajectory Mining* untuk rekomendasi rute wisata berbasis geolokasi.
- **Gap yang diisi:** Penelitian ini mengisi gap antara CF tradisional dengan CARS pada domain pariwisata lokal Semarang.

*(Detail lengkap matriks literatur: lihat [../02-literatur/matriks-literatur.md](../02-literatur/matriks-literatur.md))*

---

## 8. Metodologi Penelitian

### 8.1 Desain Penelitian

- **Tipe:** Eksperimental kuantitatif (offline evaluation)
- **Pendekatan:** *Within-subject design* (satu dataset, dua kondisi algoritma)

### 8.2 Dataset

| Atribut | Deskripsi |
|---------|-----------|
| Sumber | Google Maps Reviews (API scraping) |
| Jumlah record | 4.362 ulasan |
| Periode | 2020-2023 |
| Atribut | UserID, PlaceID, Rating (1-5), Latitude, Longitude, Timestamp |
| Missing values | 0 (data telah dibersihkan) |

### 8.3 Variabel Penelitian

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan |
|----------|------|--------|--------|-------|--------|
| Jenis Algoritma | IV | Metode rekomendasi | Kategori (Context-Aware CF vs Standar CF) | Nominal | — |
| Akurasi Prediksi | DV | Tingkat error prediksi rating | Mean Absolute Error (MAE) | Ratio | Poin (0-4) |
| Kondisi Validasi | CV | Validitas internal | K-Fold (K=5) | Ratio | — |

### 8.4 Prosedur Eksperimen

#### Tahap 1: Preprocessing
1. Data cleaning: hapus duplikat, outlier, dan user dengan < 3 rating.
2. Geocoding: validasi koordinat latitude/longitude setiap destinasi.
3. Splitting: 5-Fold Cross Validation (80% train, 20% test per fold).

#### Tahap 2: Implementasi Baseline (Standar CF)
1. Komputasi similaritas antar user menggunakan *Pearson Correlation*.
2. Prediksi rating berdasarkan weighted average dari K-nearest neighbors (K=30).

#### Tahap 3: Implementasi Context-Aware CF
1. Komputasi jarak geografis antar destinasi menggunakan **Haversine formula**.
2. Filter kandidat: hanya destinasi dalam radius 10 km dari lokasi referensi user.
3. Prediksi rating pada subset kandidat yang ter-filter.

#### Tahap 4: Evaluasi
1. Hitung MAE dan RMSE untuk setiap fold pada kedua metode.
2. Agregasi hasil: mean ± std across 5 folds.
3. Uji statistik: *Paired T-Test* untuk menguji signifikansi perbedaan MAE.

### 8.5 Tools dan Environment

- **Bahasa:** Python 3.9
- **Library:** pandas, numpy, scikit-learn, scipy, geopy
- **Compute:** Local machine (Intel Core i5, 16GB RAM)
- **Reproducibility:** Random seed = 42

*(Detail arsitektur teknis: lihat [../03-teori/arsitektur-sistem.md](../03-teori/arsitektur-sistem.md))*

---

## 9. Hasil yang Diharapkan

### 9.1 Metrik Kuantitatif

- **Baseline (Standar CF):** MAE ≈ 0.670 (berdasarkan replikasi Cholil et al., 2023)
- **Context-Aware CF:** MAE < 0.670 (target penurunan minimal 2%)

### 9.2 Validasi Hipotesis

- Jika MAE Context-Aware < MAE Standar **dan** p-value < 0.05 → H₁ diterima
- Jika tidak → H₀ diterima (metode tidak terbukti lebih baik)

### 9.3 Output Penelitian

1. Dataset terstruktur (4.362 records, geocoded)
2. Source code kedua algoritma (reproducible)
3. Tabel hasil eksperimen (MAE per fold, agregat, p-value)
4. Visualisasi: boxplot MAE, scatter plot geografis, confusion matrix kategorikal
5. Draft paper (format jurnal lokal)

---

## 10. Jadwal Penelitian

| Tahap | Kegiatan | Durasi | Target Selesai |
|-------|----------|--------|----------------|
| 1 | Identifikasi masalah & proposal | 2 minggu | Minggu 2 |
| 2 | Studi literatur & perancangan | 2 minggu | Minggu 4 |
| 3 | Pengumpulan & preprocessing data | 2 minggu | Minggu 6 |
| 4 | Implementasi algoritma | 2 minggu | Minggu 8 |
| 5 | Eksperimen & evaluasi | 2 minggu | Minggu 10 |
| 6 | Analisis hasil & visualisasi | 1 minggu | Minggu 11 |
| 7 | Penulisan laporan/paper | 2 minggu | Minggu 13 |
| 8 | Review & revisi | 1 minggu | Minggu 14 |

*(Jadwal detail dan log progres: lihat [../00-admin/jadwal-dan-log-penelitian.md](../00-admin/jadwal-dan-log-penelitian.md))*

---

## 11. Daftar Pustaka

Adomavicius, G., & Tuzhilin, A. (2011). Context-aware recommender systems. In *Recommender Systems Handbook* (pp. 217-253). Springer.

Adomavicius, G., Mobasher, B., Ricci, F., & Tuzhilin, A. (2011). Context-aware recommender systems. *AI Magazine, 32*(3), 67-80.

Brilhante, I., Macedo, J. A., Nardini, F. M., Perego, R., & Renso, C. (2015). TripBuilder: A tool for recommending sightseeing tours. In *Advances in Information Retrieval* (pp. 771-774). Springer.

Cholil, W., Handayani, T., & Wibowo, A. (2023). Sistem Rekomendasi Tempat Wisata Di Kota Semarang Menggunakan Metode Collaborative Filtering. *Jurnal Informatika dan Rekayasa Perangkat Lunak, 4*(2), 156-167.

Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems Handbook* (2nd ed.). Springer.

---

**Disetujui oleh:**

[__________________________]  
**Pembimbing**

**Tanggal:** _______________
