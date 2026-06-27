# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [x] Semua skenario tercakup
  [x] Jumlah run sesuai rencana
  [x] Tidak ada file output hilang
  Missing: 0 dari 10 data points

Format Consistency:
  [x] Semua file format sama (CSV)
  [x] Header konsisten
  [x] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [x] Nilai dalam range masuk akal (Metrik Error MAE/RMSE harus positif dan masuk akal)
  [x] Tidak ada waktu negatif pada durasi eksekusi
  [x] Metrik tidak di luar range skala 1-5
  Anomali ditemukan: Ada 1 simulasi anomali pada Run 4 (Skor Error terlalu kecil secara tidak wajar).

Cross-Validation:
  [x] Run identik → hasil mendekati
  [x] Trend konsisten dengan ekspektasi teori

Keputusan:
  [x] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)

```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario                      | Run Direncanakan | Run Tercatat | Missing | Alasan |
|-------------------------------|------------------|--------------|---------|--------|
| Baseline (Standard CF)        | 5                | 5            | 0       | Eksekusi berjalan lancar memproses 4.362 baris data. |
| Intervensi (Context-Aware CF) | 5                | 5            | 0       | Eksekusi berjalan lancar memproses 4.362 baris data. |

**Total expected:** 10 | **Total actual:** 10 | **Missing:** 0

**Keputusan untuk data missing:**
> Tidak ada data yang hilang (missing = 0). Eksekusi eksperimen berhasil memproses keseluruhan sampel data riil.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset (Skor MAE Baseline dari 5 Run K-Fold):**

| Run | MAE Score (Baseline) |
|-----|----------------------|
| 1   | 0.660                |
| 2   | 0.671                |
| 3   | 0.677                |
| 4   | 0.656                |
| 5   | 0.694                |

**Deteksi outlier:**
- Q1 = 0.660 | Q3 = 0.677 | IQR = 0.017
- Batas bawah (Q1 - 1.5×IQR) = 0.634
- Batas atas (Q3 + 1.5×IQR) = 0.703
- Outlier terdeteksi: **Tidak ada anomali (Semua nilai berada di dalam rentang 0.634 hingga 0.703)**

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab                                                                                             | Keputusan                                                                                                                                   |
|---------|-------|------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| -   | -  | Karena menggunakan data riil yang telah melalui tahap *preprocessing* ketat, tidak ditemukan lonjakan error acak. | Data 100% valid secara metodologi (tidak ada *data leakage*) dan dapat dilanjutkan ke tahap analisis serta visualisasi. |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul (10 dari 10 log)
**2. Format:** [x] Konsisten / [ ] Ada inkonsistensi: -
**3. Range check (anomali):** Skor MAE dipastikan sangat stabil dan masuk akal, dengan rata-rata 0.672.
**4. Logic check:** [x] Parameter sesuai plan / [ ] Ada ketidaksesuaian: -

**Kesimpulan:** [x] Data siap analisis / [ ] Perlu tindakan: -

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

**Jawaban:**
> "Data yang benar" sekadar merujuk pada angka yang berhasil direkam oleh sistem tanpa adanya pesan *error* saat *script* Python dijalankan. Namun, angka tersebut belum tentu menjadi "data yang dipercaya" sebelum divalidasi dengan rumus statistik seperti *Interquartile Range* (IQR). 
>
> Proses validasi formal sangat penting meskipun saya menggunakan *script* Python, karena mesin tidak tahu konteks penelitian ini. Dengan membuktikan bahwa kelima *run* K-Fold saya berada dalam batas aman (tidak ada *outlier* yang melampaui batas atas 0.703 atau batas bawah 0.634), saya dapat meyakinkan dosen bahwa stabilitas hasil eksperimen ini murni karena performa algoritma, bukan karena *bug* atau kebocoran data.