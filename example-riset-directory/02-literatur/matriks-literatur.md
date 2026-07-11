# Matriks Literatur

**Penelitian:** Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering

**Peneliti:** Kayla Putri Arsonisr (240202837)

---

## 1. Ringkasan Gap Analysis

| Dimensi Gap | Deskripsi | Diisi oleh Penelitian Ini |
|-------------|-----------|---------------------------|
| **Context Gap** | CF tradisional mengabaikan konteks geografis pada domain pariwisata | Integrasi filter spasial berbasis jarak Haversine |
| **Method Gap** | Belum ada implementasi Context-Aware CF untuk pariwisata Semarang | Implementasi dan evaluasi empiris dengan dataset lokal |
| **Evaluation Gap** | Evaluasi CF pariwisata sebelumnya tidak menggunakan validasi ketat (K-Fold) | 5-Fold Cross Validation dengan uji statistik |

---

## 2. Matriks Literatur Utama

| No | Penulis & Tahun | Judul | Metode | Dataset | Metrik | Temuan Utama | Keterbatasan | Relevansi dengan Penelitian Ini |
|----|-----------------|-------|--------|---------|--------|--------------|--------------|----------------------------------|
| 1 | **Cholil et al. (2023)** | Sistem Rekomendasi Tempat Wisata Di Kota Semarang Menggunakan Metode Collaborative Filtering | User-Based CF (Pearson Correlation) | Wisata Semarang (jumlah tidak disebutkan) | Akurasi sistem (tidak spesifik MAE/RMSE) | CF dapat diimplementasikan untuk pariwisata Semarang | Tidak memperhitungkan jarak geografis; evaluasi tidak ketat | **Baseline langsung** — Penelitian ini mereplikasi metode mereka sebagai baseline dan menambahkan dimensi spasial |
| 2 | **Adomavicius & Tuzhilin (2011)** | Context-Aware Recommender Systems | Survey CARS | — | — | Konteks (waktu, lokasi, mood) meningkatkan relevansi rekomendasi | Framework teoretis, bukan eksperimen konkret | **Landasan teoretis** — Justifikasi pentingnya context-awareness |
| 3 | **Brilhante et al. (2015)** | TripBuilder: A Tool for Recommending Sightseeing Tours | Trajectory Mining + Location-Based CF | Flickr geotagged photos | Precision, Recall | Rute wisata berbasis geolokasi lebih praktis | Fokus pada sequence, bukan akurasi rating | **Method inspiration** — Penggunaan Haversine untuk filter geografis |
| 4 | **Ricci et al. (2015)** | Recommender Systems Handbook | Survey berbagai metode RS | — | — | CF adalah metode paling mature untuk cold-start moderate | Buku umum, tidak spesifik pariwisata | **Dasar teoretis CF** — Definisi similarity metrics |
| 5 | **Zheng et al. (2010)** | Collaborative Filtering Meets Mobile Recommendation | Location-Based CF (LARS) | 164 users, 5.456 check-ins | MAE | Spatial smoothing menurunkan MAE | Dataset terbatas, domain berbeda (restoran) | **Empirical precedent** — Bukti bahwa spatial context meningkatkan akurasi |
| 6 | **Linden et al. (2003)** | Amazon.com Recommendations: Item-to-Item Collaborative Filtering | Item-Based CF | Amazon internal | Throughput, conversion | Scalability tinggi, namun tidak context-aware | Fokus pada skalabilitas, bukan akurasi geografis | **Kontras** — Menunjukkan keterbatasan CF murni pada konteks spasial |

---

## 3. Kategori Literatur

### 3.1 Foundational Papers (CF Tradisional)
- **Ricci et al. (2015):** Dasar teoretis User-Based vs Item-Based CF
- **Linden et al. (2003):** Implementasi CF skala industri (Amazon)

### 3.2 Context-Aware RS
- **Adomavicius & Tuzhilin (2011):** Framework CARS (pre-filtering, post-filtering, contextual modeling)
- **Zheng et al. (2010):** LARS — Location-Aware RS dengan spatial smoothing

### 3.3 Tourism-Specific RS
- **Cholil et al. (2023):** CF untuk pariwisata Semarang (baseline penelitian ini)
- **Brilhante et al. (2015):** Trajectory Mining untuk rekomendasi rute wisata

### 3.4 Evaluation Methodology
- **Herlocker et al. (2004):** *Evaluating Collaborative Filtering Recommender Systems* — Justifikasi pemilihan MAE/RMSE

---

## 4. Gap yang Diidentifikasi

### 4.1 Context Gap (Konteks Geografis Diabaikan)

**Literatur Pendukung:**
- Cholil et al. (2023) mengimplementasikan CF murni tanpa filter geografis.
- Adomavicius & Tuzhilin (2011) menyatakan bahwa konteks lokasi adalah salah satu dimensi kritis pada CARS, namun jarang diterapkan pada pariwisata lokal.

**Implikasi:**
- Sistem merekomendasikan destinasi berkualitas tinggi namun tidak feasible secara geografis (jarak > 20 km dari cluster utama).

**Diisi oleh Penelitian Ini:**
- Integrasi filter jarak 10 km menggunakan Haversine formula pada tahap pre-filtering.

### 4.2 Method Gap (Belum Ada Context-Aware CF untuk Semarang)

**Literatur Pendukung:**
- Zheng et al. (2010) menerapkan LARS pada domain restoran (AS).
- Brilhante et al. (2015) fokus pada trajectory mining (Eropa), bukan CF.

**Implikasi:**
- Tidak ada bukti empiris kelayakan Context-Aware CF pada pariwisata lokal Indonesia, khususnya Semarang.

**Diisi oleh Penelitian Ini:**
- Implementasi Context-Aware CF dengan dataset 4.362 ulasan riil Google Maps Semarang.

### 4.3 Evaluation Gap (Validasi Tidak Ketat)

**Literatur Pendukung:**
- Cholil et al. (2023) tidak menyebutkan protokol validasi (kemungkinan single train-test split).

**Implikasi:**
- Risiko *overfitting* dan hasil yang tidak generalizable.

**Diisi oleh Penelitian Ini:**
- 5-Fold Cross Validation + Paired T-Test untuk validasi signifikansi.

---

## 5. Justifikasi Pemilihan Metrik

### 5.1 Mean Absolute Error (MAE)

**Definisi:**
$$MAE = \frac{1}{n} \sum_{i=1}^{n} |r_i - \hat{r}_i|$$

**Justifikasi:**
- Standar industri untuk evaluasi akurasi prediksi rating (Herlocker et al., 2004).
- Mudah diinterpretasi: MAE 0.65 berarti rata-rata error prediksi adalah 0.65 bintang (pada skala 1-5).
- Tidak menghukum outlier secara berlebihan (dibanding RMSE).

### 5.2 Root Mean Square Error (RMSE)

**Definisi:**
$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (r_i - \hat{r}_i)^2}$$

**Justifikasi:**
- Metrik sekunder untuk mendeteksi error ekstrem.
- Memberikan penalti lebih besar pada prediksi yang sangat meleset (kuadratik).

---

## 6. Theoretical Framework

### 6.1 User-Based Collaborative Filtering

**Prinsip:**
- Pengguna dengan histori rating serupa cenderung memiliki preferensi serupa.
- Similarity diukur dengan Pearson Correlation:

$$sim(u, v) = \frac{\sum_{i \in I_{uv}} (r_{ui} - \bar{r}_u)(r_{vi} - \bar{r}_v)}{\sqrt{\sum_{i \in I_{uv}} (r_{ui} - \bar{r}_u)^2} \sqrt{\sum_{i \in I_{uv}} (r_{vi} - \bar{r}_v)^2}}$$

### 6.2 Context-Aware Filtering (Pre-Filtering Approach)

**Prinsip:**
- Filter kandidat item sebelum komputasi CF berdasarkan konteks.
- Pada penelitian ini: hanya destinasi dalam radius 10 km yang menjadi kandidat.

**Formula Haversine (Jarak Geografis):**

$$d = 2r \arcsin\left(\sqrt{\sin^2\left(\frac{\phi_2 - \phi_1}{2}\right) + \cos(\phi_1)\cos(\phi_2)\sin^2\left(\frac{\lambda_2 - \lambda_1}{2}\right)}\right)$$

Di mana:
- $r$ = radius bumi (6.371 km)
- $\phi$ = latitude (radian)
- $\lambda$ = longitude (radian)

---

## 7. Ringkasan Kontribusi Penelitian terhadap Literatur

| Aspek | Kontribusi |
|-------|------------|
| **Teoretis** | Membuktikan empiris bahwa dimensi spasial meningkatkan akurasi CF pada domain pariwisata |
| **Metodologis** | Menyediakan protokol eksperimen ketat (5-Fold CV) untuk evaluasi CARS |
| **Praktis** | Menghasilkan dataset terstruktur pariwisata Semarang yang dapat digunakan penelitian lanjutan |
| **Lokal** | Mengisi gap penelitian pariwisata Indonesia (mayoritas penelitian CARS menggunakan dataset luar negeri) |

---

## 8. Referensi Lengkap

Adomavicius, G., & Tuzhilin, A. (2011). Context-aware recommender systems. In F. Ricci, L. Rokach, B. Shapira, & P. B. Kantor (Eds.), *Recommender Systems Handbook* (pp. 217-253). Springer.

Brilhante, I., Macedo, J. A., Nardini, F. M., Perego, R., & Renso, C. (2015). TripBuilder: A tool for recommending sightseeing tours. In *Advances in Information Retrieval* (pp. 771-774). Springer.

Cholil, W., Handayani, T., & Wibowo, A. (2023). Sistem Rekomendasi Tempat Wisata Di Kota Semarang Menggunakan Metode Collaborative Filtering. *Jurnal Informatika dan Rekayasa Perangkat Lunak, 4*(2), 156-167.

Herlocker, J. L., Konstan, J. A., Terveen, L. G., & Riedl, J. T. (2004). Evaluating collaborative filtering recommender systems. *ACM Transactions on Information Systems (TOIS), 22*(1), 5-53.

Linden, G., Smith, B., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering. *IEEE Internet Computing, 7*(1), 76-80.

Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems Handbook* (2nd ed.). Springer.

Zheng, V. W., Zheng, Y., Xie, X., & Yang, Q. (2010). Collaborative location and activity recommendations with GPS history data. In *Proceedings of the 19th International Conference on World Wide Web* (pp. 1029-1038). ACM.

---

**Catatan:** Matriks ini akan diperbarui jika literatur tambahan ditemukan selama proses penelitian.
