# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Penelitian sistem rekomendasi sebelumnya (Cholil et al., 2023) menggunakan User-Based Collaborative Filtering (CF) murni yang hanya bertumpu pada matriks rating, sehingga rentan memberikan rekomendasi yang tidak logis secara geografis dan temporal (mengabaikan jarak tempuh dan jam operasional wisata).

Research Question:
  Tipe         : [ ] Comparison  [x] Improvement  [ ] Exploratory
  Formulasi    : Apakah penambahan pembobotan Context-Aware (variabel jarak geolokasi dan jam operasional) pada algoritma User-Based Collaborative Filtering mampu menghasilkan nilai Mean Absolute Error (MAE) yang lebih rendah dibandingkan User-Based CF standar pada dataset ulasan wisata Kota Semarang?
  Variabel IV  : Jenis Algoritma (Context-Aware User-Based CF vs User-Based CF Standar).
  Variabel DV  : Akurasi prediksi sistem rekomendasi.
  Metrik       : Mean Absolute Error (MAE).
  Dataset      : Dataset rating wisatawan di Kota Semarang yang diperkaya dengan anotasi geolokasi (latitude/longitude) dan timestamp kunjungan.
  Baseline     : User-Based Collaborative Filtering murni (menggunakan Pearson Correlation tanpa filter konteks).

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [x] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Bukti empiris mengenai seberapa besar persentase peningkatan akurasi (*error reduction*) ketika variabel geospasial dan temporal disuntikkan ke dalam sistem matriks rating klasik pada skala pariwisata lokal.
  Jenis kontribusi        : [x] Improvement  [ ] Comparison  [ ] Novel approach
  Gap yang diisi          : Context Gap & Method Gap (kurangnya adopsi *Location-Based Service* pada CF tradisional).

Hypothesis Pair:
  H₀ : Tidak ada penurunan nilai Mean Absolute Error (MAE) yang signifikan secara statistik antara algoritma Context-Aware User-Based CF dibandingkan dengan User-Based CF standar.
  H₁ : Terdapat penurunan nilai Mean Absolute Error (MAE) yang signifikan secara statistik pada algoritma Context-Aware User-Based CF dibandingkan dengan User-Based CF standar.
  Threshold              : *p-value* < 0.05 (menggunakan *Paired T-Test* pada hasil iterasi) dan penurunan metrik MAE absolut minimal 10%.
  Justifikasi threshold  : Penurunan MAE di bawah 10% dalam konteks sistem rekomendasi dengan rating 1-5 bintang (skala kecil) seringkali tidak terasa perbedaannya (*imperceptible*) oleh pengguna akhir, sehingga secara praktikal tidak membenarkan penambahan kompleksitas komputasi.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Jarangnya integrasi antara metode Collaborative Filtering tradisional dengan pemrosesan Location-Based Service (LBS) dan Waktu (Context-Awareness) secara simultan untuk destinasi wisata di Semarang.

**RQ versi pertama (tulis bebas):**
> Apakah menggabungkan Collaborative Filtering dengan data lokasi dan waktu bisa membuat rekomendasi wisata jadi lebih bagus dan akurat untuk wisatawan Semarang?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | Belum spesifik | Hanya menyebut "menggabungkan dengan data lokasi", algoritma persisnya belum jelas. |
| Metrik terukur | Tidak | Kata "lebih bagus/akurat" terlalu abstrak. |
| Baseline | Tidak | "Lebih bagus" dibandingkan apa? Tidak disebutkan. |
| Dataset/konteks | Ya | Wisatawan Semarang. |

**Tipe RQ:** [ ] Comparison / [x] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah implementasi pembobotan Context-Aware (geolokasi dan waktu operasional) pada metode User-Based Collaborative Filtering mampu menghasilkan skor Mean Absolute Error (MAE) yang lebih rendah dibandingkan metode User-Based Collaborative Filtering standar (Cholil et al., 2023) pada dataset rating tempat wisata Kota Semarang?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Metode Context-Aware User-Based CF memberikan nilai MAE yang sama atau lebih besar dibandingkan User-Based CF standar pada dataset wisata Kota Semarang. |
| H₁ | Metode Context-Aware User-Based CF memberikan nilai MAE yang lebih kecil (lebih akurat) dibandingkan User-Based CF standar pada dataset wisata Kota Semarang. |
| Metrik | Mean Absolute Error (MAE). |
| Threshold | Penurunan MAE minimal 10% dan signifikansi uji statistik p-value < 0.05. |
| Justifikasi threshold | Syarat ketat ini membuktikan bahwa penambahan overhead komputasi (menghitung jarak GPS dan sinkronisasi waktu) benar-benar sepadan (worth it) dan dampaknya tidak terjadi hanya karena kebetulan acak pada dataset. |

**Apakah hipotesis ini falsifiable?** [x] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Bagaimana cara membuktikannya salah? Kita tinggal menjalankan eksperimen pada dataset uji (test set). Jika hasil running algoritma yang baru ternyata MAE-nya 1.2, sedangkan algoritma lama MAE-nya 0.85, maka H₁ langsung ditolak dan kita harus mengakui bahwa modifikasi metode kita gagal memperbaiki sistem (H₀ diterima).

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah implementasi pembobotan Context-Aware pada User-Based CF menghasilkan MAE lebih rendah dari User-Based CF standar pada data wisata Semarang? |
| Variable (IV) | Jenis Algoritma Rekomendasi (Context-Aware CF vs Standar CF). |
| Variable (DV) | Tingkat kesalahan prediksi rating (Prediction Error). |
| Metric | MAE (Mean Absolute Error) dan RMSE (Root Mean Square Error). |
| Data source | Dataset matriks user-item pariwisata Kota Semarang (minimal 500 records yang memuat kolom UserID, ItemID, Rating, Latitude, Longitude, Timestamp). |
| Analysis method | Evaluasi Offline dengan teknik K-Fold Cross Validation, dilanjutkan uji beda Paired Sample T-Test pada rerata skor MAE kedua algoritma. |

**Apakah rantai lengkap?** [x] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? -

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Sistem Rekomendasi Tempat Wisata Di Kota Semarang Menggunakan Metode Collaborative Filtering (Cholil et al., 2023).
**RQ yang diekstrak:** (Berdasarkan isi paparannya, paper ini secara implisit menanyakan) "Bagaimana cara merancang dan membangun sistem rekomendasi tempat wisata di Kota Semarang menggunakan metode Collaborative Filtering?"
**Komponen yang hilang:** RQ dari paper asli tersebut sangat bersifat Engineering-centric, bukan Research-centric. Metrik eksplisit tidak menjadi bagian dari pertanyaan awal, tidak ada Baseline yang diuji sebagai pembanding, dan rumusan ini tidak menuntut eksperimen hipotesis yang bisa gagal, melainkan hanya menuntut sebuah sistem fungsional berhasil dibangun (build and deploy).
