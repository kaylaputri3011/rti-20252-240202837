# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

---
VARIABLE & METRIC DEFINITION
Research Question: Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan performa User-Based CF standar milik Cholil dkk. (2023) pada dataset rating pariwisata Semarang?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Jenis Algoritma | IV | Metode komputasi rekomendasi | Kategori (Context-Aware CF vs Standar CF) | Nominal | — | Menjalankan *script* algoritma pada *environment* Python | Algoritma adalah *treatment* (perlakuan) utama yang dimanipulasi untuk menguji hipotesis perbaikan performa. |
| Akurasi Prediksi | DV | Tingkat *error* atau kesalahan tebakan sistem | Mean Absolute Error (MAE) | Ratio | Poin (0-4) | Menghitung selisih absolut rata-rata antara rating prediksi sistem dengan rating aktual pengguna di data uji | MAE adalah metrik standar (SOTA) yang merepresentasikan jarak simpangan tebakan secara linear dan transparan. |
| Kondisi Eksperimen | CV | Validitas internal pengujian | Nilai K pada *K-Fold Cross Validation* dan *Dataset Size* | Ratio | — | Menetapkan nilai *K=5* dan menggunakan 100% dataset yang sama untuk kedua iterasi algoritma | Menjaga agar perbedaan performa DV murni karena IV, bukan karena perbedaan porsi data latih/uji. |
```
Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [x] Setiap langkah terdokumentasi
  [x] Tidak ada "lompatan logis"
  [x] Metrik mengukur apa yang dimaksud (construct validity)
  ```
---

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Sejauh mana integrasi variabel Context-Aware (jarak dan waktu) pada algoritma User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan performa User-Based CF standar pada dataset rating pariwisata Semarang?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Model Algoritma | IV | Pendekatan penyaringan informasi | Kategori: Context-Aware CF vs Standar CF | Nominal | - |
| Akurasi Sistem | DV | (Tingkat Kesalahan (Error Rate) | MAE (Mean Absolute Error) | Ratio | Poin Rating (0-4) |
| Lingkungan Uji | CV | Stabilitas & Reproduksibilitas | Parameter K-Fold (k=5) & Set Data | Ratio  | - |

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana? -
(Rantai sudah solid: karena ingin tahu algoritma mana yang paling akurat, maka harus membandingkan dua metode spesifik dan mengukur selisih ratingnya menggunakan metrik matematis baku).
---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 | Sangat mewakili MAE secara langsung mencerminkan seberapa jauh melesetnya tebakan sistem dari rating asli yang diberikan wisatawan. |
| Sensitive | 4 | Sensitif terhadap perubahan pembobotan parameter algoritma, meskipun tidak terlalu menghukum error yang berukuran sangat ekstrem (outlier). |
| Feasible | 5 | Sangat mudah diimplementasikan, waktu komputasi perhitungannya ringan (hanya operasi pengurangan dan rata-rata), dan tidak butuh biaya survei tambahan karena data sudah berbentuk angka. |

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Root Mean Square Error (RMSE). Dibutuhkan sebagai metrik sekunder karena RMSE memberikan penalti lebih besar pada error yang parah (misalnya tebakannya meleset 3 bintang). Ini membantu melihat apakah algoritma Context-Aware tidak hanya akurat secara rata-rata, tetapi juga mampu menekan jumlah tebakan yang sangat melenceng.

**Contoh kasus ceiling effect untuk metrik ini:**
> Ketika dataset yang digunakan sangat bersih atau terlalu mudah diprediksi, nilai MAE mungkin sudah mencapai 0.01 (hampir sempurna). Dalam kondisi ini, membuktikan bahwa algoritma usulan lebih baik dari algoritma standar menjadi sangat sulit karena performa dasar sudah mentok (efek batas atas akurasi/ceiling effect).

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | *Apakah semua data point terkumpul?* | Tidak, data pasti sparse (matriks bolong-bolong) karena tidak ada turis yang mengulas semua tempat. | Menetapkan ambang batas (threshold): hanya mengambil user yang minimal sudah memberi rating di 3 tempat berbeda. |
| Consistency | *Apakah ada kontradiksi internal?* | Mungkin. Ada pengguna yang selalu memberi bintang 5 (spam/bot) atau memberi rating di 10 lokasi berbeda pada detik yang sama. | Melakukan data cleaning untuk menghapus user anomali berdasarkan pola timestamp dan varians rating. |
| Validity | *Apakah benar-benar mengukur yang dimaksud?* | Sebagian besar ya, namun rating bintang 5 di aplikasi bisa saja bukan karena wisatanya bagus, tapi tiketnya murah. | Secara metodologi diakui sebagai limitasi (tidak murni kepuasan fasilitas), namun secara praktis matriks angka tetap valid untuk melatih machine learning. |
| Representativeness | *Apakah sampel mewakili populasi target?* | Mewakili turis digital (yang terbiasa pakai smartphone), tapi kurang mewakili turis konvensional/lansia. | Menyatakan batasan demografi secara transparan di dalam paper pada sub-bab Limitasi Riset. |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Menentukan metrik setelah melihat data dianggap sebagai p-hacking (atau HARKing - Hypothesizing After the Results are Known) karena peneliti secara sengaja menyeleksi metrik yang hanya menguntungkan hipotesisnya dan menyembunyikan metrik yang menunjukkan kegagalan sistem. Ini melanggar objektivitas ilmiah karena manipulasi kondisi eksperimen demi mengejar status "signifikan" (p-value < 0.05).
> Perbedaannya dengan eksplorasi data yang sah (Exploratory Data Analysis) terletak pada niat dan pelaporannya. Eksplorasi yang sah diumumkan secara transparan sebagai "analisis tambahan" (post-hoc) untuk menemukan pola-pola menarik yang di luar hipotesis awal (misalnya: "Meskipun secara MAE tidak signifikan, kami tidak sengaja menemukan pola menarik pada pengguna remaja..."). Eksplorasi sah tidak menutupi metrik utama (Confirmatory) yang gagal.
