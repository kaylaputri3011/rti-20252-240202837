# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan performa User-Based CF standar pada dataset rating pariwisata Semarang?
Hypothesis        : (H₁) Terdapat penurunan skor MAE yang signifikan secara statistik pada algoritma Context-Aware User-Based CF dibandingkan dengan User-Based CF standar.
Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Algoritma *baseline* tanpa filter konteks (mereplikasi paper Cholil dkk., 2023) | User-Based CF Standar | Dataset Semarang, K-Fold=5, Random Seed=42, Parameter tetangga (K)=20 |
| Treatment | Algoritma usulan yang menginkorporasikan jarak geografis dan jam buka | Context-Aware User-Based CF | Dataset Semarang, K-Fold=5, Random Seed=42, Parameter tetangga (K)=20 |

Fairness Checklist:
  [x] Dataset identik untuk semua kondisi
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    | *Data Leakage*: Secara tidak sengaja memasukkan rating masa depan ke data latih. | Menggunakan pembagian data latih/uji (*train/test split*) berbasis dimensi waktu (*time-aware split*). |
| External    | Karakteristik geografis kota Semarang mungkin terlalu unik, algoritma gagal di kota lain. | Membatasi ruang lingkup klaim hanya pada "pariwisata lokal perkotaan" di dokumen riset. |
| Construct   | MAE yang rendah mungkin tidak berarti wisatawan puas (*user satisfaction*). | Menambahkan RMSE sebagai metrik sekunder untuk melihat seberapa sering sistem membuat kesalahan fatal (tebakan meleset jauh). |
| Conclusion  | Ukuran sampel uji terlalu sedikit, hasil MAE terlihat bagus karena kebetulan (*chance*). | Melakukan iterasi *Repeated K-Fold Cross Validation* untuk mendapatkan ukuran sampel uji statistik yang lebih stabil (misal 30 iterasi). |

Statistical Plan:
  Uji statistik    : Paired Sample T-Test
  Justifikasi      : Membandingkan dua nilai rata-rata bersanding (MAE algoritma A vs MAE algoritma B) yang diuji pada potongan data latih/uji (folds) yang sama persis.
  Alpha            : 0.05
  Effect size min  : Penurunan MAE minimal sebesar 10%
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based CF mampu menghasilkan skor MAE yang lebih rendah dibandingkan User-Based CF standar pada dataset pariwisata Semarang?
**Tipe eksperimen:** [x] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Menguji metode baseline klasik dari literatur sebelumnya. | Standard User-Based CF | Dataset Semarang dengan porsi Train/Test 80:20, random_state=42 |
| Treatment | Menguji metode usulan dengan penambahan bobot jarak dan waktu. | Context-Aware CF | Dataset Semarang dengan porsi Train/Test 80:20, random_state=42 |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ | Kedua algoritma "disuapi" file CSV matriks rating yang sama persis. |
| Preprocessing setara | ✅ | Penghapusan data sparse dan imputasi data kosong dilakukan satu kali sebelum data masuk ke algoritma mana pun. |
| Tuning effort setara | ✅ | Kedua algoritma diberikan kesempatan optimasi parameter (GridSearch) dengan rentang percobaan iterasi yang sama. |
| Environment identik | ✅ | Dijalankan pada laptop/server yang sama dengan spesifikasi hardware (RAM, CPU) dan versi Python yang sama. |
| Metrik evaluasi sama | ✅ | Sama-sama diukur menggunakan fungsi kalkulasi perhitungan MAE dan RMSE yang sama dari pustaka scikit-learn. |

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya? -
> (Desain eksperimen sudah sangat fair dan terkontrol, mengikuti prinsip apple-to-apple comparison).

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Kesalahan konfigurasi K-Fold menyebabkan user yang sama berada di train sekaligus test set. | Memastikan algoritma memisahkan data berdasar User-ID, bukan pemotongan baris data acak. |
| External | Data crawling Google Maps mungkin berisi fake review yang tidak mencerminkan dunia nyata. | Menggunakan filter heuristik untuk membuang user yang memberi puluhan review dalam rentang 1 menit (terindikasi bot). |
| Construct | Metrik MAE gagal menangkap kasus di mana algoritma merekomendasikan tempat yang tutup. | Memastikan logika algoritma menghukum skor error menjadi maksimal jika memprediksi rating tinggi pada lokasi yang sedang tutup (secara temporal). |
| Conclusion | Uji parametrik (T-Test) tidak valid karena distribusi selisih error tidak normal. | Melakukan uji normalitas Shapiro-Wilk terlebih dahulu; jika tidak normal, gunakan uji non-parametrik Wilcoxon Signed-Rank Test. |

**Ancaman mana yang paling sulit dimitigasi?** 
> External Validity.

**Mengapa?**
> Karena sekuat apa pun algoritma Machine Learning yang kita buat, ia sangat bergantung pada kemurnian data (prinsip Garbage In, Garbage Out). Sangat sulit membedakan secara pasti 100% mana ulasan wisatawan asli yang benar-benar berkunjung, dan mana ulasan dari orang yang dibayar (buzzer) di platform publik. Hal ini membatasi seberapa jauh kita bisa menggeneralisasi hasil eksperimen ini ke populasi dunia nyata.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah baseline yang digunakan adalah State-of-the-Art (metode yang memang kuat/terbaru), atau sekadar straw man (metode usang yang sengaja dipilih agar mudah dikalahkan)?
2. Apakah peneliti melakukan tuning effort (hyperparameter optimization) yang sama kerasnya untuk baseline, ataukah mereka hanya melakukan tuning pada metode mereka sendiri sementara baseline menggunakan konfigurasi bawaan (default)?
3. Apakah performa unggul tersebut konsisten jika diuji pada dataset yang berbeda (external validity), atau algoritma tersebut hanya menghafal (overfitting) pada satu dataset spesifik yang menguntungkan metode mereka?
