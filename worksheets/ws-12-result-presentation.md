# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah integrasi filter jarak geospasial (Context-Aware) dapat menurunkan tingkat error pada sistem rekomendasi pariwisata?
Metrik Utama      : MAE (Mean Absolute Error) dan RMSE (Root Mean Squared Error)
```

Tabel Hasil (Berdasarkan Data Riil 4.362 Baris):
| Skenario                      | MAE (mean ± std) | RMSE (mean ± std) | n |
|-------------------------------|------------------|-------------------|---|
| Context-Aware CF (Intervensi) | 0.651 ± 0.016    | 0.945 ± 0.010     | 5 |
| Standard CF (Baseline)        | 0.672 ± 0.013    | 0.957 ± 0.012     | 5 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik                     | Pesan Utama                                                       | Metrik      |
|---|----------------------------------|-------------------------------------------------------------------|-------------|
| 1 | Grouped Bar Chart + Error Bar    | Context-Aware CF konsisten menghasilkan error yang lebih rendah.  | Mean ± std  |
| 2 | Box Plot                         | Distribusi sebaran nilai error (mengukur stabilitas antar run).   | Semua run   |

```
Bias Check:
  [x] Y-axis mulai dari 0 (atau dijustifikasi)
  [x] Error bar/CI ditampilkan
  [x] Semua data disertakan (tidak cherry-picked)
  [x] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen (menggunakan data riil hasil eksekusi 5 runs K-Fold).

| Skenario | MAE (mean ± std) | RMSE (mean ± std) | n |
|----------|------------------|-------------------|---|
| Context-Aware CF | 0.651 ± 0.016 | 0.945 ± 0.010 | 5 |
| Standard CF (Baseline) | 0.672 ± 0.013 | 0.957 ± 0.012 | 5 |

**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± std (bukan single number)
- [x] Diurutkan berdasarkan metrik utama (performa terbaik di atas)
- [x] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Grouped Bar Chart dengan Error Bar | Menggambarkan secara jelas bahwa algoritma Context-Aware mengungguli Baseline secara signifikan di kedua metrik. | Rata-rata (mean) MAE & RMSE dari 5 *runs*, ditambah *standard deviation*. |
| 2 | Box Plot | Menunjukkan sebaran variansi data dari 5 kali eksekusi untuk membuktikan bahwa kestabilan metode Context-Aware bukan sebuah kebetulan acak. | Seluruh data titik MAE dari total 10 eksekusi (5 Baseline, 5 Context-Aware). |
| 3 | Scatter Plot | Menunjukkan *trade-off* bahwa algoritma Context-Aware mungkin butuh komputasi tambahan, namun sepadan dengan penurunan *error*. | Waktu eksekusi (detik) vs Nilai MAE. |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | **Ya.** Karena Y-axis dipotong dan dimulai dari 90%, perbedaan 0.4% akan terlihat sangat ekstrem (Metode A seolah dua kali lipat lebih bagus dari B), padahal secara statistik perbedaannya sangat tipis. |
| Apakah error bar ditampilkan? | **Tidak.** Tidak ada *error bar* yang ditampilkan sehingga kita tidak tahu apakah perbedaan 0.4% itu signifikan atau hanya varians acak (kebetulan). |
| Apakah semua kondisi ditampilkan? | (Asumsi) Jika metode yang diuji ada banyak, tapi hanya Metode A dan B yang disajikan, berarti ada indikasi *cherry-picking* (memilih data yang bagus saja). |
| Apa solusinya? | 1. Mulai Y-axis dari 0% (atau minimal berikan skala yang lebih luas dan transparan).<br>2. Tambahkan *error bar* dari standar deviasi *multiple runs*. |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: -

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

**Jawaban:**

> Tabel dan grafik memiliki fungsi kognitif yang berbeda namun saling melengkapi. **Grafik** berfungsi untuk "bercerita" secara instan; audiens dapat melihat tren, perbandingan, dan pola dalam hitungan detik. Namun, grafik seringkali kekurangan presisi. Di sinilah peran **Tabel** yang menyajikan angka pasti (presisi desimal) bagi pembaca/dosen yang ingin melakukan verifikasi ulang perhitungan secara matematis. 
> 
> Sebelumnya, saat membuat laporan tugas dengan Microsoft Excel, saya sering membiarkan Excel mengatur rentang Y-axis secara otomatis (auto-scaling). Saya baru sadar bahwa hal tersebut secara tidak sengaja sering membuat grafik yang menyesatkan (*truncated axis*), di mana perbedaan nilai yang aslinya sangat kecil malah terlihat sangat dramatis. Ke depannya, saya akan selalu mengecek ulang batas mulai sumbu-Y di nol (0) atau menjelaskannya dengan transparan jika angkanya sengaja dipotong untuk *zooming*.