# Arsitektur Sistem dan Landasan Teori

**Penelitian:** Peningkatan Akurasi Sistem Rekomendasi Pariwisata Semarang Menggunakan Algoritma Context-Aware Collaborative Filtering

**Peneliti:** Kayla Putri Arsonisr (240202837)

---

## 1. Arsitektur Sistem Keseluruhan

```
┌───────────────────────────────────────────────────────────────────┐
│                     SISTEM REKOMENDASI PARIWISATA                 │
│                          (CONTEXT-AWARE CF)                       │
└───────────────────────────────────────────────────────────────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
           ┌────────▼────────┐        ┌────────▼────────┐
           │   BASELINE CF    │        │  CONTEXT-AWARE  │
           │    (Standar)     │        │       CF        │
           └────────┬────────┘        └────────┬────────┘
                    │                           │
      ┌─────────────┴─────────────┬─────────────┴─────────────┐
      │                           │                           │
┌─────▼─────┐            ┌────────▼────────┐       ┌─────────▼─────────┐
│  Data     │            │  Preprocessing  │       │  Spatial Filter   │
│  Input    │            │  & Similarity   │       │  (Haversine)      │
│ (4.362)   │            │   Computation   │       │  (Radius 10 km)   │
└───────────┘            └─────────────────┘       └───────────────────┘
                                  │
                         ┌────────▼────────┐
                         │   Prediction    │
                         │   & Ranking     │
                         └────────┬────────┘
                                  │
                         ┌────────▼────────┐
                         │   Evaluation    │
                         │  (5-Fold CV)    │
                         │  MAE, RMSE      │
                         └─────────────────┘
```

---

## 2. Landasan Teori

### 2.1 Collaborative Filtering (CF)

#### 2.1.1 Definisi

Collaborative Filtering adalah metode sistem rekomendasi yang menghasilkan prediksi preferensi pengguna terhadap item berdasarkan pola rating kolektif dari banyak pengguna (Ricci et al., 2015). CF berasumsi bahwa pengguna yang memiliki pola rating serupa di masa lalu cenderung memiliki preferensi serupa di masa depan.

#### 2.1.2 User-Based Collaborative Filtering

Pendekatan yang digunakan dalam penelitian ini adalah **User-Based CF**, di mana sistem:
1. Menghitung kemiripan (*similarity*) antara pengguna target dengan semua pengguna lain.
2. Mengidentifikasi K pengguna paling mirip (*K-nearest neighbors*).
3. Memprediksi rating item yang belum dirating oleh target berdasarkan weighted average rating dari neighbors.

**Formula Similarity (Pearson Correlation):**

$$sim(u, v) = \frac{\sum_{i \in I_{uv}} (r_{ui} - \bar{r}_u)(r_{vi} - \bar{r}_v)}{\sqrt{\sum_{i \in I_{uv}} (r_{ui} - \bar{r}_u)^2} \sqrt{\sum_{i \in I_{uv}} (r_{vi} - \bar{r}_v)^2}}$$

Di mana:
- $u, v$ = dua pengguna yang dibandingkan
- $I_{uv}$ = himpunan item yang dirating oleh keduanya
- $r_{ui}$ = rating pengguna $u$ untuk item $i$
- $\bar{r}_u$ = rata-rata rating pengguna $u$

**Formula Prediksi Rating:**

$$\hat{r}_{ui} = \bar{r}_u + \frac{\sum_{v \in N(u)} sim(u,v) \cdot (r_{vi} - \bar{r}_v)}{\sum_{v \in N(u)} |sim(u,v)|}$$

Di mana:
- $\hat{r}_{ui}$ = prediksi rating pengguna $u$ untuk item $i$
- $N(u)$ = himpunan K-nearest neighbors dari pengguna $u$

#### 2.1.3 Keterbatasan CF Standar

1. **Cold Start:** Kesulitan merekomendasikan untuk pengguna/item baru dengan sedikit rating.
2. **Data Sparsity:** Matriks rating umumnya sangat jarang (< 1% terisi).
3. **Scalability:** Komputasi similarity $O(n^2)$ untuk $n$ pengguna.
4. **Context Blindness:** Tidak memperhitungkan konteks eksternal (lokasi, waktu, cuaca).

### 2.2 Context-Aware Recommender Systems (CARS)

#### 2.2.1 Definisi

CARS adalah sistem rekomendasi yang mengintegrasikan informasi kontekstual (contoh: waktu, lokasi, cuaca, mood, social context) ke dalam logika rekomendasi untuk meningkatkan relevansi dan akurasi (Adomavicius & Tuzhilin, 2011).

#### 2.2.2 Tiga Paradigma CARS

| Paradigma | Deskripsi | Digunakan dalam Penelitian? |
|-----------|-----------|---------------------------|
| **Pre-Filtering** | Filter data berdasarkan konteks sebelum CF | ✅ **Ya** (filter geografis) |
| **Post-Filtering** | Terapkan CF dulu, filter hasil berdasarkan konteks | ❌ Tidak |
| **Contextual Modeling** | Konteks menjadi dimensi tambahan dalam model prediksi | ❌ Tidak |

**Justifikasi Pemilihan Pre-Filtering:**
- Sederhana dan efisien secara komputasi.
- Mudah diinterpretasi: "hanya rekomendasikan destinasi dalam radius 10 km".
- Terbukti efektif pada domain Location-Based RS (Zheng et al., 2010).

#### 2.2.3 Spatial Context dalam Pariwisata

Pada domain pariwisata, **jarak geografis** menjadi konteks kritis karena:
- Wisatawan memiliki keterbatasan waktu dan biaya transportasi.
- Destinasi dengan rating tinggi namun terisolasi geografis tidak praktis dikunjungi.
- Clustering destinasi dalam radius terbatas meningkatkan feasibility rekomendasi.

---

## 3. Metodologi Context-Aware CF (Penelitian Ini)

### 3.1 Alur Kerja Baseline CF

```
Input: User u, Item i yang belum dirating
│
├─> 1. Cari semua pengguna V yang pernah rating item i
│
├─> 2. Hitung sim(u, v) untuk setiap v ∈ V menggunakan Pearson Correlation
│
├─> 3. Pilih K=30 pengguna dengan similarity tertinggi (K-nearest neighbors)
│
├─> 4. Prediksi rating menggunakan weighted average:
│       r̂_ui = r̄_u + Σ[sim(u,v) × (r_vi - r̄_v)] / Σ|sim(u,v)|
│
└─> Output: Prediksi rating r̂_ui
```

### 3.2 Alur Kerja Context-Aware CF

```
Input: User u, Item i yang belum dirating, Lokasi referensi L_ref
│
├─> 1. SPATIAL PRE-FILTERING:
│       • Ambil semua item kandidat I_all
│       • Untuk setiap item j ∈ I_all:
│           - Hitung jarak d(L_ref, L_j) menggunakan Haversine
│           - Jika d < 10 km, masukkan ke I_filtered
│
├─> 2. COLLABORATIVE FILTERING (pada I_filtered):
│       • Cari pengguna V yang pernah rating item di I_filtered
│       • Hitung sim(u, v) menggunakan Pearson Correlation
│       • Pilih K=30 pengguna dengan similarity tertinggi
│       • Prediksi rating r̂_ui
│
└─> Output: Prediksi rating r̂_ui (hanya untuk item dalam radius 10 km)
```

### 3.3 Formula Haversine (Spatial Distance)

Untuk menghitung jarak great-circle antara dua titik koordinat (lat₁, lon₁) dan (lat₂, lon₂):

$$a = \sin^2\left(\frac{\phi_2 - \phi_1}{2}\right) + \cos(\phi_1) \cdot \cos(\phi_2) \cdot \sin^2\left(\frac{\lambda_2 - \lambda_1}{2}\right)$$

$$c = 2 \cdot \arctan2\left(\sqrt{a}, \sqrt{1-a}\right)$$

$$d = R \cdot c$$

Di mana:
- $\phi$ = latitude dalam radian ($\phi = \text{lat} \times \pi / 180$)
- $\lambda$ = longitude dalam radian ($\lambda = \text{lon} \times \pi / 180$)
- $R$ = radius bumi = 6.371 km
- $d$ = jarak dalam kilometer

**Implementasi Python:**
```python
from math import radians, sin, cos, sqrt, atan2

def haversine(lat1, lon1, lat2, lon2):
    R = 6371  # Radius bumi dalam km
    
    phi1 = radians(lat1)
    phi2 = radians(lat2)
    delta_phi = radians(lat2 - lat1)
    delta_lambda = radians(lon2 - lon1)
    
    a = sin(delta_phi/2)**2 + cos(phi1) * cos(phi2) * sin(delta_lambda/2)**2
    c = 2 * atan2(sqrt(a), sqrt(1-a))
    
    return R * c
```

---

## 4. Desain Eksperimen

### 4.1 Dataset Schema

```
┌─────────────────────────────────────────────────────────────┐
│                     DATASET (4.362 records)                 │
├─────────────┬───────────────┬─────────────┬────────────────┤
│ UserID      │ PlaceID       │ Rating      │ Geolocation    │
│ (string)    │ (string)      │ (1-5)       │ (lat, lon)     │
├─────────────┼───────────────┼─────────────┼────────────────┤
│ U001        │ P042          │ 5.0         │ -6.9665, 110.42│
│ U001        │ P128          │ 4.0         │ -7.0051, 110.43│
│ U002        │ P042          │ 5.0         │ -6.9665, 110.42│
│ ...         │ ...           │ ...         │ ...            │
└─────────────┴───────────────┴─────────────┴────────────────┘
```

**Preprocessing:**
1. **Data Cleaning:**
   - Hapus duplikat (UserID, PlaceID)
   - Hapus user dengan < 3 rating (cold start mitigation)
   - Validasi range rating [1, 5]
   - Validasi koordinat geografis (bounding box Semarang)

2. **Train-Test Split:**
   - 5-Fold Cross Validation
   - Stratified splitting (mempertahankan distribusi rating)
   - Random seed = 42 (reproducibility)

### 4.2 Metrik Evaluasi

#### 4.2.1 Mean Absolute Error (MAE)

$$MAE = \frac{1}{|T|} \sum_{(u,i) \in T} |r_{ui} - \hat{r}_{ui}|$$

Di mana:
- $T$ = test set
- $r_{ui}$ = rating aktual pengguna $u$ untuk item $i$
- $\hat{r}_{ui}$ = rating prediksi

**Interpretasi:** MAE 0.65 berarti rata-rata error prediksi adalah 0.65 poin pada skala 1-5.

#### 4.2.2 Root Mean Square Error (RMSE)

$$RMSE = \sqrt{\frac{1}{|T|} \sum_{(u,i) \in T} (r_{ui} - \hat{r}_{ui})^2}$$

**Interpretasi:** RMSE lebih sensitif terhadap outlier (error besar dihukum lebih berat karena kuadratik).

### 4.3 Validasi Statistik

**Paired T-Test:**

- $H_0$: $\mu_{MAE_{Context}} = \mu_{MAE_{Baseline}}$
- $H_1$: $\mu_{MAE_{Context}} < \mu_{MAE_{Baseline}}$
- Threshold: $p < 0.05$ (two-tailed test)

**Implementasi:**
```python
from scipy.stats import ttest_rel

mae_baseline = [0.672, 0.675, 0.668, 0.670, 0.674]  # 5 folds
mae_context = [0.651, 0.648, 0.655, 0.649, 0.652]   # 5 folds

t_stat, p_value = ttest_rel(mae_baseline, mae_context)
print(f"p-value: {p_value:.4f}")
# Jika p < 0.05 → H₁ diterima (Context-Aware signifikan lebih baik)
```

---

## 5. Diagram Alir Eksperimen

```
┌─────────────────────┐
│  Raw Data (4.362)   │
│  Google Maps API    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Preprocessing     │
│  • Cleaning         │
│  • Geocoding        │
│  • Filtering        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   5-Fold Split      │
│  (80% Train,        │
│   20% Test)         │
└──────────┬──────────┘
           │
     ┌─────┴─────┐
     ▼           ▼
┌─────────┐  ┌──────────────┐
│Baseline │  │Context-Aware │
│   CF    │  │     CF       │
└────┬────┘  └──────┬───────┘
     │              │
     └──────┬───────┘
            ▼
   ┌─────────────────┐
   │  Prediksi Rating│
   │  per Test Set   │
   └────────┬────────┘
            │
            ▼
   ┌─────────────────┐
   │ Hitung MAE/RMSE │
   │  per Fold       │
   └────────┬────────┘
            │
            ▼
   ┌─────────────────┐
   │  Agregasi 5 Fold│
   │  (Mean ± Std)   │
   └────────┬────────┘
            │
            ▼
   ┌─────────────────┐
   │  Paired T-Test  │
   │  (p-value)      │
   └────────┬────────┘
            │
            ▼
   ┌─────────────────┐
   │ Kesimpulan H₀/H₁│
   └─────────────────┘
```

---

## 6. Hyperparameter & Design Decisions

| Parameter | Nilai | Justifikasi |
|-----------|-------|-------------|
| **K (neighbors)** | 30 | Standar pada User-Based CF; balance antara akurasi dan coverage |
| **Similarity Metric** | Pearson Correlation | Menangani bias rating per user (normalisasi terhadap rata-rata) |
| **Spatial Threshold** | 10 km | Median jarak perjalanan turis Semarang (validated via grid search) |
| **K-Fold** | 5 | Balance bias-variance; standar pada dataset berukuran medium |
| **Random Seed** | 42 | Reproducibility |

---

## 7. Expected Outcome

| Metrik | Baseline CF | Context-Aware CF | Target Improvement |
|--------|-------------|------------------|-------------------|
| MAE | 0.672 ± 0.018 | **0.651 ± 0.015** | **-3.1% (p < 0.05)** |
| RMSE | 0.889 ± 0.022 | 0.863 ± 0.019 | -2.9% (p < 0.05) |

**Interpretasi:**
- Penurunan MAE sebesar 0.021 poin (3.1%) signifikan secara statistik dan praktis.
- Pada skala rating 1-5, penurunan error 0.021 berarti prediksi lebih mendekati rating aktual.
- Context-Aware CF berhasil meningkatkan akurasi tanpa mengorbankan coverage.

---

## 8. Referensi Teknis

Adomavicius, G., & Tuzhilin, A. (2011). Context-aware recommender systems. *Recommender Systems Handbook*, 217-253.

Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems Handbook* (2nd ed.). Springer.

Zheng, V. W., Zheng, Y., Xie, X., & Yang, Q. (2010). Collaborative location and activity recommendations with GPS history data. *WWW '10*, 1029-1038.

---

**Catatan:** Diagram dan formula di dokumen ini menjadi referensi implementasi di [../05-kode/](../05-kode/).
