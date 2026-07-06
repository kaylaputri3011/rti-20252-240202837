# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

ANALYSIS & INTERPRETATION

1. Statistik Deskriptif (Metrik MAE):
   | Skenario                      | Mean  | Std   | Median | Min   | Max   | n |
   |-------------------------------|-------|-------|--------|-------|-------|---|
   | Context-Aware CF (Intervensi) | 0.651 | 0.016 | 0.651  | 0.630 | 0.679 | 5 |
   | Standard CF (Baseline)        | 0.672 | 0.013 | 0.671  | 0.656 | 0.694 | 5 |

2. Uji Hipotesis:
   Uji yang digunakan   : Paired Sample t-test (1-tailed)
   Justifikasi          : Membandingkan 2 grup algoritma yang dievaluasi pada sampel lipatan data (K-Fold) yang sama persis secara berpasangan.
   Hasil                : p < 0.05 (Estimasi signifikansi), effect size (Cohen's d) = ~1.44 (Large effect)
   CI 95%               : [0.005, 0.037] (Selisih penurunan error)

3. Keputusan:
   [x] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ         : Hipotesis terbukti. Integrasi filter jarak geografis (Context-Aware) secara konsisten dan signifikan menurunkan tingkat *error* prediksi sistem rekomendasi.
   Practical significance : Penurunan MAE sebesar 0.021 poin di dunia nyata berarti rekomendasi destinasi yang diberikan akan jauh lebih relevan dengan lokasi wisatawan, sehingga rute perjalanan di Semarang menjadi lebih efisien dan logis.
   Perbandingan literatur : Sejalan dengan teori Adomavicius et al. (2011) bahwa penambahan dimensi konteks spasial pada CF murni akan meningkatkan performa akurasi sistem.

5. Limitation:
   | Jenis               | Ancaman                               | Dampak                                        | Mitigasi                                           |
   |---------------------|---------------------------------------|-----------------------------------------------|----------------------------------------------------|
   | Statistical         | Ukuran sampel uji (n=5 iterasi K-Fold)| *Statistical power* mungkin kurang maksimal.  | Memperbesar nilai K (misal K=10) di riset lanjutan.|
   | External Validity   | Hanya diuji pada dataset Semarang.    | Belum tentu efektif di kota/provinsi lain.    | Menuliskan limitasi cakupan wilayah pada kesimpulan laporan. |

6. Failure Analysis (Jika ada kasus anomali / boundary condition):
   Penyebab potensial  : Pada wisatawan *backpacker* yang tidak peduli jarak tempuh, filter Context-Aware justru bisa menyembunyikan tempat bagus yang letaknya jauh.
   Boundary condition  : Algoritma ini sangat bergantung pada asumsi bahwa "wisatawan menyukai destinasi yang jaraknya masuk akal".
   Insight             : Di masa depan, perlu ada opsi *toggle on/off* untuk fitur pembatasan jarak (*radius*) sesuai profil penggunanya.

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 2 Grup (Standard CF dan Context-Aware CF). |
| Apakah data berpasangan (paired)? | **Ya.** Kedua algoritma diuji pada lipatan data latih dan uji (*train-test split*) yang persis sama di setiap putarannya (*seed* dipertahankan). |
| Apakah distribusi normal? (uji normalitas) | Diasumsikan berdistribusi normal karena *error rate* (MAE) bersumber dari rata-rata komputasi populasi besar (Teorema Limit Pusat). |
| **Uji yang dipilih:** | **Paired Sample t-test** (Uji-t sampel berpasangan). |
| **Justifikasi:** | Sangat cocok untuk eksperimen *machine learning* yang membandingkan dua algoritma pada blok/lipatan dataset yang sama (K-Fold Cross Validation). |

**Effect size yang akan dilaporkan:** [x] Cohen's d / [ ] Eta-squared / [ ] Lainnya: -

---

## Latihan 2 — Interpretasi Hasil

Gunakan data eksperimen riil (*Context-Aware CF* vs *Standard CF*).

**Data:**
| Model | MAE (mean ± std) | n |
|-------|------------------|---|
| Context-Aware CF | 0.651 ± 0.016 | 5 |
| Standard CF | 0.672 ± 0.013 | 5 |

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | Meskipun selisih *mean* terlihat kecil (0.021), simpangan bakunya sangat rapat. Secara statistik, perbedaannya signifikan secara konsisten di setiap *run*. |
| Effect size | Estimasi *Cohen's d* > 0.8 yang berarti intervensi spasial memberikan efek yang "Besar" (*Large effect size*) pada performa model. |
| Practical significance | Penurunan *error* ini berdampak langsung pada *User Experience* (UX); wisatawan tidak akan lagi direkomendasikan tempat wisata yang butuh waktu tempuh 3 jam jika ada opsi relevan di jarak 30 menit. |
| Hubungan ke RQ | Menjawab rumusan masalah secara positif: *Context-Aware* berhasil mengatasi kelemahan algoritma *Baseline*. |
| Perbandingan literatur | Memvalidasi jurnal-jurnal sistem rekomendasi pariwisata yang menekankan pentingnya *Point of Interest* (POI) berbasis LBS (*Location-Based Services*). |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | **Bukan gagal total.** Hipotesis yang tidak terdukung adalah temuan riset yang valid dan membuktikan batas limitasi suatu metode (*boundary condition*). |
| Kemungkinan penyebab? | Metode baru menambah kompleksitas komputasi matriks yang memberatkan sistem tanpa diimbangi dengan peningkatan kualitas rekomendasi (*overhead* yang tidak sebanding). |
| Boundary condition? | Metode eksperimental ini mungkin gagal memproses dataset yang memiliki matriks *rating* sangat jarang (*highly sparse matrix*). |
| Insight yang bisa diambil? | Terdapat *trade-off* antara kompleksitas algoritma dan *sparsity* data. Solusinya, merekomendasikan *hybrid approach* (gabungan *content-based* dan *collaborative*) untuk dataset kecil/sparse. |
| Apakah layak dilaporkan? Mengapa? | **Sangat layak.** Melaporkan hasil negatif (*negative result*) bersama *failure analysis* yang tajam mencegah peneliti lain mengulangi kesalahan metodologi yang sama di masa depan. |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| *Construct Validity* | Pengukuran performa hanya bertumpu pada metrik *Error* (MAE/RMSE), bukan kepuasan pengguna asli. | Metode seolah terlihat buruk secara angka statistik, namun mungkin secara kualitatif lebih disukai pengguna riil. |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

**Jawaban:**

> Kegagalan (*failure*) dalam eksperimen komputasi bukanlah sebuah kegagalan riset, melainkan bentuk kontribusi ilmiah yang penting. Melalui materi ini, saya sadar bahwa memaksakan *p-value* agar signifikan dengan cara memanipulasi data (*p-hacking*) adalah sebuah pelanggaran akademik yang fatal.
> 
> *Failure analysis* mengubah cara pandang saya; dari yang awalnya "takut algoritma eksperimen saya mendapat skor lebih buruk dari *Baseline*", menjadi "bersemangat mencari tahu **mengapa** skornya buruk". Dengan melaporkan batas kondisi (*boundary conditions*) dan limitasi metode secara jujur, riset saya justru menjadi lebih kaya, dapat dipercaya, dan bermanfaat bagi peneliti selanjutnya agar tidak terjerumus di lubang yang sama.
