# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
Dataset           : `dataset_semarang_real.csv` (Gabungan data ulasan dan koordinat tempat dari Google Maps)
Jumlah data awal  : 4.362 baris (Sesuai file CSV *raw* ekstraksi Apify)
```

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 0 kasus     | Verifikasi kelengkapan dataset | Setelah proses *merging* antara file ulasan dan file koordinat, seluruh 4.362 baris memiliki data lengkap (tidak ada *Null* pada kolom target maupun koordinat). |
| Duplikat| 0 kasus     | Pengecekan ID User & Item | Setiap baris mewakili interaksi unik antara satu *user* dan satu destinasi wisata. |
| Error   | 0 kasus     | Standardisasi tipe data | Memastikan kolom *Rating* bertipe numerik (float/int) sebelum masuk model. |

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
| Label Encoding | `UserID` & `ItemID` | Mengubah string nama menjadi angka indeks (contoh: "Bay Galihovic" -> 0, "Curug" -> 1). | Algoritma *Collaborative Filtering* (K-Fold dan kalkulasi matriks) membutuhkan *input* berupa integer, bukan teks/string. |
```

Normalization:
  Metode    : Tidak dilakukan normalisasi (*None*)
  Alasan    : Nilai target (*Rating*) sudah berada dalam skala ordinal alami yang terikat (1 hingga 5). Koordinat spasial (*Latitude/Longitude*) juga dipertahankan dalam nilai absolutnya agar kalkulasi jarak geografis (*Haversine*) tetap valid di dunia nyata.
  Parameter : N/A

Leakage Check:
  [x] Parameter perhitungan (contoh: rata-rata rating tempat / `item_means`) dihitung dari *training set* saja.
  [x] Tidak ada informasi *test set* yang bocor ke tahap *preprocessing*.
  [x] *Cross-validation* (K-Fold) dilakukan di awal sebelum perhitungan bobot model.

Jumlah data akhir : 4.362 baris (Data bersih yang siap dan sukses dianalisis)
Script tersedia   : [x] Ya → path: `clean_data.py` dan `run_experiment.py` | [ ] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| *Missing values* (N/A) | 0 dari 4.362 (0%) | Verifikasi menggunakan fungsi `dropna()` di Python | Dataset hasil ekstraksi (*crawler*) terbukti sangat berkualitas. Semua atribut esensial yang dibutuhkan oleh algoritma *Context-Aware* (UserID, ItemID, Rating, Lat, Lng) terisi penuh. |

**Jumlah data sebelum cleaning:** 4.362 baris 
**Jumlah data setelah cleaning:** 4.362 baris
**Persentase data yang hilang/berubah:** 0% (Dataset murni dan 100% utuh).

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| `Rating` (Target) | 1.0 – 5.0 | *Left-skewed* (Cenderung positif) | Tidak | Tidak perlu | Sudah berada dalam skala yang terstandar dan seragam [1, 5]. Melakukan *scaling* (misal ke 0-1) justru akan menghilangkan interpretabilitas nilai error MAE/RMSE. |
| `Latitude` & `Longitude` | -6.9 s/d -7.1 (Lat) | Terpusat di Semarang | Tidak | Tidak perlu | Jika dinormalisasi menggunakan Z-score, perhitungan jarak riil dalam kilometer akan menjadi rusak dan tidak relevan. |

**Apakah normalisasi diperlukan?** [ ] Ya / [x] Tidak
**Justifikasi:**
> Karakteristik dataset sistem rekomendasi spasial mewajibkan nilai *rating* dan koordinat bumi (Lat/Lon) dipertahankan dalam bentuk aslinya (*raw numeric*) agar fungsi jarak dan evaluasi metrik (*error rate* bintang) tetap masuk akal untuk diinterpretasikan (minimal distorsi).

**Leakage check:**
- [x] Parameter dihitung dari training set saja (Nilai rata-rata item dihitung **setelah** fungsi K-Fold Split dijalankan).
- [x] Normalisasi diterapkan setelah train-test split (N/A).

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: dataset_semarang_real.csv (Google Maps Reviews)
2. Data awal: 4.362 records, 6 features utama (UserID, ItemID, Rating, Lat, Lng, Timestamp)
3. Cleaning:
   - Missing values: 0 kasus (dataset utuh 100%)
   - Duplikat: 0 kasus, tindakan: Verifikasi dataset iterasi
   - Error: 0 kasus, tindakan: Filter format string ke float
4. Transformation: Label Encoding pada variabel 'UserID' dan 'ItemID' menggunakan fungsi pandas `.cat.codes` untuk mengubah teks string menjadi integer.
5. Normalisasi: Tidak dilakukan (metode: None), parameter dipertahankan pada skala asli (Rating 1-5, Lat/Lon koordinat derajat).
6. Data akhir: 4.362 records, 6 features
7. Leakage check: [x] Lulus (Validasi ketat: perhitungan nilai rata-rata/item_means murni bersumber dari subset training `train.groupby()`) / [ ] Ada masalah.

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

**Jawaban**

> Sebelum mempelajari materi ini, saya sering beranggapan bahwa setiap dataset Machine Learning wajib melalui tahap normalisasi (seperti Min-Max Scaler ke rentang 0-1) agar model menjadi lebih pintar. Saya baru menyadari prinsip Minimal Distortion; bahwa mengubah data sesedikit mungkin justru lebih baik jika normalisasi tidak benar-benar diperlukan.

> Pada eksperimen rekomendasi pariwisata ini, saya memutuskan tidak melakukan normalisasi pada variabel Rating dan Koordinat. Risiko over-preprocessing jika saya menormalisasi data tersebut adalah hancurnya interpretabilitas evaluasi (dosen/pengguna tidak akan paham jika nilai error MAE adalah 0.05 dalam skala Z-score, dibandingkan dengan MAE 0.65 dalam skala rating bintang 1-5), serta rusaknya perhitungan jarak geografis riil antar tempat wisata. Selain itu, saya juga belajar pentingnya mencegah Data Leakage dengan cara memisahkan data latih dan uji (K-Fold) terlebih dahulu sebelum menghitung nilai rata-rata (mean) parameter.